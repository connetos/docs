BGP配置
=======================================

BGP简介
---------------------------------------

概述
+++++++++++++++++++++++++++++++++++++++
为方便管理规模不断扩大的网络，网络被分成了不同的自治系统。

BGP（Border Gateway Protocol，边界网关协议）是一种实现自治系统AS（Autonomous System）之间的路由可达，并选择最佳路由的距离矢量路由协议。

BGP具有以下优点：
 * BGP采用认证和GTSM的方式，保证了网络的安全性。
 * BGP提供了丰富的路由策略，能够灵活的进行路由选路。
 * BGP提供了路由聚合和路由衰减功能用于防止路由振荡，有效提高了网络的稳定性。
 * BGP使用TCP作为其传输层协议（端口号为179），并支持BGP与BFD联动、BGP Auto FRR和BGP GR和NSR，提高了网络的可靠性。

常用概念
+++++++++++++++++++++++++++++++++++++++

自治系统AS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
AS(Autonomous System，自治系统)是指在一个实体管辖下的拥有相同选路策略的IP网络。

BGP网络中的每个AS都被分配一个唯一的AS号，用于区分不同的AS。AS号分为2字节AS号和4字节AS号，其中2字节AS号的范围为1至65535，4字节AS号的范围为1至4294967295。支持4字节AS号的设备能够与支持2字节AS号的设备兼容。

报文交互中的角色
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
BGP报文交互中分为Speaker和Peer两种角色。

 * Speaker：发送BGP报文的设备称为BGP发言者（Speaker），它接收或产生新的报文信息，并发布（Advertise）给其它BGP Speaker。
 * Peer：相互交换报文的Speaker之间互称对等体（Peer）。若干相关的对等体可以构成对等体组（Peer Group）。

BGP的Router ID
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
BGP的Router ID是一个用于标识BGP设备的32位值，通常是IPv4地址的形式，在BGP会话建立时发送的Open报文中携带。对等体之间建立BGP会话时，每个BGP设备都必须有唯一的Router ID，否则对等体之间不能建立BGP连接。

BGP的Router ID在BGP网络中必须是唯一的，可以采用手工配置，也可以让设备自动选取。缺省情况下，BGP选择设备上的Loopback接口的地址作为BGP的Router ID。如果设备上没有配置Loopback接口，系统会选择接口中最大的IPv4地址作为BGP的Router ID。

BGP分类
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
BGP按照运行方式分为EBGP（External/Exterior BGP）和IBGP（Internal/Interior BGP）

 * EBGP：运行于不同AS之间的BGP称为EBGP。为了防止AS间产生环路，当BGP设备接收EBGP对等体发送的路由时，会将带有本地AS号的路由丢弃。
 * IBGP：运行于同一AS内部的BGP称为IBGP。为了防止AS内产生环路，BGP设备不将从IBGP对等体学到的路由通告给其他IBGP对等体，并与所有IBGP对等体建立全连接。IBGP对等体的连接数量太多时，可以用路由反射器和BGP联盟来减少连接的数量。

路由反射器RR
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
为保证IBGP对等体之间的连通性，需要在IBGP对等体之间建立全连接关系。当设备数目很多时，设备配置将十分复杂，而且配置后网络资源和CPU资源的消耗都很大。在IBGP对等体间使用路由反射器可以解决以上问题。

路由反射器相关角色为 ＃这里画一个图形表示，和rr的连接用实线表示，全连接用虚线表示。或者放一个对比图。看实际效果

同一cluster内的客户机只需要与该集群的RR建立IBGP连接，不需要与其他客户机建立IBGP连接，从而减少了IBGP连接数量。

RR突破了“从IBGP对等体获得的BGP路由，BGP设备只发布给它的EBGP对等体。”的限制，并采用独有的Cluster_List属性和Originator_ID属性防止路由环路。RR向IBGP邻居发布路由规则如下：#这段话需要再理一下，放到最前的介绍去

 * 从非客户机学到的路由，发布给所有客户机。
 * 从客户机学到的路由，发布给所有非客户机和客户机（发起此路由的客户机除外）。
 * 从EBGP对等体学到的路由，发布给所有的非客户机和客户机。


BGP联盟
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
和RR一样，BGP联盟也是为了解决AS内部的IBGP网络连接激增问题。

联盟将一个AS划分为若干个子AS。每个子AS内部建立IBGP全连接关系，子AS之间建立联盟EBGP连接关系，但联盟外部AS仍认为联盟是一个AS。配置联盟后，原AS号将作为每个路由器的联盟ID。

这样的好处是：

 * 可以保留原有的IBGP属性，包括Local Preference属性、MED属性和NEXT_HOP属性等
 * 联盟相关的属性在传出联盟时会自动被删除，即管理员无需在联盟的出口处配置过滤子AS号等信息的操作。

路由衰减
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
路由振荡指路由表中添加一条路由后，该路由又被撤销的过程。当发生路由振荡时，设备就会向邻居发布路由更新，收到更新报文的设备需要重新计算路由并修改路由表。当BGP应用于复杂的网络环境时，路由振荡就会十分频繁。为了避免频繁的路由振荡，BGP使用路由衰减来抑制不稳定的路由。

路由衰减只对EBGP路由起作用，对IBGP路由不起作用。

＃增加一个图形

路由衰减使用惩罚值（Penalty value）来衡量一条路由的稳定性，惩罚值越高说明路由越不稳定。

#. 路由每发生一次振荡，BGP便会给此路由增加1000的惩罚值，其余时间惩罚值会慢慢下降。
#. 当惩罚值超过抑制阈值（suppress value）时，此路由被抑制，不加入到路由表中，也不再向其他BGP对等体发布更新报文。
#. 被抑制的路由每经过一段时间，惩罚值便会减少一半，这个时间称为半衰期（half-life）。
#. 当惩罚值降到再使用阈值（reuse value）时，此路由变为可用并被加入到路由表中，同时向其他BGP对等体发布更新报文。

从路由被抑制到路由恢复可用的时间称为抑制时间（suppress time）。

工作原理
+++++++++++++++++++++++++++++++++++++++

BGP的报文类型
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
BGP对等体间通过以下5种报文进行交互，其中Keepalive报文为周期性发送，其余报文为触发式发送：

 * Open报文：用于建立BGP对等体连接。
 * Update报文：用于在对等体之间交换路由信息。
 * Notification报文：用于中断BGP连接。
 * Keepalive报文：用于保持BGP连接。
 * Route-refresh报文：用于在改变路由策略后请求对等体重新发送路由信息。只有支持路由刷新（Route-refresh）能力的BGP设备会发送和响应此报文。

BGP对等体交互过程
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
BGP对等体的交互过程中存在6种状态机：

 * 空闲（Idle）
 * 连接（Connect）
 * 活跃（Active）
 * Open报文已发送（OpenSent）
 * Open报文已确认（OpenConfirm）
 * 连接已建立（Established）。

 在BGP对等体建立的过程中，通常可见的3个状态是：Idle、Active和Established。 

BGP对等体交互过程如下：

#.Idle状态是BGP初始状态。在Idle状态下，BGP拒绝邻居发送的连接请求。只有在收到本设备的Start事件后，BGP才开始尝试和其它BGP对等体进行TCP连接，并转至Connect状态。

  ..note:: 
   * Start事件是由一个操作者配置一个BGP过程，或者重置一个已经存在的过程或者路由器软件重置BGP过程引起的。
   * 任何状态中收到Notification报文或TCP拆链通知等Error事件后，BGP都会转至Idle状态。

#. 在Connect状态下，BGP启动连接重传定时器（Connect Retry），等待TCP完成连接。
   
   * 如果TCP连接成功，那么BGP向对等体发送Open报文，并转至OpenSent状态。
   * 如果TCP连接失败，那么BGP转至Active状态。
   * 如果连接重传定时器超时，BGP仍没有收到BGP对等体的响应，那么BGP继续尝试和其它BGP对等体进行TCP连接，停留在Connect状态。

#. 在Active状态下，BGP总是在试图建立TCP连接。

   * 如果TCP连接成功，那么BGP向对等体发送Open报文，关闭连接重传定时器，并转至OpenSent状态。
   * 如果TCP连接失败，那么BGP停留在Active状态。
   * 如果连接重传定时器超时，BGP仍没有收到BGP对等体的响应，那么BGP转至Connect状态。

#. 在OpenSent状态下，BGP等待对等体的Open报文，并对收到的Open报文中的AS号、版本号、认证码等进行检查。

   * 如果收到的Open报文正确，那么BGP发送Keepalive报文，并转至OpenConfirm状态。
   * 如果发现收到的Open报文有错误，那么BGP发送Notification报文给对等体，并转至Idle状态。

#. 在OpenConfirm状态下，BGP等待Keepalive或Notification报文。如果收到Keepalive报文，则转至Established状态，如果收到Notification报文，则转至Idle状态。

#. 在Established状态下，BGP可以和对等体交换Update、Keepalive、Route-refresh报文和Notification报文。
   * 如果收到正确的Update或Keepalive报文，那么BGP就认为对端处于正常运行状态，将保持BGP连接。
   * 如果收到错误的Update或Keepalive报文，那么BGP发送Notification报文通知对端，并转至Idle状态。
   * Route-refresh报文不会改变BGP状态。
   * 如果收到Notification报文，那么BGP转至Idle状态。
   * 如果收到TCP拆链通知，那么BGP断开连接，转至Idle状态。

BGP对等体之间的交互原则
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
BGP设备将最优路由加入BGP路由表，形成BGP路由。BGP设备与对等体建立邻居关系后，采取以下交互原则：
从IBGP对等体获得的BGP路由，BGP设备只发布给它的EBGP对等体。
从EBGP对等体获得的BGP路由，BGP设备发布给它所有EBGP和IBGP对等体。
当存在多条到达同一目的地址的有效路由时，BGP设备只将最优路由发布给对等体。
路由更新时，BGP设备只发送更新的BGP路由。
所有对等体发送的路由，BGP设备都会接收。


配置BGP基本功能
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. （可选）配置BGP使用的AS编号形式。
   
   ConnetOS# **set protocols bgp 4byte-as-numbers enable** { **false** | **true** }

   缺省情况下，BGP不使用4字节的AS编号，使用2字节的AS编号。

#. 设置BGP设备的Router ID。
   
   ConnetOS# **set protocols bgp bgp-id** *bgp-id*

   缺省情况下，设备没有配置Router ID。

#. 提交配置。

   ConnetOS# **commit**

配置
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 使能BGP联盟。
 
   ConnetOS# **set protocols bgp confederation enable** { **false** | **true** }

#. 设置联盟ID。
 
   ConnetOS# **set protocols bgp confederation identifier** *confederation-id*

#. 设置联盟中的子自治系统

#. 提交配置。

   ConnetOS# **commit**



配置BGP网络的收敛速度
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 使能BGP路由衰减功能。
 
   ConnetOS# **set protocols bgp damping enable** { **false** | **true** }

   缺省情况下，路由衰减功能是使能的。

#. 设置路由进入抑制状态的抑制阈值。

   ConnetOS# **set protocols bgp damping suppress** *suppress-value*

   缺省情况下，抑制阈值是3000。

#. 设置路由的抑制时间。

   ConnetOS# **set protocols bgp damping max-suppress** *max-suppress-time*

   缺省情况下，路由抑制时间是60分钟。

#. 设置可达路由的半衰期。

   ConnetOS# **set protocols bgp damping half-life** *half-life*

   缺省情况下，半衰期是15分钟。

#. 设置路由解除抑制状态时的再使用阈值。

   ConnetOS# **set protocols bgp damping reuse** *reuse-value*

   缺省情况下，再使用阈值是750。

#. 提交配置。

   ConnetOS# **commit**

