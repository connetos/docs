.. configure documentation master file, created by
   sphinx-quickstart on Mon Feb 20 18:25:17 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

命令参考
=====================================
本章介绍了设备中各特性的配置命令，包括每条命令的功能、格式、参数、视图、缺省级别、使用指南和举例。

.. toctree::
   :maxdepth: 1
   :glob:
   :numbered:

   basic/index
   system-manage/index
   interface/index
   l2/index
   l3/index
   qos/index
   flow-monitor/index
   iss/index
   vxlan/index
   

  
命令行格式约定

================  =================================================
符号               说明
================  =================================================
粗体               命令行关键字，必须原样输入。
斜体               命令行参数，需要按照要求输入实际值。
[ ]                命令行配置过程中，括号中的部分是可选的
[ a | b | ……]      从括号中的值选取一个或不选
{ a | b | ……}      从括号中的值选取一个
[ a | b | ……] *    从括号中的值选取多个或不选
{ a | b | ……} *    从括号中的值选取一个或多个
================  ================================================= 

