初次登录设备
=======================================

登录方式简介
---------------------------------------
用户可以通过Console口、Telnet、SSH等方式登录交换机，但是当用户需要为第一次上电的设备进行配置时，必须使用Console口登录。

 * Console口进行本地登录是最基本的登录方式，也是配置其他登录方式的基础。
 * 用户通过SSH／Telnet远程登录到交换机上，对交换机进行远程管理和维护。

配置通过Console口登录
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
=======================================
ConnetOS系统的管理口为eth0。

配置管理口
---------------------------------------
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
---------------------------------------   
* 执行 **show interface management-ethernet eth0** 命令查看管理口的详细信息::

   ConnetOS> show interface management-ethernet eth0 
   eth0     Inet addr: 192.168.30.24/24， Gateway: 0.0.0.0， HW address: 08:9e:01:88:51:ba

* 执行 **show all interface management-ethernet eth0** 命令，查看管理口的配置信息::

   ConnetOS# show all interface management-ethernet eth0 
   Waiting for building configuration.
       dhcp {
           enable: false
       }
       address: "192.168.30.24/24"
       gateway: 0.0.0.0

用户登录权限配置
=======================================

配置登录访问控制
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 配置允许登录设备的网段。
  
   ConnetOS# **set system login-acl network** *network-ip-address*

   缺省情况下，允许所有的网段登录设备。

#. 提交配置。

   ConnetOS# **commit**

带内访问配置
=======================================
ConnetOS系统除了支持从管理口登录外，还支持从三层接口进行登录，使用三层接口的IP地址当作管理口IP使用。

该功能在ConnetOS系统下缺省是开启的。

配置带内访问
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 配置带内访问功能是否开启。
   
   ConnetOS# **set system inband enable** { **false** | **true** } 

#. 提交配置。

   ConnetOS# **commit**

帐号管理
=======================================

账号介绍
---------------------------------------
用户在Linux shell和CLI shell下都可以创建账户，账户类型分别为：
 
 * Linux shell账户：

   * 特权账户：在设备上可以进行任何操作。缺省账户：root。
   * 非特权账户：只具有查看权限。缺省账户：admin。
 
 * CLI shell账户：

   * read-only：只能对设备进行查询操作。
   * super-user：可以对设备进行查询和配置操作。缺省账户：root、admin。

如果想要Linux shell下创建的账号也能够正常使用CLI，有两种方式：

 * 手工配置：首先将Linux shell下的账号加入connetos组，其次根据想赋予的权限，决定是否将账号加入xorp组（加入xorp具有super-user权限）。
 * 自动配置：直接在CLI shell下对账号进行权限设置。

通常不建议直接在Linux shell下单独创建账号，可以使用CLI的账号功能进行账号的管理。

配置local账户
---------------------------------------
ConnetOS的local账户要可用，必须同时满足如下两个条件：
 
 * local账号启用。
 * AAA可用，或开启了AAA但AAA服务器不可达。

在local账号启用的情况下，如果配置了AAA且可用，local账号会自动禁用，如果AAA失效，那local账号会自动恢复为可用。

#. 进入配置模式。

   ConnetOS> **configure**

#. 配置是否禁用local帐号。

   ConnetOS# **set system aaa local enable** { **false** | **true** }

   缺省情况下，local帐号是开启的。

#. 创建local账户。

   ConnetOS# **set system login user** *user-name* **authentication plain-text-password** *plain-text-password*

   缺省情况下，创建local账户时，账户类型是super-user。

#. 设置账户类型

   ConnetOS# **set system login user** *user-name* **class** { **read-only** | **super-user** }

#. 提交配置。

   ConnetOS# **commit**

CLI登录交换机
=======================================

通过Console口登录
---------------------------------------
直接用Console口通信线缆连接，进行登录。

通过SSH登录
---------------------------------------
SSH（Secure Shell）安全外壳，是一个网络安全协议，标准协议端口号22。当用户通过一个不能保证安全的网络环境远程登录到交换机时，SSH通过对网络数据的的加密和认证，保证交换机不受IP地址欺骗、明文密码截取等恶意攻击。

用户通过SSH登录到交换机上，对交换机进行远程管理和维护。

#. 进入配置模式。

   ConnetOS> **configure**

#. （可选）使能SSH服务功能。
 
   ConnetOS# set system services ssh enable { false | true }
    
   缺省情况下，SSH服务功能是开启的。

#. （可选）配置允许SSH登录的最大连接数。
   
   ConnetOS# set system services ssh connection-limit limit-number
    
   缺省情况下，允许SSH登录的最大连接数是15。

#. 提交配置。

   ConnetOS# **commit**

通过Telnet登录
---------------------------------------
#. 进入配置模式。
   
   ConnetOS> **configure**

#. （可选）使能Telnet服务功能。

   ConnetOS# **set system services telnet enable** { **false** | **true** }
   
   缺省情况下，Telnet服务功能是开启的。

#. （可选）配置Telnet登录的最大连接数。

   ConnetOS# **set system services telnet connection-limit** *limit-number*

   缺省情况下，允许Telnet登录的最大连接数是15。

#. 提交配置

   ConnetOS# **commit**

NMS登录设备
=======================================
ConnetOS支持用户通过NMS（Network Management Station，网管工作站）登录到交换机，对交换机进行配置、管理。

如果要使用NMS登录设备，需要先在设备上配置好SNMP功能。配置完成后，即可通过登录。

SNMP概述
---------------------------------------
SNMP（Simple Network Management Protocol）简单网络管理协议，是网络中管理设备和被管理设备之间的通信规则，它定义了一系列消息、方法和语法，用于实现管理设备对被管理设备的访问和管理。

SNMP具有以下优势：

 * 自动化网络管理。
   网络管理员可以利用SNMP平台在网络上的节点检索信息、修改信息、发现故障、完成故障诊断、进行容量规划和生成报告。
 * 屏蔽不同设备的物理差异，实现对不同厂商产品的自动化管理。
   SNMP只提供最基本的功能集，使得管理任务分别与被管设备的物理特性和下层的联网技术相对独立，从而实现对不同厂商设备的管理，特别适合在小型、快速和低成本的环境中使用。

配置SNMP
---------------------------------------
#. 进入配置模式。
   
   ConnetOS> **configure**

#. 启动SNMP功能。
 
   ConnetOS# **set protocols snmp community** *community-info* [ **authorization read-only** | **clients** *ip-address* ]

   缺省情况下，SNMP功能是关闭的。

#. 配置SNMP访问控制
 
   ConnetOS# **set system snmp-acl network** *ip-address*

   缺省情况下，允许所有网段查询。

#. 提交配置

   ConnetOS# **commit**

配置AAA
=======================================

AAA介绍
---------------------------------------
AAA是Authentication（认证）、Authorization（授权）和Accounting（计费）的简称它提供对用户进行认证、授权和计费三种安全功能：

 * 认证（Authentication）：验证用户是否可以获得访问权，确定哪些用户可以访问网络。
 * 授权（Authorization）：授权用户可以使用哪些服务。
 * 计费（Accounting）：记录用户使用网络资源的情况。

ConnetOS支持完整的认证、授权和计费功能。

配置TACACS方式进行认证、授权和计费
---------------------------------------
#. 进入配置模式。
  
   ConnetOS> **configure**

#. 指定TACACS服务器的地址。

   ConnetOS# **set system aaa tacacs-plus host server-ip** *ip-address*

#. 使能TACACS功能

   ConnetOS# **set system aaa tacacs-plus enable** { **false** | **true** }

   缺省情况下，TACACS功能没有使能。使能后，TACACS功能直接生效。

#. （可选）配置TACACS服务器共享密钥

   ConnetOS# **set system aaa tacacs-plus key** *shared-key*
   
   缺省情况下，TACACS服务器的共享密钥是keystring。

#. （可选）配置TACACS的认证类型

   ConnetOS# **set system aaa tacacs-plus auth-type** { **ascii** | **chap** | **pap** }
 
   缺省情况下，TACACS的认证类型是ASCII。

#. （可选）使能TACACS授权功能

   ConnetOS# **set system aaa tacacs-plus authorization enable** { **false** | **true** }
 
   缺省情况下，TACACS授权功能是使能的。

#. （可选）使能TACACS计费功能

   ConnetOS# **set system aaa tacacs-plus accounting enable** { **false** | **true** }

   缺省情况下，TACACS计费功能是使能的。

#. 提交配置。
  
   ConnetOS# **commit**
