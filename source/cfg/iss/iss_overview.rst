简介
=======================================

概述
---------------------------------------
随着数据中心数据访问量的逐渐增大，对交换机提出了高密度端口、高可靠性、高性能的要求，而单台交换机由于存在单点异常、端口数量等问题已经无法满足数据中心的需求，交换机虚拟化技术（如堆叠）应运而生。

ConnetOS支持的ISS（Intelligent Stacking System）堆叠功能，是指将两台及以上的交换机组合在一起，从逻辑上组成一台交换机。用户通过对这台“逻辑交换机”的管理，实现对堆叠中所有交换机的管理。

通过堆叠，可以实现网络高可靠性和网络大数据量转发，同时简化网络管理。ISS堆叠主要有以下优点：

 * 简化运维。整个堆叠系统被作为一台交换机进行管理，配置命令直接在堆叠内的所有交换机上生效；用户可以通过登录堆叠内的任意一台交换机，对堆叠内的所有交换机进行统一配置和管理。
 * 高可靠性。堆叠内的交换机互为备份，同时，利用跨设备的Eth-Trunk实现跨设备的链路冗余备份。
 * 强大的网络扩展能力。通过组建堆叠，在不改变网络拓扑的情况下，扩展端口数量、带宽和处理能力。

常见概念
---------------------------------------
**角色**

  ISS堆叠中的单台设备称为成员设备。成员设备按照功能不同，分为两种角色：
  
  * Master：负责整个堆叠的运行、维护和管理，由角色选举产生。一个堆叠系统中只能有一台Master设备。
  * Slave：作为Master设备的备份设备运行。当Master重启时，Slave会被选举为Master。

**Member ID**

  成员设备ID，用来标识和管理成员设备。堆叠系统中成员ID是唯一的。

**ISS链路**

  成员设备之间用于互连形成ISS的链路。

**堆叠接口**
  
  被配置为堆叠模式的物理接口，用于堆叠成员交换机之间的连接。

  成员设备间可以配置多个堆叠接口，进行负载分担，但是控制报文只能从控制接口转发。

**优先级**

  参与堆叠角色选举，用来确定成员交换机的角色。

  优先级值越大表示优先级越高，当选为Master的可能性越大。

**ISS MAC**

  堆叠MAC地址，即堆叠系统的对外体现的MAC地址。

  堆叠系统刚刚建立时，ISS MAC和Master设备的MAC地址一致。当Master设备重启，Slave被选举为Master时，ISS MAC不会重新选举，保持不变。

**堆叠报文**
  
  ISS用到的主要报文有：

  * Hello报文：点对点报文，在相邻设备间交互，携带本设备所收集到的所有的设备信息、优先级信息和其它上下文信息。
  * Elect选举报文：点对点报文，设备仅仅携带用于选举的相关信息，如设备MAC地址，优先级，设备运行时间等。
  * ElectAck：Elect选举回应报文。
  * Anno通告报文：竞选结果通告报文，Master发送宣布竞选结果，Slave回复ACK进行确认。
  * AnnoAck：Anno通告回应报文。
  * Urgent报文：广播报文，用于ISS系统紧急事件的通告，如堆叠口DOWN。

ConnetOS支持的堆叠特性
---------------------------------------
在为了防止堆叠建立后，大量的报文跨越中间有限带宽的堆叠链路进行转发导致链路满载现象出现，ISS采取报文转发本地优先机制。对于等价路由或聚合端口，如果本地有出口时，报文直接由本地转发，不会经过堆叠链路，只有当本地出口down时，才经堆叠链路由另一台设备进行转发。

在ISS堆叠开始运行后：

 * 在maste设备上的配置，在堆叠系统内的所有交换机上同时生效。
 * 远程登录界面都能进行配置，但是对管理网络接入有要求：单线接入时必须接入到Master。
 * 串口界面只有Master能做配置，Slave只能做查询。
 * 切换ISS模式后，以下特性暂时不能使用：LLDP、SNMP、ATP。