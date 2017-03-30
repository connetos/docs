登录命令
========================

set system services ssh enable
-------------------------------------------

命令功能
+++++++++++++++
**set system services ssh enable** 命令用来配置是否使能SSH功能。

**delete system services ssh enable** 命令用来删除配置的SSH功能。

缺省情况下，SSH功能是使能的。

命令格式
+++++++++++++++
**set system services ssh enable** { **false** | **true** }

**delete system services ssh enable**

参数说明
+++++++++++++++
**false**：不使能SSH功能。

**true**：使能SSH功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能SSH功能::

 ConnetOS# set system services ssh enable true 

set system services ssh connection-limit
-------------------------------------------

命令功能
+++++++++++++++
**set system services ssh connection-limit** 命令用来配置允许通过SSH方式登录的用户数。

**delete system services ssh connection-limit** 命令用来删除配置的SSH登录用户数。

缺省情况下，允许15个用户通过SSH方式登录设备。

命令格式
+++++++++++++++
**set system services ssh connection-limit** *limit-number*

**delete system services ssh connection-limit**

参数说明
+++++++++++++++
*limit-number*：可以登录的用户数目。整数形式，取值范围是1～250。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 设置可以通过SSH方式登录设备的用户数是25::

 ConnetOS# set system services ssh connection-limit 25

set system services telnet enable
-------------------------------------------

命令功能
+++++++++++++++
**set system services telnet enable** 命令用来配置是否使能Telnet功能。

**delete system services telnet enable** 命令用来删除配置的Telnet功能。

缺省情况下，Telnet没有使能。

命令格式
+++++++++++++++
**set system services telnet enable** { **false** | **true** }

**delete system services telnet enable**

参数说明
+++++++++++++++
**false**：不使能Telnet功能。

**true**：使能Telnet功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能Telnet功能::

 ConnetOS# set system services telnet enable true

set system services telnet connection-limit
-------------------------------------------------

命令功能
+++++++++++++++
**set system services telnet connection-limit** 命令用来配置允许通过Telnet方式登录的用户数。

**delete system services telnet connection-limit** 命令用来删除配置的Telnet登录用户数。

缺省情况下，允许15个用户通过Telnet方式登录设备。

命令格式
+++++++++++++++
**set system services telnet connection-limit** *limit-number*

**delete system services telnet connection-limit**

参数说明
+++++++++++++++

*limit-number*：可以通过Telnet登录的用户数目。整数形式，取值范围是1～250。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 设置可以通过Telnet方式登录设备的用户数是25::

 ConnetOS# set system services telnet connection-limit 25

set system inband enable
-------------------------------------------

命令功能
+++++++++++++++
**set system inband enable** 命令用来配置是否使能带内访问功能。

**delete system inband enable** 命令用来删除配置的带内访问功能，恢复为缺省值。

缺省情况下，带内访问功能是开启的。

命令格式
+++++++++++++++
**set system inband enable** { **false** | **true** }

**delete system inband enable**

参数说明
+++++++++++++++
**false**：不使能带内访问功能.

**true**：使能带内访问功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能带内访问功能::

 ConnetOS# set system inband enable true

set system login announcement
-------------------------------------------

命令功能
+++++++++++++++
**set system login announcement** 命令用来设置用户登录设备时的通知信息。

**delete system login announcement** 命令用来删除配置的通知信息。

缺省情况下，用户登录设备时的通知信息为ConnetOS。

命令格式
+++++++++++++++
**set system login announcement** *announcement-message*

**delete system login announcement**

参数说明
+++++++++++++++
*announcement-message*：通知信息。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 设置用户登录设备时的通知信息为Hello::

 ConnetOS# set system login announcement Hello

set system login user authentication
-------------------------------------------

命令功能
+++++++++++++++
**set system login user authentication** 命令用来创建用户账户。

**delete system login user authentication** 命令用来删除配置的用户账户。

命令格式
+++++++++++++++
**set system login user** *user-name* **authentication plain-text-password** *plain-password*

**delete system login user** *user-name* **authentication** [ *plain-text-password* ]

参数说明
+++++++++++++++
*user-name*：用户名。

*plain-password*：用户密码

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 创建用户名为usera，密码为test的用户账户::

 ConnetOS# set system login user usera authentication plain-text-password test

set system login user class
-------------------------------------------

命令功能
+++++++++++++++
**set system login user user-name class** 命令用来配置账户类型。

**delete system login user authentication** 命令用来删除配置的账户类型，恢复为缺省值。

缺省情况下，用户账户创建后，账户类型为 **super-user**。

命令格式
+++++++++++++++
**set system login user** *user-name* **class** { **read-only** | **super-user** }

**delete system login user** *user-name* **class** 

参数说明
+++++++++++++++
**read-only**：只能对设备进行查询操作。

**super-user**：可以对设备进行查询和配置操作。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 设置用户usera的账户类型为read-only::

 ConnetOS# set system login user usera class read-only

set system login-acl network
-------------------------------------------

命令功能
+++++++++++++++
**set system login-acl network** 命令用来配置允许登录设备的网段。

**delete system login-acl network** 命令用来删除配置的允许登录网段。

缺省情况下，允许所有网段登录。

命令格式
+++++++++++++++
**set system login-acl network** *acl-network*

**delete system login-acl network**

参数说明
+++++++++++++++
*acl-network*：允许登录的网段。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 设置只允许1.1.1.0/24网段的用户登录::

 ConnetOS# set system login-acl network 1.1.1.0/24

