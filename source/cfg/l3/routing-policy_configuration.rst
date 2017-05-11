路由策略配置
=====================================



这里概要介绍一下各个策略都有什么应该怎么用

配置路由策略
---------------------------------------

#. 进入配置模式。

   ConnetOS> **configure**

#. 配置静态路由。
   
   ConnetOS# **set protocols static route** *ip-address* **next-hop** *ip-address*

#. （可选）设置路由metric。
   
   ConnetOS# **set protocols static route** *ip-address* **metric** *metric-value*

#. 提交配置。

   ConnetOS# **commit**