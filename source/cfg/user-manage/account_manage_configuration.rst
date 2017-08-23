用户账户管理
=======================================

用户账号介绍
---------------------------------------
用户在Linux shell和CLI shell下都可以创建账户，账户类型分别为：
 
 * Linux shell账户：

   * 特权账户：在设备上可以进行任何操作。缺省账户：root。
   * 非特权账户：具有有限的操作权限。缺省并没有创建此类账户，用户可以根据需要自行创建。
 
 * CLI shell账户：

   * read-only：只能对设备进行查询操作。
   * super-user：可以对设备进行查询和配置操作。缺省可使用账号root。

如果想要Linux shell下创建的账号也能够正常使用CLI，有两种方式：

 * 手工配置：首先在Linux shell下创建账号，其次根据想赋予的权限，决定是否将账号加入xorp组（加入xorp具有super-user权限）。
 * 自动配置：直接在CLI shell下对账号进行权限设置。

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

配置用户登录权限
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 配置允许登录设备的网段。
  
   ConnetOS# **set system login-acl network** *network-ip-address*

   缺省情况下，允许所有的网段登录设备。

#. 提交配置。

   ConnetOS# **commit**




