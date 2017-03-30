sDrop配置
=======================================

sDrop概述
---------------------------------------
不同于sFlow主要分析接口转发的数据流量，sDrop主要用于分析丢弃的数据流量。

设备丢弃的报文有两种：
 
 * 可以用 **show sdrop** 命令查看报文的实际内容，如转发层面的丢包。
 * 不能看到报文的实际内容，只在设备上有计数统计。如硬件buffer不够导致的丢包。

sDrop可以进行计数的比较和查看，经过一定的轮询时间，可以查询丢包内容和统计。

sDrop功能嵌入到交换机中，对设备上丢弃的报文进行采样，并将采样结果发送给 collector。collector对sFlow报文进行分析、显示分析结果。

.. note::
 collector可以是安装了分析软件的用户终端，或专门的分析设备。

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



