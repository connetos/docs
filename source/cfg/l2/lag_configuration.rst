链路聚合配置
=======================================

链路聚合简介
---------------------------------------
链路聚合通过将多条以太网物理链路捆绑在一起成为一条逻辑链路，从而实现增加链路带宽的目的。同时，通过相互间的动态备份，有效地提高链路的可靠性。

ConnetOS支持通过手动、动态LACP配置汇聚接口。同一个汇聚组中端口的基本配置应该保持一致，即如果某端口为trunk端口，则其他端口也配置为trunk端口；如该端口的链路类型改为access端口，则其他端口的链路类型也改为access端口。

链路聚合技术主要有以下三个优势：

 * 增加带宽

   链路聚合接口的最大带宽可以达到各成员接口带宽之和。

 * 提高可靠性

   当某条活动链路出现故障时，流量可以切换到其他可用的成员链路上，从而提高链路聚合接口的可靠性。

 * 负载分担

在一个链路聚合组内，可以实现在各成员活动链路上的负载分担。

常见概念
---------------------------------------

LAG
+++++++++++++++++++++++++++++++++++++++
LAG（Link Aggregation Group）链路汇聚组，是指将若干条以太链路捆绑在一起所形成的逻辑链路。

每个LAG唯一对应着一个逻辑接口，这个逻辑接口称之为汇聚接口。

组成汇聚接口接口的各个物理接口称为成员接口。成员接口对应的链路称为成员链路。

汇聚接口可以作为普通的以太网接口来使用，实现各种路由协议以及其它业务。与普通以太网接口的差别在于：转发的时候链路聚合组需要从成员接口中选择一个或多个接口来进行数据转发。

成员接口
+++++++++++++++++++++++++++++++++++++++
汇聚组接口的成员接口存在：

 * 活动接口：转发数据的接口

   对应的链路称为活动链路。

 * 非活动接口两种：不转发数据的接口。

   对应的链路称为非活动链路。

活动接口数上限阈值
+++++++++++++++++++++++++++++++++++++++
设置活动接口数上限阈值的目的是在保证带宽的情况下提高网络的可靠性。当前活动链路数目达到上限阈值时，再向汇聚组接口中添加成员接口，不会增加活动接口的数目，超过上限阈值的链路状态将被置为Down，作为备份链路。

活动接口数下限阈值
+++++++++++++++++++++++++++++++++++++++
设置活动接口数下限阈值是为了保证最小带宽，当前活动链路数目小于下限阈值时，Eth-Trunk接口的状态转为Down。

LACP
+++++++++++++++++++++++++++++++++++++++
LACP（Link Aggregation Control Protocol，链路聚合控制协议）基于IEEE 802.3ad标准，是一种实现链路动态聚合与解聚合的协议。

接口使能LACP协议后，接口通过LACPDU（Link Aggregation Control Protocol Data Unit，链路聚合控制协议数据单元）与对端交互信息，通告自己的系统优先级、系统mac、端口优先级、端口号和操作key。对端接收到这些信息后，将这些信息与端口所保存的信息比较，选择能够聚合的端口，双方可以对端口加入或退出某个动态聚合组达成一致。

负载分担
+++++++++++++++++++++++++++++++++++++++
操作Key是在链路聚合时用来表明成员端口汇聚能力的一个数值，它是根据成员端口上的一些信息（包括该端口的速率、双工模式等）的组合自动计算生成的，这个信息组合中任何一项的变化都会引起操作Key的重新计算。在同一汇聚组中，所有的选中端口都必须具有相同的操作Key。

其中，动态聚合端口在使能lacp协议后，其管理key缺省为零。静态聚合端口在使能lacp后，端口的管理key与聚合组id相同。对于动态聚合组而言，同组成员一定有相同的操作key，而手工和静态聚合组中，selected的端口有相同的操作key。

手动配置汇聚接口
---------------------------------------

#. 进入配置模式。

   ConnetOS> **configure**

#. 创建汇聚接口

   ConnetOS# **set interface aggregate-ethernet** *ae-number*

   ConnetOS支持最多配置32个汇聚接口。

#. （可选）使能汇聚接口

   ConnetOS# **set interface aggregate-ethernet** *ae-number* **enable true**

   缺省情况下，汇聚接口组创建后就使能

#. （可选）配置汇聚接口的描述

   ConnetOS# **set interface aggregate-ethernet** *ae-number* **description** *description*

#. 将物理接口加入汇聚接口

   ConnetOS# **set interface gigabit-ethernet** *interface-name* **ether-options 802.3ad** *ae-number*

   实际使用时，建议每个汇聚组的成员接口数不要超过8个。

#. 提交配置

   ConnetOS# **commit**

配置汇聚组负载均衡
---------------------------------------

#. 进入配置模式。

   ConnetOS> **configure**

#. 配置LAG哈希算法

   ConnetOS# **set forwarding-options load-balance lag algorithm** *algorithm-num* 

   缺省情况下，ConnetOS采用的hash算法是0。

#. 配置哈希因子

   ConnetOS# **set forwarding-options load-balance lag key** { **dest-ip** | **dest-mac** | **ether-type** | **ingress-interface** | **ip-protocol** | **l4-dest-port** | **l4-source-port** | **source-ip** | **source-mac** | **vlan-id** } **enable** { **false** | **true** }

#. 提交配置。

ConnetOS# **commit**

配置LACP汇聚接口
---------------------------------------

#. 进入配置模式。
 
   ConnetOS> **configure**

#. 使能接口的LACP协议。

   ConnetOS# **set interface aggregate-ethernet** *interface-name* **ether-options lacp enable** { **false** | **true** }

#. 设置最小选中接口。

   ConnetOS# set interface aggregate-ethernet interface-name ether-options min-selected-port port-number
   
   缺省情况下，最小选中接口数是1。
   
   当汇聚组中的活动接口数少于设置的最小数值时，ConnetOS会自动Down掉整个汇聚组。

＃. 配置汇聚接口组MTU
    
    ConnetOS# set interface aggregate-ethernet ae-number mtu mtu-value

#. 配置汇聚接口组的风暴控制

   ConnetOS# **set interface aggregate-ethernet** *interface-name* **storm-control** { **broadcast | multicast | unicast } kilobits suppress

#. 提交配置

   ConnetOS# **commit**

可以通过：
 * 执行命令 **show lacp neighbor**，查看LACP邻居，
 * 执行命令 **show lacp internal**，查看汇聚接口组的LACP状态，
 * 执行命令 **show lacp statistics**，查看LACP协议包的状态

