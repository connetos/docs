系统信息查询
=======================================

查询版本信息
---------------------------------------
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
---------------------------------------
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
---------------------------------------
ConnetOS支持对风扇的转速和PWM值进行查询::

 ConnetOS> show system fan
 Fan Status:
     Fan 1 : speed =  8850 RPM, PWM =  40%
     Fan 2 : speed =  8700 RPM, PWM =  40%
     Fan 3 : speed =  8850 RPM, PWM =  40%
     Fan 4 : speed =  8775 RPM, PWM =  40%
     Fan 5 : speed =  8850 RPM, PWM =  40%

查询系统序列号
---------------------------------------
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
---------------------------------------
DDM（Digital Diagnostic Monitoring）数字诊断监控功能，可以监测模块温度、电压、偏置电流、收发光功率等，上述监控参数经过A/D转换后，会被写入模块内部的EEPROM，此部分内容由SFF-8472进行定义。

ConnetOS支持对光模块的DDM信息进行查询展示::

 ConnetOS> show system ddm
 Interface   Temp(C)  Voltage(V)  Bias(mA)  Tx Power(dBm)  Rx Power(dBm)  Module Type
 ----------  -------  ----------  --------  -------------  -------------  -----------
 te-1/1/6    36.24    3.39        8.10      -1.94          -2.80          SR/850nm
 te-1/1/7    28.45    3.35        5.14      -2.32          -2.75          SR/850nm
 te-1/1/34   32.33    3.37        8.09      -2.15          -2.24          SR/850nm
 qe-1/1/52   35.78    3.29        5.83      -3.61          -2.52          SR4/850nm
 qe-1/1/54   33.78    3.33        NA        NA             NA             SR4/850nm
