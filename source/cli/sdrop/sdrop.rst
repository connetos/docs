sDrop命令
=========================

set protocols sdrop collector address
-------------------------------------------

命令功能
+++++++++++++++
**set protocols sdrop collector address** 命令用来指定sDrop Collector。

**delete protocols sdrop collector address** 命令用来删除指定的sDrop Collector。

缺省情况下，没有指定sDrop Collector。

命令格式
+++++++++++++++
**set protocols sdrop collector address** *ip-address*

**delete protocols sdrop collector address**

参数说明
+++++++++++++++
*ip-address*：sDrop Collector的IP地址。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
只能指定一个sDrop Collector。

配置举例
+++++++++++++++
# 指定IP地址是1.1.1.1的服务器作为本设备的sDrop Collector。::

 ConnetOS# set protocols sdrop collector address 1.1.1.1

set protocols sdrop collector port
-------------------------------------------

命令功能
+++++++++++++++
**set protocols sdrop collector port** 命令用来配置sDrop Collector的UDP端口号。

**delete protocols sdrop collector port** 命令用来删除配置的轮UDP端口号，恢复为缺省值。

缺省情况下， sDrop Collector的UDP端口号为32768。

命令格式
+++++++++++++++
**set protocols sdrop collector port** *port-number*

**delete protocols sdrop collector port** 

参数说明
+++++++++++++++
*port-number*：UDP端口号。整数形式，取值范围是32768～65535。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置sDrop Collector的UDP端口号为65535::

 ConnetOS# set protocols sdrop collector port 65535

set protocols sdrop polling-interval
-------------------------------------------------------

命令功能
+++++++++++++++
**set protocols sdrop polling-interval** 命令用来配置sDrop采样的轮询时间。

**delete protocols sdrop polling-interval** 命令用来删除配置的轮询时间，恢复为缺省值。

缺省情况下，采样时间是60s。

命令格式
+++++++++++++++
**set protocols sdrop polling-interval** *polling-interval*

**delete protocols sdrop polling-interval** 

参数说明
+++++++++++++++
*polling-interval*：报文采样的轮询时间。整数形式，取值范围是1～60，单位是秒。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置采样时间间隔是30秒::

 ConnetOS# set protocols sdrop collector polling-interval 30

show sdrop
-------------------------------------------------------

命令功能
+++++++++++++++
**show sdrop** 命令用来查看设备上报文的丢弃信息。

命令格式
+++++++++++++++
**show sdrop**

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
# 查看设备上报文丢弃的信息::

 ConnetOS 1> show sdrop
 Info of Dropped Packets in last 1 min.
 Input Physical Port     Output Physical Port    Drop Reason                             Last Detectted Time
 --------------------    --------------------    -----------------------------------     ---------------------
 NA                      te-1/1/2                Exceed Egress Buffer Threshold          2017-03-23 14:56:55
 NA                      te-1/1/5                Exceed Egress Buffer Threshold          2017-03-23 14:56:55
 NA                      te-1/1/6                Exceed Egress Buffer Threshold          2017-03-23 14:56:55
 NA                      te-1/1/48               Exceed Egress Buffer Threshold          2017-03-23 14:56:55
