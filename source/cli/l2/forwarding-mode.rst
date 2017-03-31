转发模式配置命令
=======================================

set forwarding-options forwarding-mode
-------------------------------------------

命令功能
+++++++++++++++
**set forwarding-options forwarding-mode** 命令用来设置设备的转发模式。

**delete forwarding-options forwarding-mode** 命令用来删除配置的转发模式，恢复为缺省值。

缺省情况下，设备采用存储转发模式。

命令格式
+++++++++++++++
**set forwarding-options forwarding-mode** { **cut-through** | **store-and-forwarding** }

**delete forwarding-options forwarding-mode**

参数说明
+++++++++++++++
**cut-through**：直通模式。设备接收到基本的用于二层转发的头部信息后就进行转发，不对数据包做帧校验，时延小。

**store-and-forwarding**：存储转发模式。设备把完整的数据包收完才进行转发，会对数据包做帧校验。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
直通模式主要应用于网络环境较好的情况下，可以做到比存储转发的时延小。如果线上的应用业务对时延的敏感度没有达到这个级别，建议使用存储转发模式。

配置举例
+++++++++++++++
# 配置设备的转发模式为直通模式::

 ConnetOS# set forwarding-options forwarding-mode cut-through