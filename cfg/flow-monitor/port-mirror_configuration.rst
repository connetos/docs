端口镜像配置
===================

端口镜像概述
----------------
在网络维护的过程中会遇到需要对报文进行获取和分析的情况，比如怀疑有攻击报文，此时需要在不影响报文转发的情况下，对报文进行获取和分析。

端口镜像是指在不影响报文正常处理流程的情况下，将镜像端口的报文复制一份到观测端口。用户可以利用数据监控设备来分析复制到观测端口的报文，进行网络监控和故障排除。

 * 镜像端口：又叫源端口，是被监控的端口，从镜像端口流经的报文将被复制到观测端口。

 * 观测端口：又叫目的端口，是连接监控设备的端口，用于输出从镜像端口复制过来的报文。

配置端口镜像
----------------
端口镜像支持对镜像端口入方向、出方向或双向的流量进行镜像。如果要对双向的流量进行镜像，分别配置出、入方向的端口镜像即可。input表示配置镜像端口，output表示配置观测端口。

#. 进入配置模式。

   ConnetOS> **configure**
 
#. 配置镜像端口。

  ConnetOS# **set analyzer instance** **instance-name* **input** { **egress** | **ingress** } *interface-name*

#. 配置观测端口，观测端口不可以是LAG成员。
  
   ConnetOS# **set analyzer instance** *instance-name* **output** *interface-name*

#. 提交配置

   ConnetOS# **commit**

检查配置结果
-------------
# 查看端口镜像的相关配置信息::

 ConnetOS# show analyzer
      instance mirror1 {
         input {
             egress "te-1/1/10"
         }
         output: "te-1/1/20"
     }

# 查看镜像信息::

 ConnetOS# show analyzer
 Analyzer name: mirror1
 Output interface: <te-1/1/20>
 Ingress monitored interfaces:
 Egress monitored interfaces: <te-1/1/10>
