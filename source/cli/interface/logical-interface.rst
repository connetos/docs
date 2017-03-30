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
**set loopback-interface interface** *lo-interface-name* **address** *ip-address*

**delete loopback-interface interface** *lo-interface-name* **address**

参数说明
+++++++++++++++
*lo-interface-name*：Loopback接口名称，取值形式为lo100。

*ip-address*：Loopback接口的IP地址，取值形式为：目的IP地址/掩码长度，点分十进制格式。

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

