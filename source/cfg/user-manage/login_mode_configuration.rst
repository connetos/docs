配置用户登录方式
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
