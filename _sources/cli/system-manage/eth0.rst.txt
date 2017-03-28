管理口命令参考
=============================

set interface management-ethernet eth0 address
--------------------------------------------------------

命令功能
+++++++++++++++
**set interface management-ethernet eth0 address** 命令用来配置管理口的IP地址。

**delete interface management-ethernet eth0 address** 命令用来删除配置的管理口IP地址，恢复为缺省值。

缺省情况下，管理口的IP地址为0.0.0.0/0。

命令格式
+++++++++++++++
**set interface management-ethernet eth0** [ **member** *member-id* ] **address** *ip-address*

**delete interface management-ethernet eth0** [ **member** *member-id* ] **address**

参数说明
+++++++++++++++
*member-id*：堆叠系统的成员设备编号，本参数只在stack模式下显示。整数形式，取值为1、2。
 
 * 1：表示设备为master设备；
 * 2：表示设备为slave设备。

*ip-address*：管理口IP地址。点分十进制格式，取值形式为：目的IP地址/掩码长度。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 设置设备的管理口IP地址为1.1.1.1/24::

 ConnetOS# set interface management-ethernet eth0 member 1 address 1.1.1.1/24

set interface management-ethernet eth0 dhcp
--------------------------------------------------

命令功能
+++++++++++++++
**set interface management-ethernet eth0 dhcp enable** 命令用来配置是否使能管理口的DHCP功能。

**delete interface management-ethernet eth0 dhcp enable** 命令用来删除配置的管理口DHCP功能，恢复为缺省值。

缺省情况下，管理口的DHCP功能已经使能。

命令格式
+++++++++++++++
**set interface management-ethernet eth0** [ **member** *member-id* ] **dhcp enable** { **false** | **true** }

**delete interface management-ethernet eth0** [ **member** *member-id* ] **dhcp enable**


参数说明
+++++++++++++++
*member-id*：堆叠系统的成员设备编号，本参数只在stack模式下显示。整数形式，取值为1、2。
 
 * 1：表示设备为master设备；
 * 2：表示设备为slave设备。

**false**：不使能管理口的DHCP功能。

**true**：使能管理口的DHCP功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能管理口的DHCP功能::

 ConnetOS# set interface management-ethernet eth0 dhcp enable true

set interface management-ethernet eth0 gateway
---------------------------------------------------

命令功能
+++++++++++++++
**set interface management-ethernet eth0 gateway** 命令用来配置管理口的网关地址。

**delete interface management-ethernet eth0 gateway** 命令用来删除配置的管理口网关地址，恢复为缺省值。

省情况下，管理口的网关地址为0.0.0.0。

命令格式
+++++++++++++++
**set interface management-ethernet eth0** [ **member** *member-id* ] **gateway** *ip-address*

**delete interface management-ethernet eth0** [ **member** *member-id* ] **gateway**

参数说明
+++++++++++++++
*member-id*：堆叠系统的成员设备编号，本参数只在stack模式下显示。整数形式，取值为1、2。
 
 * 1：表示设备为master设备；
 * 2：表示设备为slave设备。

*ip-address*：管理口网关的IP地址。点分十进制格式。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 设置设备的管理口网关的IP地址为1.1.1.1::

 ConnetOS# set interface management-ethernet eth0 member 1 gateway 1.1.1.1

show interface management-ethernet eth0
------------------------------------------------

命令功能
+++++++++++++++
**show interface management-ethernet eth0** 命令用来查看管理网口的信息。

命令格式
+++++++++++++++
**show interface management-ethernet eth0**

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
# 查看管理网口的信息::

 ConnetOS 1> show interface management-ethernet eth0
 Member ID  Interface   Address             Gateway          MAC
 ---------  ----------  ------------------  ---------------  -----------------
 1          eth0        192.168.1.34/24     0.0.0.0          cc:37:ab:f4:82:f2
 2          eth0        192.168.1.35/24     0.0.0.0          00:03:0f:64:da:9f
