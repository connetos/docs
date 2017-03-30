Navmesh
=======================================

Navmesh概述
---------------------------------------
在网络出现故障时，ConnetOS提供了命令行诊断方式：Navmesh。Navmesh命令用于查看指定流量的路径。

通过报文流量的五元组，Navmesh可以查询到流量唯一的出端口和入端口信息。并且，即使此流量已经停止发送，只要表项还在，仍然可以查询到出入端口信息。

但是如果流量是通过ECMP的方式发送到设备，那么通过Navmesh查询到的可能是入端口和出端口列表。此时，Navmesh将发起二次查询，二次查询会精确的找到唯一的一对出端口和入端口。

.. note::
 二次查询可以查到的前提是流量一直在发送。

查询流量的出入端口
---------------------------------------
Navmesh通过五元组来查询流量的出端口和入端口::

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
