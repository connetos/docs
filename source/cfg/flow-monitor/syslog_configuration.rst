系统日志
=======================================

简介
---------------------------------------
设备运行过程中，日志模块会对设备运行中的各种情况进行记录，从而形成Syslog系统日志。

当设备出现异常或故障时，通过系统日志，用户可以查看设备的运行状态、分析网络的状况以及定位问题发生的原因，为系统诊断和维护提供依据。

日志的格式
+++++++++++++++++++++++++++++++++++++++
系统日志的各个字段之间用空格隔开，标准格式为：

事件发生的时间   哪台主机的日志   产生日志信息的系统   系统发生的事件

如::
 
 Apr 12 2017 17:53:57 ConnetOS local0.debug : [1][rtrmgr] user admin requested non-exclusive config

日志facility
+++++++++++++++++++++++++++++++++++++++
facility，是用来指定产生日志的程序模块。syslog服务器上根据facility的值来对日志进行区分。

本地设备的facility的标识为local0～local7，缺省情况下facility的标识为local0。

日志级别
+++++++++++++++++++++++++++++++++++++++
日志级别是用来表示日志的严重程度。

===========   ==========================
级别			      含义
===========   ==========================
info          一般提示信息
trace         调试信息
warning       告警信息
error	        错误事件
fatal         致命错误，必须马上采取行动
===========   ==========================

日志的存储
+++++++++++++++++++++++++++++++++++++++
生成的系统日志可以在本设备查看，也可以输出到日志服务器进行查看。

配置系统日志
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 配置日志级别。

   ConnetOS# **set system syslog log-level** { **error** | **fatal** | **info** | **trace** | **warning** }

   缺省情况下，日志级别是warning。

#. 配置日志的facility。

   ConnetOS# **set system syslog log-facility** *facility-number*

   缺省情况下，日志的facility级别是0，即local0。

#. （可选）指定远端日志服务器，用于接收ConnetOS发送过来的日志。

   ConnetOS# **set system syslog host server-ip** *ip-address*

#. 提交配置

   ConnetOS# **commit**

#. 打开日志监控功能
  
   ConnetOS> **syslog monitor** { **off** | **on** }


查看本地系统日志
---------------------------------------
ConnetOS系统支持按行数和日期查看系统日志。

* 按行数查看日志::
   
   ConnetOS> show log last-rows 4
   Apr 12 2017 11:36:50 ConnetOS local2.debug : [1][cli_sh] Parsing configuration
   Apr 12 2017 11:36:57 ConnetOS local2.debug : [1][cli_sh] Starting CLI
   Apr 12 2017 11:36:57 ConnetOS local0.warning : admin logined the switch cli
   Apr 12 2017 11:37:10 ConnetOS local0.warning : [1][cli_sh] Executing command by admin: 
   "show log last-rows 4"

* 按日期查看日志::
   
   ConnetOS> show log date 2017.4.18
   Apr 18 2017 15:41:38 ConnetOS local0.info : START: telnet pid=29107 from=192.168.1.141
   Apr 18 2017 15:41:58 ConnetOS local0.debug : [1][rtrmgr] registering interest in 
   cli-29134-ConnetOS
   Apr 18 2017 15:41:58 ConnetOS local2.debug : [1][cli_sh] Waiting for configuration from 
   rtrmgr
   Apr 18 2017 15:41:58 ConnetOS local0.debug : [1][rtrmgr] XRL Birth: class 
   cli-29134-ConnetOS instance cli-29134-ConnetOS-dfe1a22adc1cbd2ebbdae103226aee58@127.0.0.1
   Apr 18 2017 15:41:59 ConnetOS local2.debug : [1][cli_sh] Parsing configuration
   Apr 18 2017 15:42:05 ConnetOS local2.debug : [1][cli_sh] Starting CLI
   Apr 18 2017 15:42:05 ConnetOS local0.warning : admin logined the switch cli
   Apr 18 2017 15:42:22 ConnetOS local0.warning : [1][cli_sh] Executing command by admin: 
   "show version "
   Apr 18 2017 15:42:38 ConnetOS local0.warning : [1][cli_sh] Executing command by admin: 
   "show log date 2017.4.18"
