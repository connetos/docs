navmesh流量查询
=======================================

show navmesh
---------------------------------------

命令功能
+++++++++++++++++++++++++++++++++++++++
**show navmesh** 命令用来查看指定五元组流量的出入端口信息。

命令格式
+++++++++++++++++++++++++++++++++++++++
**show navmesh source-ipv4** *source-ipv4-address* **dest-ipv4** *dest-ipv4-address* **l4-source-port** *source-port-number* **l4-dest-port** *dest-port-number* **protocol** *protocol-number*

参数说明
+++++++++++++++++++++++++++++++++++++++
*source-ipv4-address*：源IP地址。

*dest-ipv4-address*：目的IP地址。

*source-port-number*：源端口号。整数形式，取值范围是1～65535。

*dest-port-number*：目的端口号。整数形式，取值范围是1～65535。

*protocol-number*：IP协议号。

命令模式
+++++++++++++++++++++++++++++++++++++++
运维模式

使用指南
+++++++++++++++++++++++++++++++++++++++
无。

配置举例
+++++++++++++++++++++++++++++++++++++++
# 查看源地址为10.10.10.10，目的地址40.40.40.10，源端口号为55，目的端口为11，协议号为17的流量的出入端口::

 ConnetOS> show navmesh source-ipv4 10.10.10.10 dest-ipv4 40.40.40.10 l4-source-port 55 
 l4-dest-port 11 protocol 17 
 The Flow Information :
   Source ipv4 address          : 10.10.10.10
   Destination ipv4 address	: 40.40.40.10
   L4 source port               : 55
   L4 destination port          : 11
   IP protocol                  : 17
 The forwarding path :
    Ingress Port   Egress Port
    ------------   ------------
    te-1/1/5       te-2/1/17
    te-1/1/5       te-2/1/17
