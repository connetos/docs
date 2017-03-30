接口简介
=======================================
接口是设备与网络中的其它设备交换数据并相互作用的部件，分为管理接口、物理业务接口和逻辑接口三类，其中：

 * 管理接口
  
   管理接口主要为用户提供配置管理支持，也就是用户通过此类接口可以登录到设备，并进行配置和管理操作。管理接口不承担业务传输。

 * 物理接口

   物理接口是真实存在、有器件支持的接口，承担业务传输。

 * 逻辑接口

   逻辑接口是指能够实现数据交换功能但物理上不存在、需要通过配置建立的接口。逻辑接口需要承担业务传输。

配置以太接口
=======================================
缺省情况下，接口的基本参数都有缺省值，请根据具体网络情况进行选择。

#. 进入配置模式。

   ConnetOS> **configure**

#. （可选）配置接口功能是否使能。

   ConnetOS# **set interface gigabit-ethernet** *interface-name* **enable** { **false** | **true** }

   缺省情况下，接口功能是使能的。

#. 可选）配置接口描述。

   ConnetOS# **set interface gigabit-ethernet** *interface-name* **description** *description*

   缺省情况下，接口下没有接口描述。

#. 配置接口模式

   ConnetOS# **set interface gigabit-ethernet** *interface-name* **family ethernet-switching port-mode** { **access** | **trunk** }

   * Trunk类型的接口主要用来连接其它交换机设备，一般用于干道链路。Trunk接口允许多个VLAN的帧通过。
   * Access类型的接口主要用来连接用户主机，一般用于接入链路，且接入链路上通过的帧为不带Tag的以太网帧。如果Access接口配置了缺省VLAN，则在该报文上加上Tag标记，并将Tag中的VID字段的值设置为接口所属的缺省VLAN编号，此时接入链路上允许与缺省VLAN Tag匹配的以太网帧通过。

#. 配置接口MTU

   ConnetOS# **set interface gigabit-ethernet** *interface-name* **mtu** *mtu-value*

#. 配置接口限速

   ConnetOS# **set interface** *interface-name* **rate-limiting egress kilobits** *rate-limit*

#. 配置接口速率

   ConnetOS# **set interface gigabit-ethernet** *interface-name* **speed** *speed-vlaue*

#. 配置端口风暴控制

   ConnetOS# **set interface gigabit-ethernet** *interface-name* **storm-control** { **broadcast** | **multicast** | **unicast** } **kilobits** *suppress*

   ConnetOS支持物理接口单播，组播和广播的风暴抑制，单位是bps，范围1～40000000。

#. 提交配置

   ConnetOS# **commit**

配置loopback接口
=======================================

#. 进入配置模式。

   ConnetOS> **configure**

#. 配置Loopback接口的IP地址和掩码

   ConnetOS# **set loopback-interface interface** *lo-interface-name* **address** *ip-address*

   ConnetOS支持配置多个loopback接口。

#. 配置Loopback接口的接口描述

   ConnetOS# **set loopback-interface interface** *lo-interface-name* **description** *description*

#. 提交配置

   ConnetOS# **commit**

配置汇聚接口
=======================================

接口汇聚是将多个接口聚合在一起形成1个汇聚组，以实现流量在成员接口中的分担，同时提供更高的连接可靠性。

ConnetOS支持通过手动、静态LACP、动态LACP配置汇聚接口。同一个汇聚组中端口的基本配置应该保持一致，即：

 * 如果某端口为trunk端口，则其他端口也配置为trunk端口；
 * 如该端口的链路类型改为access端口，则其他端口的链路类型也改为access端口。

汇聚接口的配置，请参见"以太网交换配置－链路聚合配置"。

配置VLAN接口
=======================================
#. 进入配置模式。

   ConnetOS> **configure**

#. 创建VLAN
   
   ConnetOS# **set vlans vlan-id** *vlan-id*

#. 创建VLAN对应的接口vlan-interface

   ConnetOS# **set vlans vlan-id** *vlan-id* **l3-interface** *l3-interface-name*

#. 配置vlan-interface的地址及掩码

   ConnetOS# **set vlan-interface interface** *l3-interface-name* **address** *ip-address* **prefix-length** *prefix-length*

   ConnetOS支持一个VLAN配置多个IP地址。

#. 为vlan-interface指定DHCP Relay服务器。

   ConnetOS# **set vlan-interface interface** *l3-interface-name* **dhcp-relay server-ip** *ip-address*

#. 配置vlan-interface的MTU

   ConnetOS# **set vlan-interface interface** *l3-interface-name* **mtu** *mtu-vlaue*

#. （可选）配置vlan-interface的接口描述

   ConnetOS# **set vlan-interface interface** *l3-interface-name* **description** *description*

#. 提交配置

   ConnetOS# **commit**

