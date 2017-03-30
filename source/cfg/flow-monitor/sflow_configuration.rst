sFlow配置
===============

sFlow简介
----------------

概述
++++++++++++++++++++++++++++++
sFlow（Sampled Flow）采样流，是一种基于报文采样的网络流量监控技术，主要用于对网络流量进行统计分析。

企业网络规模较小、组网灵活，容易出现由于组网或者遭受攻击导致的流量业务异常。所以企业用户需要实时监控接口的流量状况，以便及时采取措施来保证企业网络的正常稳定运行。

sFlow关注的是接口的流量情况、转发情况以及设备整体运行状况，适合于网络异常监控以及网络异常定位，为企业用户的日常巡检维护提供了极大的方便。特别适合于企业网用户。

原理介绍
++++++++++++++++++++++++++++++

sFlow系统组成
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

sFlow系统由sFlow Agent和sFlow Collector组成。sFlow Agent嵌入到交换机中，对接口上的流量进行采样，然后将采样结果发送给sFlow collector。sFlow collector对sFlow报文进行分析，并显示分析结果。

采样机制
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
sFlow Agent将接口上获取的将信息封装成sFlow报文，当sFlow报文缓冲区满或达到sFlow报文老化时间后，将sFlow报文发送到指定的sFlow Collector。

sFlow Agent提供了两种采样方式，供用户从不同的角度分析网络流量状况：

  * Flow采样： 基于数据包的流采样。在指定接口上按照特定的采样方向和采样比对报文进行采样分析。
  * Counter采样：基于时间的统计信息采样。在指定接口上周期性地获取流量统计信息、内存使用信息。

Flow采样和Counter采样是两种相互独立的采样，两者互相没有影响。但是由于采样的方式不一样，获取的信息维度也不一样。Flow方式关注流量的详细信息，更聚焦于具体的流的分析，可以监控和分析网络上的流行为。而Counter采样只关注接口上流量的数量，不关注流量的详细信息。

优势
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
和其他网络流量监控技术相比，sFlow 具有如下优点:

 * 能够在线实时的监控每个接口。
 * 可以针对不同接口设置不同的采样方式及采样参数，采样灵活。
 * 采样时不需要镜像流量，对网络性能影响小。
 * sFlow Agent内嵌在设备中，不需要额外的监测设备和接口，节省成本。

配置sFlow
----------------
在配置sFlow时：

#. 首先需要指定进行sFlow采样的接口，即使能接口下的sFlow使能，并设置采样比或采样时间等采样参数。

#. 如果不配置接口下的采样参数，就按照全局的采样参数进行采样。如果配置了接口下的采样参数，就按照接口下的采样参数进行采样。

#. 必须指定Collector，否则无法进行采样分析。

配置Flow采样
++++++++++++++++++++++++++++++

#. 进入配置模式。

   ConnetOS> **configure**
 
#. 配置全局sFlow的采样比。
 
   ConnetOS# **set protocols sflow sampling-rate** { **ingress** | **egress** }  *sampling-rate*

   缺省情况下，全局sFlow的采样比为2000。

#. 配置全局sFlow的采样报文最大长度。
  
   ConnetOS# **set protocols sflow sampling-rate** { **ingress** | **egress** } *header-length*

#. 使能指定接口的sFlow的功能

   ConnetOS# **set protocols sflow interface** *interface-name* **enable** { **false** | **ture** }

   sFlow采样时必须指定接口进行采样。

#. （可选）配置指定接口下的采样比。

   ConnetOS# **set protocols sflow interface** *interface-name* **sampling-rate**  { **ingress** | **egress** } *sampling-rate*

   如果接口下不配置采样比，就按照全局下的配置生效。

#. （可选）配置指定接口下的采样报文最大长度。

   ConnetOS# **set protocols sflow interface** *interface-name* **header-length** *header-length*
   
   如果接口下不配置采样报文最大长度，就按照全局下的配置生效。

#. 指定Collector的IP地址。
   
   ConnetOS# **set protocols sflow collector address** *ip-address*

#. 指定Collector的端口号。
   
   ConnetOS# **set protocols sflow collector port** *port-number*

#. 提交配置

   ConnetOS# **commit**

配置Counter采样
++++++++++++++++++++++++++++++

#. 进入配置模式。

   ConnetOS> **configure**

#. 配置全局Counter采样的时间间隔报文。

   ConnetOS# **set protocols sflow polling-interval** *polling-interval*
   
   如果接口下不配置采样时间间隔，就按照全局下的配置生效。

#. 使能指定接口的sFlow的功能

   ConnetOS# **set protocols sflow interface** *interface-name* **enable** { **false** | **ture** }

   sFlow采样时必须指定接口进行采样。

#. （可选）配置接口下的Counter采样的时间间隔报文。

   ConnetOS# **set protocols sflow interface** *interface-name* **polling-interval** *polling-interval*
 
   如果接口下不配置采样时间间隔，就按照全局下的配置生效。

#. 指定Collector的IP地址。
   
   ConnetOS# **set protocols sflow collector address** *ip-address*

#. 指定Collector的端口号。

   ConnetOS# **set protocols sflow collector port** *port-number*
   
#. 提交配置

   ConnetOS# **commit**

检查配置结果
++++++++++++++++++++++++++++++
# 执行 **show sflow collector** 命令，查看collector的配置信息::
 
 ConnetOS> show sflow collector
 Collector IP Address  UDP Port   Flow Sample Counters   Counter Sample Counters   Datagram Counters
 --------------------    --------     --------------------        -----------------------       -----------------  
 2.2.2.2              6400      0                     4                      4     

# 执行 **show sflow** 命令，查看全局的sFlow配置信息::

 ConnetOS> show sflow
 Status   Agent IP Address   Ingress Sample Rate   Egress Sample Rate   Polling Interval   Header Length
 --------   ----------------     -------------------       ------------------       ----------------     -------------
 Enabled  192.168.1.35     1:2000              1:2000              60s             64B

# 执行 **show sflow interface** 命令，查看接口上的sFlow配置信息::

 ConnetOS> show sflow interface
 Interface  Status    Ingress Sample Rate  Egress Sample Rate  Polling interval    Header length
 ---------   ---------   -------------------      -----------------------   ----------------     -------------
 te-1/1/1   Enabled  1:2000             1:2000             60s             100B
 te-1/1/2   Enabled  1:600              1:2000             0s              64B         64B
