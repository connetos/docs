sDrop配置
=======================================

概述
---------------------------------------

sDrop简介
+++++++++++++++++++++++++++++++++++++++
现代网络中出现的大部分的网络问题都跟丢包有扯不开的关系，而如何对丢包进行诊断一直是繁杂且专业的问题，针对这一现象ConnetOS对现今的数据中的网络环境中的丢包进行了详细的分析，并设计了sDrop（Streaming Dropped packet）解决用户所关注的问题。

不同于sFlow主要分析接口转发的数据流量，sDrop主要用于分析丢弃的数据流量。sDrop可以解决如下情况下的丢包：
 
 * 发现瞬间突发流量丢包。
 * 协助解决业务配置错误丢包。
 * 发现网络中存在攻击流量丢包。
 * 发现网络中存在的错误的报文。

并且提供用户全网的丢包信息的收集及分析能力。

sDrop对数据中心网络中存在的20多种常见的丢包情况进行了分析后，将设备丢弃的报文分为两种：

 * 可以获取丢弃的原始报文，将报文送往CPU进行分析，得到丢包原因。
 * 无法获取丢弃的原始报文，通过获取统计信息，得到丢包的原因。

sDrop可以进行计数的比较和查看，经过一定的轮询时间，可以查询丢包内容和统计。

sDrop功能嵌入到交换机中，对设备上丢弃的报文进行采样，并将采样结果发送给 collector。collector对sFlow报文进行分析、显示分析结果。

.. note::
 collector可以是安装了分析软件的用户终端，或专门的分析设备。

丢包查看方式
++++++++++++++++++++++++++++++++++++++

对于丢包的感知，ConnetOS提供了设备上和设备外两种展示方式。

 * 设备支持将报文的丢包信息导出，通过wireshark的lua插件进行展示。
 * 对于设备上的报文，通过 **show sdrop** 命令查看报文的实际内容，定位基本的丢包原因。

配置sDrop
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**
 
#. 配置sDrop采样的轮询时间。
 
   ConnetOS# **set protocols sdrop polling-interval** *polling-interval*

   缺省情况下，轮询时间是60s。

#. 指定Collector的IP地址。
   
   ConnetOS# **set protocols sdrop collector address** *ip-address*

#. 指定Collector的UDP端口号。
   
   ConnetOS# **set protocols sdrop collector port** *port-number*

   缺省情况下，UDP端口号的端口号是32768。

#. 提交配置

   ConnetOS# **commit**

检查配置结果
---------------------------------------
执行 **show sdrop** 命令，查看丢弃报文的信息::

 ConnetOS 1> show sdrop
 Info of Dropped Packets in last 1 min.
 Input Physical Port     Output Physical Port    Drop Reason                             Last Detectted Time
 --------------------    --------------------    -----------------------------------     ---------------------
 NA                      te-1/1/2                Exceed Egress Buffer Threshold          2017-03-23 14:56:55
 NA                      te-1/1/5                Exceed Egress Buffer Threshold          2017-03-23 14:56:55
 NA                      te-1/1/6                Exceed Egress Buffer Threshold          2017-03-23 14:56:55
 NA                      te-1/1/48               Exceed Egress Buffer Threshold          2017-03-23 14:56:55



