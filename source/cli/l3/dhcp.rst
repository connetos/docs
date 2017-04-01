DHCP Relay命令
=======================================

set vlan-interface interface dhcp-relay server-ip
--------------------------------------------------------

命令功能
+++++++++++++++
**set vlan-interface interface dhcp-relay server-ip** 命令用来指定DHCP Relay服务器。

**set vlan-interface interface dhcp-relay server-ip** 命令用来指定DHCP Relay服务器。

缺省情况下，没有指定HCP Relay服务器。

命令格式
+++++++++++++++
**set vlan-interface interface** *l3-interface-name* **dhcp-relay server-ip** *ip-address*

**delete vlan-interface interface** *l3-interface-name* **dhcp-relay server-ip** *ip-address*

参数说明
+++++++++++++++
*l3-interface-name*：vlan－interface的名称。

*ip-address*：DHCP Relay服务器的IP地址。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 指定IP地址为1.1.1.1的DHCP Relay服务器作为本设备的服务器::

 ConnetOS# set vlan-interface interface vlan3 dhcp-relay server-ip 1.1.1.1

 