初次登录设备
=======================================

登录方式简介
---------------------------------------
用户可以通过Console口、Telnet、SSH等方式登录交换机，但是当用户需要为第一次上电的设备进行配置时，必须使用Console口登录。

 * Console口进行本地登录是最基本的登录方式，也是配置其他登录方式的基础。
 * 用户通过SSH／Telnet远程登录到交换机上，对交换机进行远程管理和维护。

通过Console口登录设备
---------------------------------------
在配置通过Console口登录设备之前，需要准备好：

 * Console口通信线缆
 * PC端仿真软件

通过Console口登录时：

 #. 首先用通信线缆把PC机和交换机连接起来；
 #. 然后在PC机上运行终端仿真程序（如Windows的超级终端），选择与交换机相连的串口，设置终端通信参数。

    用户终端的参数配置必须和交换机Console口的缺省配置保持一致，用户才能通过Console口登录到交换机上。

ConnetOS上，Console口的缺省配置如下：

 ================  ================
 参数               缺省值
 ================  ================
 传输速率           115200 bit/s
 流控方式           不进行流控
 奇偶校验           不进行校验
 停止位             1
 数据位             8
 ================  ================ 

管理口配置
---------------------------------------

配置管理口
+++++++++++++++++++++++++++++++++++++++
#. 进入配置模式。

   ConnetOS> **configure**

#. 配置管理口的IP地址。

   ConnetOS# **set interface management-ethernet eth0 address** *ip-address*

   缺省情况下，管理口的IP地址为0.0.0.0/0。

#. （可选）开启管理口的DHCP功能。

   ConnetOS# **set interface management-ethernet eth0 dhcp enable** { **false** | **true** }

   缺省情况下，管理口的DHCP功能是开启的。

#. 提交配置。

   ConnetOS# **commit**

检查配置结果
+++++++++++++++++++++++++++++++++++++++
执行 **show interface management-ethernet eth0** 命令查看管理口的详细信息::

 ConnetOS> show interface management-ethernet eth0 
 eth0     Inet addr: 192.168.30.24/24， Gateway: 0.0.0.0， HW address: 08:9e:01:88:51:ba

带内访问配置
---------------------------------------
ConnetOS系统除了支持从管理口登录外，还支持从三层接口进行登录，使用三层接口的IP地址当作管理口IP使用。

该功能在ConnetOS系统下缺省是开启的。

配置带内访问
+++++++++++++++++++++++++++++++++++++++
#. 进入配置模式。

   ConnetOS> **configure**

#. 配置带内访问功能是否开启。
   
   ConnetOS# **set system inband enable** { **false** | **true** } 

#. 提交配置。

   ConnetOS# **commit**

