配置系统时间
=======================================

系统时间概述
---------------------------------------
NTP（Network Time Protocol）网络时间协议是由RFC 1305定义的时间同步协议。NTP用于分布式时间服务器与客户端之间的时间同步，使网络内所有设备的时钟保持一致，从而使设备能够提供基于统一时间的多种应用。NTP报文通过UDP传输，端口号是123。

对于运行 NTP 的本地系统，既可以接受来自其他时钟源的同步，又可以作为时钟源同步其他的时钟，并且可以和其他设备互相同步。 

修改本地时间
---------------------------------------
#. 修改系统时间。

   ConnetOS> **set date time**

#. 配置NTP
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 指定NTP服务器的地址。
    
   ConnetOS# **set system ntp-server-ip** *ip-address*

#. 提交配置。

   ConnetOS# **commit**

配置时区
---------------------------------------

#. 进入配置模式。

   ConnetOS> **configure**

#. 修改系统时区
   
   ConnetOS# **set system timezone** *timezone*

   缺省情况下，系统时区为UTC。

#. 提交配置。

   ConnetOS# **commit**

配置系统日志
=======================================

配置系统日志
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 配置日志级别。

   ConnetOS# **set system syslog log-level** { **error** | **fatal** | **info** | **trace** | **warning** }

   缺省情况下，日志级别是warning。

#. 配置日志的facility值。

   ConnetOS# **set system syslog log-facility** *facility-number*

   缺省情况下，日志的facility值是0。

#. （可选）指定远端日志服务器，用于接收ConnetOS发送过来的日志。

   ConnetOS# **set system syslog host server-ip** *ip-address*

#. 提交配置

   ConnetOS# **commit**

本地日志查看
---------------------------------------
ConnetOS系统支持按行数和日期查看系统日志。

* 按行数查看日志::
   
   ConnetOS> show log last-rows 5

* 按日期查看日志: 
   
   ConnetOS> show log date 2016.11.18

查询系统信息
---------------------------------------

查询版本信息
+++++++++++++++++++++++++++++++++++++++
查看当前版本信息::
 
 ConnetOS 1> show version
 Copyright (C) 2015-2017 YUNQI TECH, Inc.
 PN             : C1020
 OS             : ConnetOS GENERAL
 Version ID     : 2.1.1
 Build Code     : r2078 (12Y17)
 Switch MAC     : 00:03:0f:64:da:4d
 Management MAC : 00:03:0f:64:da:4e
 Release Time   : 2017-03-17 11:35:05

查询电源信息
+++++++++++++++++++++++++++++++++++++++
ConnetOS支持对电源模块的SN号、温度、风扇转速、电压、电流和功率进行查询，并能对电源模块的状态进行监控展示。当前，定义了4种状态：

 * Unpresent，表示电源模块不在位。
 * No Power，表示电源模块在位，但是没有AC/DC输入。
 * Error，表示电源模块在位，有AC/DC输入，但模块工作异常。
 * OK，表示电源模块正常工作。

查看当前的电源信息::

 ConnetOS> show system rpsu
 RPSU 1:
     Module Status     : OK
     Serial Number     : SA020T051623000134
     Temperature       : 36     Centigrade
     IIN               : 0.44   A
     VIN               : 221.00 V
     PIN               : 95.00  W
     IOUT              : 7.59   A
     VOUT              : 11.94  V
     POUT              : 75.00  W
 RPSU 2:
     Module Status     : No Power
     Serial Number     : SA020T051623000142
     Temperature       : 42     Centigrade
     IIN               : 0.00   A
     VIN               : 0.00   V
     PIN               : 0.00   W
     IOUT              : 0.00   A
     VOUT              : 0.00   V
     POUT              : 0.00   W

.. note::
 由于rpsu report精度原因，查询出来的参数可能和实际有些出入。

查询风扇信息
+++++++++++++++++++++++++++++++++++++++
ConnetOS支持对风扇的转速和PWM值进行查询::

 ConnetOS> show system fan
 Fan Status:
     Fan 1 : speed =  8850 RPM, PWM =  40%
     Fan 2 : speed =  8700 RPM, PWM =  40%
     Fan 3 : speed =  8850 RPM, PWM =  40%
     Fan 4 : speed =  8775 RPM, PWM =  40%
     Fan 5 : speed =  8850 RPM, PWM =  40%

查询序列号
+++++++++++++++++++++++++++++++++++++++
ConnetOS支持对系统的SN进行查询，包括主板SN、电源模块SN以及光模块信息。

查询产品序列号::

 ConnetOS> show system serial-number
 MotherBoard Serial Number : 1626000404
 RPSU 1 Serial Number      : SA020T051623000173
 RPSU 2 Serial Number      : SA020T051623000176
 SFP+ te-1/1/2
     Vendor Name           : FINISAR CORP.
     Serial Number         : MUD1KHT
     Product Number        : FTLX8571D3BCL
     Module Type           : SR/850nm
     Cable Length          : 300.0m
 SFP+ te-1/1/5
     Vendor Name           : FINISAR CORP.
     Serial Number         : MUG11SG
     Product Number        : FTLX8571D3BCL
     Module Type           : SR/850nm
     Cable Length          : 300.0m
 SFP+ te-1/1/6
     Vendor Name           : YUNQI
     Serial Number         : RD161100070098
     Product Number        : RTXM228-551
     Module Type           : SR/850nm
     Cable Length          : 300.0m
 SFP+ te-1/1/48
     Vendor Name           : YUNQI
     Serial Number         : BP162201790061
     Product Number        : RTXM228-551
     Module Type           : SR/850nm
     Cable Length          : 300.0m
 QSFP+ qe-1/1/49
     Vendor Name           : FINISAR CORP
     Serial Number         : XUC065G
     Product Number        : FTL410QE2C
     Module Type           : SR4/850nm
     Cable Length          : 100.0m

查询光模块DDM信息
+++++++++++++++++++++++++++++++++++++++
DDM（Digital Diagnostic Monitoring）数字诊断监控功能，可以监测模块温度、电压、偏置电流、收发光功率等，上述监控参数经过A/D转换后，会被写入模块内部的EEPROM，此部分内容由SFF-8472进行定义。

ConnetOS支持对光模块的DDM信息进行查询展示::

 ConnetOS> show interface diagnostics optics all
 Interface   Temp(C)  Voltage(V)  Bias(mA)  Tx Power(dBm)  Rx Power(dBm)   Module Type
 ----------    -------     ----------    --------      -------------        -------------    -----------
 qe-1/1/49   40.31    3.32        5.83      NA            -2.01            CR4/DAC

Ping和Traceroute
=======================================
在日常的系统维护中，用户可以使用Ping功能和Tracert功能来检查当前网络的连接情况。

Ping功能
---------------------------------------
Ping功能是基于ICMP协议实现的：

源端向目的端发送ICMP回显请求(ECHO-REQUEST)报文后，根据是否收到目的端的ICMP回显应答(ECHO-REPLY)报文来判断目的端是否可达。对于可达的目的端，再根据发送报文个数、接收到响应报文个数来判断链路的质量，根据ping报文的往返时间来判断源端与目的端之间的“距离”。 

**ping** 命令是最常见的用于检测网络设备可访问性的调试工具，它使用ICMP报文信息可以来检测：
 
 * 远程设备是否可用。
 * 与远程主机通信的来回旅程（round-trip）的延迟。
 * 报文（packet）的丢失情况。

Traceroute功能
---------------------------------------
运维模式下支持traceroute操作。

*tracert* 命令用来测试数据包从发送主机到目的地所经过的网关，主要用于检查网络连接是否可达，以及分析网络什么地方发生了故障。

设备重启
=======================================
ConnetOS重启命令为 **request system reboot**，命令执行时需要输入yes或no进行确认::
 
 ConnetOS> request system reboot
 Are you sure you want to reboot (yes/no)?

设备升级
=======================================

系统升级
---------------------------------------
系统升级的步骤如下：

 #. 将image拷贝到/var/upgrade目录下。
 #. 重启设备，系统将自动完成升级::
 
     ConnetOS> request system reboot

.. Caution::
 * 执行 **request system reboot** 时，需要输入yes进行确认。
 * 升级image时，不会覆盖原有配置文件。

配置文件升级
---------------------------------------
配置文件升级主要指通过tftp方式将配置文件下载到交换机加载生效。

升级的步骤如下：
 
 #. tftp下载配置文件::

     ConnetOS> file tftp get remote-file xxx local-file connetos.boot ip-address 192.168.2.2

 #. 重启系统
 
 #. 启动后，配置文件自动加载::

     ConnetOS> request system reboot

.. Caution::
 * 上述升级命令中xxx为待升级的配置文件。
 * 上述升级命令中local-file的名字必须为connetos.boot。
 * 执行request system reboot时，需要输入yes进行确认。
 * 配置文件升级时，原有配置文件会被覆盖。

