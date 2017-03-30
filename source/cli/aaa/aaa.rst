AAA命令
=============================
set system aaa local enable
-------------------------------------------

命令功能
+++++++++++++++
**set system aaa local enable** 命令用来配置是否使能本地认证功能。

**delete system aaa local enable** 命令用来删除本地认证功能。

缺省情况下，本地认证功能能没有使能。

命令格式
+++++++++++++++
**set system aaa local enable** { **false** | **true** }

**delete system aaa local enable**

参数说明
+++++++++++++++
**false**：不使能本地认证功能。

**true**：使能本地认证功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 使能本地认证功能::

 ConnetOS# set system aaa local enable true

set system aaa tacacs-plus accounting enable
-----------------------------------------------

命令功能
+++++++++++++++
**set system aaa tacacs-plus accounting enable** 命令用来配置是否使能TACACS+计费功能。

**delete system aaa tacacs-plus accounting enable** 命令用来删除TACACS＋计费功能使能。

缺省情况下，TACACS+计费功能并没有使能。

命令格式
+++++++++++++++
**set system aaa tacacs-plus accounting enable** { **false** | **true** }

**delete system aaa tacacs-plus accounting enable**

参数说明
+++++++++++++++
**false**：不使能TACACS＋计费功能。

**true**：使能TACACS＋计费功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能TACACS＋计费功能::

 ConnetOS# set system aaa tacacs-plus accounting enable true


set system aaa tacacs-plus auth-type
-------------------------------------------
 
命令功能
+++++++++++++++
**set system aaa tacacs-plus auth-type** 命令用来配置TACACS+的认证类型。

**delete system aaa tacacs-plus auth-type** 命令用来删除TACACS＋计费功能使能。

缺省情况下，TACACS+的认证类型是ASCII。

命令格式
+++++++++++++++
**set system aaa tacacs-plus auth-type** { **ascii** | **chap** | **pap** }

**delete system aaa tacacs-plus auth-type**

参数说明
+++++++++++++++
**ascii**：ASCII认证类型。

**chap**：CHAP认证类型。

**pap**：PAP认证类型。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 配置TACACS+的认证类型为CHAP::

 ConnetOS# set system aaa tacacs-plus auth-type chap

set system aaa tacacs-plus authorization enable
---------------------------------------------------

命令功能
+++++++++++++++
**set system aaa tacacs-plus authorization enable** 命令用来配置是否使能TACACS+授权功能。

**delete system aaa tacacs-plus authorization enable** 命令用来删除TACACS＋授权功能使能。

缺省情况下，TACACS+授权功能是使能的。

命令格式
+++++++++++++++
**set system aaa tacacs-plus authorization enable** { **false** | **true** }

**delete system aaa tacacs-plus authorization enable**

参数说明
+++++++++++++++
**false**：不使能TACACS＋授权功能。

**true**：使能TACACS＋授权功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能TACACS+授权功能::

 ConnetOS# set system aaa tacacs-plus authorization enable true

set system aaa tacacs-plus enable
-------------------------------------------

命令功能
+++++++++++++++
**set system aaa tacacs-plus enable** 命令用来配置是否使能TACACS+功能。

**delete system aaa tacacs-plus enable** 命令用来删除TACACS＋功能。

缺省情况下，TACACS+功能没有使能。

命令格式
+++++++++++++++
**set system aaa tacacs-plus accounting enable** { **false** | **true** }

**delete system aaa tacacs-plus accounting enable**

参数说明
+++++++++++++++
**false**：不使能TACACS＋功能。

**true**：使能TACACS＋功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
使能后，TACACS功能直接生效。

配置举例
+++++++++++++++
# 使能TACACS功能直接生效::

 ConnetOS# set system aaa tacacs-plus enable true

system aaa tacacs-plus host server-ip
-------------------------------------------

命令功能
+++++++++++++++
**set system aaa tacacs-plus host server-ip** 命令用来指定TACACS＋服务器。

**delete system aaa tacacs-plus host server-ip** 命令用来删除指定的TACACS＋服务器。

缺省情况下，并没有指定TACACS＋服务器。

命令格式
+++++++++++++++
**set system aaa tacacs-plus host server-ip** *ip-address*

**delete system aaa tacacs-plus host server-ip** *ip-address*

参数说明
+++++++++++++++
*ip-address*：TACACS＋服务器的IP地址。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
TACACS＋服务器可以指定多个。

配置举例
+++++++++++++++
# 指定IP地址为1.1.1.1的TACACS＋服务器作为本设备的TACACS＋服务器::

 ConnetOS# set system aaa tacacs-plus host server-ip 1.1.1.1

set system aaa tacacs-plus key
-------------------------------------------

命令功能
+++++++++++++++
**set system aaa tacacs-plus key** 命令用来配置是TACACS+服务器的共享密钥。

**delete system aaa tacacs-plus key** 命令用来删除TTACACS+服务器的共享密钥。

缺省情况下，TACACS+服务器没有共享密钥。

命令格式
+++++++++++++++
**set system aaa tacacs-plus key** *shared-key*

**delete system aaa tacacs-plus key**

参数说明
+++++++++++++++
*shared-key*：共享密钥。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
配置TACACS+服务器的共享密钥为test::

 ConnetOS# set system aaa tacacs-plus key test
