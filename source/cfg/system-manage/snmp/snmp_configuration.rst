NMS管理设备
=======================================
ConnetOS支持用户通过NMS（Network Management Station，网管工作站）登录到交换机，对交换机进行配置、管理。

如果要使用NMS登录设备，需要先在设备上配置好SNMP功能。配置完成后，即可通过登录。

SNMP概述
---------------------------------------
SNMP（Simple Network Management Protocol）简单网络管理协议，是网络中管理设备和被管理设备之间的通信规则，它定义了一系列消息、方法和语法，用于实现管理设备对被管理设备的访问和管理。

SNMP具有以下优势：

 * 自动化网络管理。
   网络管理员可以利用SNMP平台在网络上的节点检索信息、修改信息、发现故障、完成故障诊断、进行容量规划和生成报告。
 * 屏蔽不同设备的物理差异，实现对不同厂商产品的自动化管理。
   SNMP只提供最基本的功能集，使得管理任务分别与被管设备的物理特性和下层的联网技术相对独立，从而实现对不同厂商设备的管理，特别适合在小型、快速和低成本的环境中使用。

配置SNMP
---------------------------------------
#. 进入配置模式。
   
   ConnetOS> **configure**

#. 启动SNMP功能。
 
   ConnetOS# **set protocols snmp community** *community-info* [ **authorization read-only** | **clients** *ip-address* ]

   缺省情况下，SNMP功能是关闭的。

#. 配置SNMP访问控制
 
   ConnetOS# **set system snmp-acl network** *ip-address*

   缺省情况下，允许所有网段查询。

#. 提交配置

   ConnetOS# **commit**