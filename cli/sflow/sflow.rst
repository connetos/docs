sFlow命令
================================

clear sflow statistics
-------------------------------------------

命令功能
+++++++++++++++
**clear sflow statistics** 命令用来清除设备上的sFlow的统计信息。

命令格式
+++++++++++++++
**clear sflow statistics**

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
# 清除sFlow的统计信息::

 ConnetOS> clear sflow statistics

set protocols sflow collector
-------------------------------------------

命令功能
+++++++++++++++
**set protocols sflow collector** 命令用来指定sFlow Collector

**delete protocols sflow collector** 命令用来删除指定的sFlow Collector。

缺省情况下，没有指定sFlow Collector。

命令格式
+++++++++++++++
**set protocols sflow collector** { **address** *ip-address* | **port** *port-number* }

**delete protocols sflow collector** { **address** | **port** }


参数说明
+++++++++++++++
*ip-address*：sFlow Collector的IP地址。只支持配置一个sFlow Collector。

*port-number*：sFlow Collector使用的UDP端口号。整数形式，取值范围是1～65535。

缺省情况下，UDP端口号为6343。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
只有配置了sFlow Collector之后，sFlow才开始进行采样。

配置举例
+++++++++++++++
# 指定地址为1.1.1.1的sFlow Collector作为采样输出的Collector::

 ConnetOS# set protocols sflow collector 1.1.1.1 udp-port 6500

set protocols sflow header-length
-------------------------------------------

命令功能
+++++++++++++++
**set protocols sflow header-length** 命令用来配置全局的sFlow采样报文长度。

**delete protocols sflow header-length** 命令用来删除配置的全局采样报文长度，恢复为缺省值。

缺省情况下，采样报文长度是128字节。

命令格式
+++++++++++++++
**set protocols sflow header-length** *header-length*

**delete protocols sflow header-length**

参数说明
+++++++++++++++
*header-length*：采样报文长度。整数形式，取值范围是64～512，单位是字节。


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
采样时，如果被采样的报文的长度小于配置的采样长度，那么采样全部报文。

配置举例
+++++++++++++++
# 配置全局的sFlow采样报文长度为512byte::

 ConnetOS# set protocols sflow header-length 512

set protocols sflow interface enable
-------------------------------------------

命令功能
+++++++++++++++
**set protocols sflow interface enable** 命令用来配置是否使能接口下的sFlow功能。

**delete protocols sflow interface enable** 命令用来删除接口下的sFlow功能。

缺省情况下，接口下的sFlow功能并没有使能。

命令格式
+++++++++++++++
**set protocols sflow interface** *interface-name* **enable** { **falses** | **true** }

**delete protocols sflow interface** *interface-name* **enable**

参数说明
+++++++++++++++
*interface-name*：接口名称。

**false**：去使能接口下的sFlow功能。

**true**：使能接口下的sFlow功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
如果sFlow功能要生效，必须使能具体接口的sFlow功能。

配置举例
+++++++++++++++
# 使能接口te-1/1/1的sFlow功能::

 ConnetOS# set protocols sflow interface te-1/1/1 enable true

set protocols sflow interface header-length
-----------------------------------------------------

命令功能
+++++++++++++++
**set protocols sflow interface header-length** 命令用来配置全局的sFlow采样报文长度。

**delete protocols sflow interface header-length** 命令用来删除配置的全局采样报文长度，恢复为缺省值。

缺省情况下，采样报文长度是128字节。


命令格式
+++++++++++++++
**set protocols sflow interface** *interface-name* **header-length** *header-length*

**delete protocols sflow interface** *interface-name* **header-length** 

参数说明
+++++++++++++++
*header-length*：采样报文长度。整数形式，取值范围是64～512，单位是字节。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
如果接口下配置了报文采样长度，就按照接口下的采样长度进行采样。如果接口下没有配置，就按照全局的采样长度进行采样。

采样时，如果被采样的报文的长度小于配置的采样长度，那么采样全部报文。

配置举例
+++++++++++++++
# 配置接口te-1/1/1的sFlow采样报文长度为512 byte::

 ConnetOS# set protocols sflow interface te-1/1/1 header-length 512

set protocols sflow interface polling-interval
---------------------------------------------------------

命令功能
+++++++++++++++
**set protocols sflow interface polling-interval** 命令用来配置指定接口的sFlow采样时间间隔。

**delete protocols sflow interface polling-interval polling** 命令用来删除配置的sFlow采样时间间隔，恢复为缺省值。

缺省情况下，接口的采样间隔是0，即不采样。

命令格式
+++++++++++++++
**set protocols sflow interface** *interface-name* **polling-interval** *polling-interval*

**delete set protocols sflow interface** *interface-name* **polling-interval**

参数说明
+++++++++++++++
polling-interval：报文采样时间间隔。整数形式，取值范围是0～86400，单位是秒。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
如果接口下配置了采样间隔，就按照接口下的采样间隔进行采样。如果接口下没有配置，就按照全局的采样间隔进行采样。

配置举例
+++++++++++++++
# 配置接口下的sFlow报文采样时间间隔是100秒::

 ConnetOS# set protocols sflow interface te-1/1/1 polling-interval 100

set protocols sflow interface sampling-rate
------------------------------------------------

命令功能
+++++++++++++++
**set protocols sflow interface sampling-rate** 命令用来配置指定接口的sFlow采样比。

**delete protocols sflow interface sampling-rate** 命令用来删除配置的指定接口的采样比，恢复为缺省值。

缺省情况下，出入方向的接口sFlow采样比都是2000，即每2000个报文采样一个报文。

命令格式
+++++++++++++++
**set protocols sflow interface** *interface-name* **sampling-rate** { **egress** | **ingress** } *sampling-rate*

**delete protocols sflow interface** *interface-name* **sampling-rate** { **egress** | **ingress** } 

参数说明
+++++++++++++++
**egress**：对出方向的报文进行采样。

**ingress**：对入方向的报文进行采样。

*sampling-rate*：sFlow采样比。整数形式，取值范围是1000～1000000。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 设置sFlow对接口te-1/1/1的出方向采样比为1500::

 ConnetOS# set protocols sflow interface te-1/1/1 sampling-rate egress 1500

set protocols sflow polling-interval
-------------------------------------------

命令功能
+++++++++++++++
**set protocols sflow polling-interval** 命令用来配置全局的sFlow采样时间间隔。

**delete protocols sflow polling-interval** 命令用来删除配置的sFlow采样时间间隔，恢复为缺省值。

缺省情况下，全局的采样间隔是0，即不采样。

命令格式
+++++++++++++++
**set protocols sflow polling-interval** *polling-interval*

**delete set protocols sflow polling-interval**

参数说明
+++++++++++++++
*polling-interval*：报文采样时间间隔。整数形式，取值范围是0～86400，单位是秒。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 配置全局的sFlow报文采样时间间隔是100秒::

 ConnetOS# set protocols sflow polling-interval 100

set protocols sflow sampling-rate
-------------------------------------------

命令功能
+++++++++++++++
**set protocols sflow sampling-rate** 命令用来配置指定全局的sFlow采样比。

**delete protocols sflow interface sampling-rate** 命令用来删除配置的全局采样比，恢复为缺省值。

缺省情况下，出入方向的全局sFlow采样比都是2000，即每2000个报文采样一个报文。

命令格式
+++++++++++++++
**set protocols sflow sampling-rate** { **egress** | **ingress** } *sampling-rate*

**delete protocols sflow  sampling-rate** { **egress** | **ingress** } 

参数说明
+++++++++++++++
**egress**：对出方向的报文进行采样。

**ingress**：对入方向的报文进行采样。

*sampling-rate*：sFlow采样比。整数形式，取值范围是1000～1000000。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 设置sFlow全局出方向采样比为1500::

 ConnetOS# set protocols sflow sampling-rate egress 1500

show sflow
-------------------------------------------

命令功能
+++++++++++++++
**show sflow** 命令用来查看sFlow的配置信息。

命令格式
+++++++++++++++
**show sflow** [ **collector** | **interface** ]

参数说明
+++++++++++++++
**collector**：查看sFlow collector的配置信息。

**interface**：查看接口的sFlow配置信息。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
所有配置都必须 **commit** 之后，才能查看到配置信息。

配置举例
+++++++++++++++
# 查看全局的sFlow配置信息::

 ConnetOS> show sflow
 Status   	Agent IP Address  Ingress Sample Rate  Egress Sample Rate  Polling Interval  Header Length
 --------   	----------------  	-------------------  	   ------------------   	 ----------------    -------------
 Enabled  	192.168.1.35  	1:2000             1:2000             60s            64B
