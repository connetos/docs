MAC地址命令
=======================================

set interface gigabit-ethernet static-mac-address
-----------------------------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet static-mac-address** 命令用来配置指定接口的静态MAC地址。

**delete interface gigabit-ethernet static-mac-address** 命令用来删除配置的指定接口静态MAC地址。

缺省情况下，没有配置静态MAC地址。

命令格式
+++++++++++++++

**set interface gigabit-ethernet** *interface-name* **static-mac-address** *mac-address* [ **vlan** *vlan-id* ]

**delete interface gigabit-ethernet** *interface-name* **static-mac-address** *mac-address* [ **vlan** *vlan-id* ]

参数说明
+++++++++++++++
*interface-name*：接口名称。

*mac-address*：静态MAC地址。取值形式为00:11:22:33:44:55。

*vlan-id*：VLAN ID，整数形式，取值范围是1～4094。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置vlan100下的te-1/1/1口静态MAC地址为00:22:22:22:22:22::

 ConnetOS# set interface gigabit-ethernet te-1/1/10 static-mac-address 00:22:22:22:22:22 vlan 100

set forwarding-options mac-aging-time
-------------------------------------------

命令功能
+++++++++++++++
**set forwarding-options mac-aging-time** 命令用来配置MAC地址的老化时间。

**delete forwarding-options mac-aging-time** 命令用来删除配置的MAC地址老化时间，恢复为缺省值。

缺省情况下，MAC地址的老化时间为300s。

命令格式
+++++++++++++++
**set forwarding-options mac-aging-time** *aging-time*

**delete forwarding-options mac-aging-time**

参数说明
+++++++++++++++
*aging-time*：MAC地址的老化时间。整数形式，取值范围是60～1000000，单位是秒。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 设置MAC地址的老化时间为100s::

 ConnetOS# set forwarding-options mac-aging-time 100

clear ethernet-switching table
-------------------------------------------

命令功能
+++++++++++++++
**clear ethernet-switching table** 命令用来清除MAC地址表。

命令格式
+++++++++++++++
**clear ethernet-switching table** { **all** | *interface-name* | **tunnel-ethernet** *tunnel-name* }

参数说明
+++++++++++++++
**all**：清除全部MAC地址表。

*interface-name*：接口名称。

*tunnel-name*：隧道名称。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 清空全部MAC表::

 ConnetOS> clear ethernet-switching table all
