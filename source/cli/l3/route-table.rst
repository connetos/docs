路由表查看命令参考
========================

show route admin distance ipv4 unicast
-------------------------------------------

命令功能
+++++++++++++++
**show route admin distance ipv4 unicast** 命令用来查看不同种类路由的优先级。

命令格式
+++++++++++++++
**show route admin distance ipv4 unicast**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查看不同种类路由的优先级::

 ConnetOS> show route admin distance ipv4 unicast
 Protocol                 Administrative distance
 connected                0
 static                   1
 eigrp-summary            5
 ebgp                     20
 eigrp-internal           90
 igrp                     100
 ospf                     110
 is-is                    115
 rip                      120
 eigrp-external           170
 ibgp                     200
 fib2mrib                 254
 unknown                  255

show route forward-host
-------------------------------------------

命令功能
+++++++++++++++
**show route forward-host** 命令用来查看硬件路由表中本机的路由信息。

命令格式
+++++++++++++++
**show route forward-host** { **brief** | **ipv4** { *ip-address* | **all** } }

参数说明
+++++++++++++++
**brief**：查看表中的概要信息，即路由条目数。

*ip-address*：本机IP地址。

**all**：查看所有的路由信息。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查看硬件路由表中本机的所有路由信息::

 ConnetOS> show route forward-host ipv4 all
 Address           HWaddress           Port
 ---------------   -----------------   ---------
 9.9.9.9           00:00:00:11:22:99   te-2/1/9
 Total host count:1

show route forward-route
-------------------------------------------

命令功能
+++++++++++++++
**show route forward-route** 命令用来查看FIB转发表中的路由条目。

命令格式
+++++++++++++++
**show route forward-route** { **brief** | **ipv4** { *network-address* | **all** } }

参数说明
+++++++++++++++
**brief**：查看转发表中的概要信息，即路由条目数。

*network-address*：目的网络地址。取值形式是网段地址／掩码。

**all**：查看转发表中所有的IPv4路由信息。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查看转发表中所有的IPv4路由信息::

 ConnetOS> show route forward-route ipv4 all
 Destination       NetMask           NextHopMac          Port
 ---------------   ---------------   -----------------   ---------
 9.9.9.0           255.255.255.0     00:03:0F:64:DA:53   connected
 11.11.11.0        255.255.255.0     00:03:0F:64:DA:53   connected
 33.33.33.0        255.255.255.0     00:03:0F:64:DA:53   connected
 Total route count:3

show route table ipv4 unicast
-------------------------------------------

命令功能
+++++++++++++++
**show route table ipv4 unicast** 命令用来查看RIB路由表中的路由条目。

命令格式
+++++++++++++++
**show route table ipv4 unicast** { **connected** | **final** | **ospf** [ **winners** ]| **static** } [ **brief** | **detail** ]

参数说明
+++++++++++++++
**connected**：查看直连网络的路由条目。

**final**：查看最终选择进行转发的路由条目。

**ospf**：查看通过OSPF协议学到的路由条目。

**winners**：查看通过OSPF协议学到的路由条目

**static**：查看静态路由条目。

**brief**：查看路由表的概要信息。

**detail**：查看路由表的详细信息。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查看路由表中最终选择进行转发的路由条目的详细信息::

 ConnetOS> show route table ipv4 unicast final detail
 Network 9.9.9.0/24
     Nexthop        := 9.9.9.1
     Interface      := vlan9
     Vif            := vlan9
     Metric         := 0
     Protocol       := connected
     Admin distance := 0
 Network 11.11.11.0/24
     Nexthop        := 11.11.11.1
     Interface      := vlan100
     Vif            := vlan100
     Metric         := 0
     Protocol       := connected
     Admin distance := 0
 Network 33.33.33.0/24
     Nexthop        := 33.33.33.10
     Interface      := vlan30
     Vif            := vlan30
     Metric         := 0
     Protocol       := connected
     Admin distance := 0
 Network 55.55.55.0/24
     Nexthop        := 33.33.33.20
     Interface      := vlan30
     Vif            := vlan30
     Metric         := 30
     Protocol       := ospf
     Admin distance := 110



