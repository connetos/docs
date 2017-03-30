日志命令
=======================

set system syslog host server-ip
-------------------------------------------

命令功能
+++++++++++++++
**set system syslog host server-ip** 命令用来指定远端日志服务器。

**delete system syslog host server-ip** 命令用来删除指定的日志服务器。

缺省情况下，没有指定远端日志服务器。

命令格式
+++++++++++++++
**set system syslog host server-ip** *ip-address*

**delete system syslog host** [ **server-ip** *ip-address* ]

参数说明
+++++++++++++++
*ip-address*：远端日志服务器的地址。ConnetOS可以指定多个日志服务器。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
如果不指定具体的IP地址，将删除所有的指定远端日志服务器。

配置举例
+++++++++++++++
# ConnetOS将日志发送到地址2.2.2.2的日志服务器::

 ConnetOS# set system syslog host server-ip 2.2.2.2

set system syslog log-facility
-------------------------------------------

命令功能
+++++++++++++++
**set system syslog log-facility** 命令用来日志的facility级别。

**delete system syslog log-facility** 命令用来删除用户配置的facility级别，恢复缺省值。

缺省情况下，日志的facility级别是0。

命令格式
+++++++++++++++
**set system syslog log-facility** *facility-number*

**delete system syslog log-facility**

参数说明
+++++++++++++++
*facility-number*：facility的编号。整数形式，取值范围是0～7。缺省值是0。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
日志服务器根据facility的值对日志进行存储，facility值相同的日志会被存储在同一个.log文件中。

配置举例
+++++++++++++++
# 设置日志的facility的级别是3::

 ConnetOS# set system aaa tacacs-plus key connetos

set system syslog log-level
-------------------------------------------

命令功能
+++++++++++++++
**set system syslog log-level** 命令用来配置日志的级别。

**delete system syslog log-facility** 命令用来删除配置的日志级别，恢复到缺省值。

缺省情况下，日志的级别是 **warning**。

命令格式
+++++++++++++++
**set system syslog log-level** { **error** | **fatal** | **info** | **trace** | **warning** }

**delete system syslog log-level**

参数说明
+++++++++++++++
**error**：错误。

**fatal**：致命。

**info**：提示。

**trace**：跟踪。

**warning**：警告。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置日志的级别是error::

 ConnetOS# set system syslog log-level error

show system syslog
-------------------------------------------

命令功能
+++++++++++++++
**show system syslog** 命令用来查看设备的日志信息。

命令格式
+++++++++++++++
**show system syslog** [ **host** [ **server-ip** ] ] 

参数说明
+++++++++++++++
**host**：查看日志服务器的地址。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查看设备上的日志信息::

 ConnetOS# show system syslog
 Waiting for building configuration.
    host {
        server-ip 2.2.2.2
    }
    log-level: "error"
    log-facility: 3
