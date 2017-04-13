环回接口命令
=====================================

set loopback-interface interface address
-------------------------------------------

命令功能
+++++++++++++++
**set loopback-interface interface address** 命令用来配置Loopback接口的IP地址。

**delete loopback-interface interface address** 命令用来删除配置的Loopback接口的IP地址。

缺省情况下，没有配置Loopback的IP地址。

命令格式
+++++++++++++++
**set loopback-interface interface** *lo-interface-name* **address** *ip-address* [ **member** *member-id* ]

**delete loopback-interface interface** *lo-interface-name* **address** [ member** ]

参数说明
+++++++++++++++
*lo-interface-name*：Loopback接口名称，取值形式为lo100。

*ip-address*：Loopback接口的IP地址，取值形式为：目的IP地址/掩码长度，点分十进制格式。

*member-id*：堆叠系统的成员设备编号，本参数只在stack模式下显示：表示此Loopback接口所属的成员设备。所有发送到此Loopback接口的报文都将发送到所属设备上。整数形式，取值为1、2。

 * 1：表示设备为master设备。
 * 2：表示设备为slave设备。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置Loopback接口lo100的IP地址::

 ConnetOS# set loopback-interface interface lo100 address 1.1.1.1/24

set loopback-interface interface description
------------------------------------------------

命令功能
+++++++++++++++
**set loopback-interface interface description** 命令用来配置对Loopback接口的描述。

**delete loopback-interface interface description** 命令用来删除配置的Loopback接口描述。

缺省情况下，没有配置对Loopback接口的描述。

命令格式
+++++++++++++++
**set loopback-interface interface** *lo-interface-name* **description** *description*

**delete loopback-interface interface** *lo-interface-name* **description**

参数说明
+++++++++++++++
*lo-interface-name*：Loopback接口名称，取值形式为lo100。

*description*：Loopback接口的接口描述。字符串形式，不支持空格。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置Loopback接口lo100的接口描述::

 ConnetOS# set loopback-interface interface lo100 description test

show loopback-interface
------------------------------------------------

命令功能
+++++++++++++++
**show loopback-interface** 命令用来查看Loopback接口信息。

命令格式
+++++++++++++++
**show loopback-interface** [ *lo-interface-name* ]

参数说明
+++++++++++++++
*lo-interface-name*：当前已经配置好的Loopback接口名称。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查看Loopback接口信息::

 ConnetOS> show loopback-interface
 lo100: Index:101  Flags:<ENABLED,LOOPBACK>
         member 1 inet 1.1.1.1 subnet 1.1.1.0/24 broadcast 1.1.1.255
