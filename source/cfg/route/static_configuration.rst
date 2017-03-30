静态路由配置
=====================================

IP路由简介
--------------------------------
路由就是报文在转发过程中的路径信息，用来指导报文转发。

根据路由目的地的不同，路由划分为：

 * 网段路由：目的地址为网段，子网掩码长度小于32位。
 * 主机路由：目的地为主机，子网掩码长度为32位。

据来源的不同，路由可以分为三类：

 * 直连路由：通过链路层协议发现的路由。
 * 静态路由：通过网络管理员手动配置的路由。
 * 动态路由：通过动态路由协议发现的路由。

ConnetOS支持配置静态路由和OSPF动态路由协议。

静态路由配置
--------------------------------
静态路由适用于结构简单并且稳定的小型网络，能改进网络性能，并保证重要应用的带宽。但是当网络发生故障或者拓扑发生变化后，静态路由不会自动改变，必须手动修改。

配置静态路由必须配置：目的地址和掩码、下一跳。

配置静态路由
--------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 配置静态路由。
   
   ConnetOS# **set protocols static route** *ip-address* **next-hop** *ip-address*

#. （可选）设置路由metric。
   
   ConnetOS# **set protocols static route** *ip-address* **metric** *metric-value*

#. 提交配置。

   ConnetOS# **commit**

检查配置结果
--------------------------------
* 配置完成后，查看软件路由表::

   ConnetOS> show route table ipv4 unicast final
 
   1.0.0.0/24         [connected(0)/0]
                    > via vlan100/vlan100
   2.0.0.0/24         [connected(0)/0]
                    > via vlan200/vlan200
   10.0.0.0/24        [static(1)/1]
                    > to 20.0.0.2 via vlan200/vlan200
   20.0.0.0/24        [static(1)/1]
                    > to 2.0.0.2 via vlan200/vlan200

* 查看硬件路由表::
 
   ConnetOS> show route forward-route ipv4 all
   Destination       NetMask          	NextHopMac          Port
   ---------------   		---------------   		-----------------   		---------
   1.0.0.0           	255.255.255.0     	CC:37:AB:F4:82:F3   	connected
   2.0.0.0           255.255.255.0     	CC:37:AB:F4:82:F3   	connected
   20.0.0.0          255.255.255.0     	00:10:94:00:00:04     	te-1/1/4
   Total route count:3





