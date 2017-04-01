系统时间设置命令
=======================================

set date
-------------------------------------------

命令功能
+++++++++++++++
**set date** 命令用来设置系统时间。

命令格式
+++++++++++++++
**set date** *date*

参数说明
+++++++++++++++
*date*：系统时间。可以设置的系统时间包括：hh:mm[:ss]; [YYYY.]MM.DD-hh:mm[:ss]; MMDDhhmm[YYYY][.ss]

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 设置当前时间为14:52:00::

 ConnetOS> set date 14:52:00

set system ntp-server-ip
-------------------------------------------

命令功能
+++++++++++++++
**set system ntp-server-ip** 命令用来指定NTP服务器的地址。

**delete system ntp-server-ip** 命令用来删除配置的NTP服务器地址。

缺省情况下，没有配置NTP服务器。

命令格式
+++++++++++++++
**set system ntp-server-ip** *ip-address*

**delete system ntp-server-ip**

参数说明
+++++++++++++++
*ip-address*：NTP服务器的地址

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 指定NTP服务器的地址为1.1.1.1::

 ConnetOS# set system ntp-server-ip 1.1.1.1

set system timezone
---------------------------------------

命令功能
+++++++++++++++
**set system timezone** 命令用来配置系统时区。

**delete system timezone** 命令用来删除配置的系统时区，恢复为缺省值。

缺省情况下，系统时区为UTC。

命令格式
+++++++++++++++
**set system timezone** *timezone*

**delete system timezone**

参数说明
+++++++++++++++
*timezone*：系统时区。系统支持的时区，请在设备上查看。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 设置系统时区为Africa/Malabo::

 ConnetOS# set system timezone Africa/Malabo