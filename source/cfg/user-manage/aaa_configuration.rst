配置用户认证方式
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
