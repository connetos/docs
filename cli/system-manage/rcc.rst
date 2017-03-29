RCC命令
========================

set system rcc allow-client
-------------------------------------------

命令功能
+++++++++++++++
**set system rcc enable allow-client** 命令用来配置允许进行RCC远程配置的用户网段。

**delete system rcc enable allow-client** 命令用来删除配置的RCC远程配置的用户网段。

缺省情况下，所有网段的用户都可以进行RCC远程配置。

命令格式
+++++++++++++++
**set system rcc allow-client** *network-address*

**delete system rcc allow-client network-address**

参数说明
+++++++++++++++
*network-address*：允许进行RCC远程配置的网段。取值形式是IP地址／掩码的形式。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置允许网段1.1.1.0/24内的用户都可以通过RCC远程执行交换机上的命令行::

 ConnetOS# set system rcc allow-client 1.1.1.0/24 

set system rcc enable
-------------------------------------------

命令功能
+++++++++++++++
**set system rcc enable** 命令用来配置是否使能RCC功能。

**delete system rcc enable** 命令用来删除配置的RCC功能，恢复为缺省值。

缺省情况下，RCC功能没有使能。

命令格式
+++++++++++++++
**set system rcc enable** { **false** | **true** }

**delete system rcc enable**

参数说明
+++++++++++++++
**false**：去使能RCC功能。

**true**：使能RCC功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
使能RCC功能后，用户可以远程执行交换机上的任何命令。

配置举例
+++++++++++++++
# 使能RCC功能::

 ConnetOS# set system rcc enable true 