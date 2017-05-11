系统信息查询命令参考
=======================================

show system ddm 
---------------------------------------

命令功能
+++++++++++++++
**show system ddm** 命令用来查看设备上光模块DDM信息。

命令格式
+++++++++++++++
**show system ddm** [ *interface-name* ]

参数说明
+++++++++++++++
*interface-name*：接口名称。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查看设备上所有光模块DDM信息::

 ConnetOS> show system ddm
 Interface   Temp(C)  Voltage(V)  Bias(mA)  Tx Power(dBm)  Rx Power(dBm)  Module Type
 ----------  -------  ----------  --------  -------------  -------------  -----------
 te-1/1/6    36.24    3.39        8.10      -1.94          -2.80          SR/850nm
 te-1/1/7    28.45    3.35        5.14      -2.32          -2.75          SR/850nm
 te-1/1/34   32.33    3.37        8.09      -2.15          -2.24          SR/850nm
 qe-1/1/52   35.78    3.29        5.83      -3.61          -2.52          SR4/850nm
 qe-1/1/54   33.78    3.33        NA        NA             NA             SR4/850nm

show system fan
-------------------------------------------

命令功能
+++++++++++++++
**show system fan** 命令用来查询风扇的转速和PWM值。

命令格式
+++++++++++++++
**show system fan**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查询风扇的转速和PWM值::

 ConnetOS> show system fan
 Fan Status:
     Fan 1 : speed =  8925 RPM, PWM =  40%
     Fan 2 : speed =  8850 RPM, PWM =  40%
     Fan 3 : speed =  8850 RPM, PWM =  40%
     Fan 4 : speed =  8850 RPM, PWM =  40%
     Fan 5 : speed =  8850 RPM, PWM =  40%

show system rpsu
-------------------------------------------

命令功能
+++++++++++++++
**show system rpsu** 命令用来查询电源信息。

命令格式
+++++++++++++++
**show system rpsu**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
本命令可以查询电源模块的SN号、温度、风扇转速、电压、电流和功率，并能对电源模块的状态进行监控展示。

配置举例
+++++++++++++++
# 查询电源信息::

 ConnetOS> show system rpsu
 RPSU 1:
     Module Status   : OK
     Serial Number   : SA020T051623000218
     Temperature     : 29     Centigrade
     IIN             : 0.43   A
     VIN             : 215.00 V
     PIN             : 89.00  W
     IOUT            : 6.16   A
     VOUT            : 12.02  V
     POUT            : 74.00  W
 RPSU 2:
     Module Status   : Unpresent

show system running-mode
-------------------------------------------

命令功能
+++++++++++++++
**show system running-mode** 查看系统的运行状态，单机还是堆叠。

命令格式
+++++++++++++++
**show system running-mode**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查看设备的运行状态::

 ConnetOS> show system running-mode
 Current mode      :  Standalone

show system serial-number
-------------------------------------------

命令功能
+++++++++++++++
**show system serial-number** 命令用来查询系统的SN信息，包括主板SN、电源模块SN以及光模块信息。

命令格式
+++++++++++++++
**show system serial-number**

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
# 查询产品序列号信息::

 ConnetOS> show system serial-number
 MotherBoard Serial Number : SW047110G826000010
 RPSU 1 Serial Number      : SA020T051623000218
 RPSU 2 is not ready.
 SFP+ te-1/1/6
     Vendor Name           : FINISAR CORP.
     Serial Number         : MUG0ZRH
     Product Number        : FTLX8571D3BCL
     Module Type           : SR/850nm
     Cable Length          : 300.0m
 SFP+ te-1/1/7
     Vendor Name           : CISCO-SUMITOMO
     Serial Number         : SPC150704J2
     Product Number        : SPP5100SR-C5
     Module Type           : SR/850nm
     Cable Length          : 300.0m
 SFP+ te-1/1/34
     Vendor Name           : FINISAR CORP.
     Serial Number         : MUG1702
     Product Number        : FTLX8571D3BCL
     Module Type           : SR/850nm
     Cable Length          : 300.0m
 QSFP+ qe-1/1/52
     Vendor Name           : Yunqi
     Serial Number         : RD160900420010
     Product Number        : RTXM320-571
     Module Type           : SR4/850nm
     Cable Length          : 300.0m
 QSFP+ qe-1/1/54
     Vendor Name           : FINISAR CORP
     Serial Number         : XUC06GP
     Product Number        : FTL410QE2C
     Module Type           : SR4/850nm
     Cable Length          : 100.0m

show system temperature
-------------------------------------------

命令功能
+++++++++++++++
**show system temperature** 命令用来查看设备的温度信息。

命令格式
+++++++++++++++
**show system temperature**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查询设备温度信息::

 ConnetOS> show system temperature
 Temperature: 31 Centigrade
     Sensor 1 Temperature :  32 Centigrade
     Sensor 2 Temperature :  33 Centigrade
     Sensor 3 Temperature :  30 Centigrade
