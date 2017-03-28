镜像命令
==========================================
set analyzer instance input
-------------------------------------------

命令功能
+++++++++++++++
**set analyzer instance input** 命令用来配置镜像端口。

**delete analyzer instance input** 命令用来删除配置的镜像端口。

缺省情况下，没有配置镜像端口。

命令格式
+++++++++++++++
**set analyzer instance** instance-name **input** { **egress** | **ingress** } *interface-name*

**delete analyzer instance** instance-name **input** { **egress** | **ingress** } *interface-name*

参数说明
+++++++++++++++
*instance-name*：镜像实例的名称。

**egress**：对出方向的流量进行镜像。

**ingress**：对入方向的流量进行镜像。

*interface-name*：接口名称。此接口是用于做镜像的接口。


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
如果要对接口双向的流量进行镜像，分别配置出、入方向的端口镜像即可。

配置举例
+++++++++++++++
# 对接口te-1/1/1上ingress方向的报文进行镜像::

 ConnetOS#  set analyzer instance mirror1 input ingress te-1/1/1

set analyzer instance output
-------------------------------------------

命令功能
+++++++++++++++
**set analyzer instance output** 命令用来配置镜像时的观测端口。

**delete analyzer instance output** 命令用来删除配置的镜像观测端口。

缺省情况下，没有配置观测端口。

命令格式
+++++++++++++++
**set analyzer instance** *instance-name* **output** *interface-name*

**delete analyzer instance** *instance-name* **output**


参数说明
+++++++++++++++
*instance-name*：镜像实例的名称。

*interface-name*：接口名称。此接口是将镜像的报文复制到的接口。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 设置接口te-1/1/2为观测端口::

 ConnetOS# set analyzer instance mirror1 output te-1/1/2

show analyzer
-------------------------------------------

命令功能
+++++++++++++++
**show analyzer** 命令用来查看端口镜像的配置信息。

命令格式
+++++++++++++++
**show analyzer** [ *instance-name* ]

参数说明
+++++++++++++++
*instance-name*：镜像实例的名称。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
如果指定 *instance-name* ，查看的是指定镜像的配置信息；否则查看的是设备上所有镜像的配置信息。

配置举例
+++++++++++++++
# 查看设备上所有镜像的配置信息::

 ConnetOS> show analyzer 
 Analyzer name: mirror1 
 Output interface: <te-1/1/2>
 Ingress monitored interfaces: <te-1/1/1> 
 Egress monitored interfaces:
