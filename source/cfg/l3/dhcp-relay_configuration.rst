DHCP Relay配置
=======================================

简介
---------------------------------------
DHCP（Dynamic Host Configuration Protocol）动态主机配置协议，用于对用户IP地址进行动态分配和管理。

DHCP采用客户端/服务器模式，DHCP客户端向DHCP服务器动态地请求网络配置信息，DHCP服务器根据策略返回相应的配置信息（IP地址、子网掩码、缺省网关等网络参数）。

DHCP Relay，负责转发来自客户端方向或服务器方向的DHCP报文，协助DHCP客户端和DHCP服务器完成地址配置功能。它实现了不同网段间的DHCP服务器和客户端之间的报文交互，避免在每个网段范围内都部署DHCP服务器，既节省成本，又便于进行集中管理。

配置DHCP Relay功能
---------------------------------------
#. 进入配置模式。
  
   ConnetOS> **configure**

#. 创建VLAN。

   ConnetOS# **set vlans vlan-id** *vlan-id*

#. 创建VLAN对应的接口vlan-interface。

   ConnetOS# **set vlans vlan-id** *vlan-id* **l3-interface** *l3-interface-name*

#. 指定DHCP Relay服务器。

   ConnetOS# **set vlan-interface interface** *l3-interface-name* **dhcp-relay** **server-ip** *ip-address*

#. 提交配置。

   ConnetOS# **commit**

查看DHCP Relay的配置信息
---------------------------------------
执行 **show vlan-interface interface** 命令，查看DHCP Relay的配置情况::

 ConnetOS# show vlan-interface interface vlan100
 Waiting for building configuration.
     description: ""
     mtu: 1500
     dhcp-relay {
         server-ip 1.1.1.1
     }
