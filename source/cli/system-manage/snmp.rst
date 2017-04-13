SNMP命令参考
=============================

set system snmp-acl
-------------------------------------------

命令功能
++++++++++++++++++++++++++++++
**set system snmp-acl network** 命令用来配置允许通过SNMP协议管理设备的用户网段。

**delete system snmp-acl network** 命令用来删除配置的SNMP管理用户网段，恢复为缺省值。

缺省情况下，允许所有网段的用户通过SNMP管理设备。

命令格式
++++++++++++++++++++++++++++++
**set system snmp-acl network** *network-address*

**delete system snmp-acl** [ **network** *network-address* ] 

参数说明
++++++++++++++++++++++++++++++
*network-address*：允许通过SNMP管理设备的用户网段。取值形式是网段地址／掩码。

命令模式
++++++++++++++++++++++++++++++
配置模式

使用指南
++++++++++++++++++++++++++++++
无。

配置举例
++++++++++++++++++++++++++++++
# 设置网段地址是1.1.1.0/24的用户可以通过SNMP协议管理设备::

 ConnetOS# set system snmp-acl network 1.1.1.0/24

show snmp statistics
-------------------------------------------

命令功能
+++++++++++++++
**show snmp statistics** 命令用来查看

命令格式
+++++++++++++++
**show snmp statistics**

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
# 查看SNMP协议的统计信息::

 ConnetOS> show snmp statistics
 SNMP statistics:
 Input:
 Packets: 2431, Bad versions: 0, Bad community names: 0,
 Bad community uses: 0, ASN parse errors: 0,
 Too bigs: 0, No such names: 0, Bad values: 0,
 Read onlys: 0, General errors: 0,
 Total request varbinds: 79849, Total set varbinds: 0,
 Get requests: 187, Get nexts: 2244, Set requests: 0,
 Get responses: 0, Traps: 0,
 Silent drops: 0, Proxy drops 0
 Output:
 Packets: 2431, Too bigs: 0, No such names: 0,
 Bad values: 0, General errors: 0,
 Get requests: 0, Get nexts: 0, Set requests: 0,
 Get responses: 2431, Traps: 0
