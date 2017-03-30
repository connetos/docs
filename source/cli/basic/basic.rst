基础命令
========================

cls
-------------------------------------------

命令功能
+++++++++++++++
**cls** 命令用来清除当前终端屏幕上显示的信息。

命令格式
+++++++++++++++
**cls**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式、配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 清除当前终端屏幕上的显示信息::

 ConnetOS# cls

commit
-------------------------------------------

命令功能
+++++++++++++++
**commit** 命令用来提交当前用户更改的配置，使配置生效。

缺省情况下，用户配置并不会自动提交。

命令格式
+++++++++++++++
**commit** [ **at** *active-time* | **comment** *comment* | **confirmed** *auto-confirm-time* ]

参数说明
+++++++++++++++
*active-time*：提交的配置开始生效的时间。

*comment*：增加对本次提交内容的描述记录。字符串形式，不支持空格。

*auto-confirm-time*：设置如果配置没有确认，自动回滚的时间。整数形式，取值范围是1～30000，单位是秒。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
配置模式下，修改配置的命令，只有 **commit** 之后才能真正生效。即：配置由候选配置变为活动配置。

配置举例
+++++++++++++++
# 提交当前配置::

 ConnetOS# set system hostname switcha
 ConnetOS# commit

configure
-------------------------------------------

命令功能
+++++++++++++++
**configure** 命令用来从运维模式进入配置模式提交当前用户配置，使配置生效。

缺省情况下，用户进入的命令行视图是运维模式。

命令格式
+++++++++++++++
**configure** [ **exclusive** ]

参数说明
+++++++++++++++
**exclusive**：锁定当前配置模式，不允许其他用户进入。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
如果设备当前有其他用户正在登录，不允许锁定当前配置模式。  

如果想解除配置模式的锁定，执行 **quit** 命令或 **exit** 命令退出当前配置模式即可。


配置举例
+++++++++++++++
# 进入配置模式::

 ConnetOS> configure
 Entering configuration mode.
 Users root and admin are also in configuration mode.
 ConnetOS#

discard
-------------------------------------------

命令功能
+++++++++++++++
**discard** 命令用来丢弃当前没有提交的配置。

命令格式
+++++++++++++++
**discard**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 丢弃当前未提交的配置::

 ConnetOS# discard

exit
-------------------------------------------

命令功能
+++++++++++++++
**exit** 命令用来退出当前模式。

命令格式
+++++++++++++++
**exit** [ **configuration-mode** | **discard** ]

参数说明
+++++++++++++++
**configuration-mode**：退出配置模式，返回运维模式。

**discard**：丢弃当前尚未 **commit** 的配置，并返回运维模式。

命令模式
+++++++++++++++
运维模式、配置模式

使用指南
+++++++++++++++
运维模式下，只能执行 **exit** 命令。

在edit视图下，执行 **exit configuration-mode** 或者 **exit discard** 命令，将直接返回到运维模式。


配置举例
+++++++++++++++
# 从配置模式，返回到运维模式::

 ConnetOS# exit
 Leave configuration mode.
 ConnetOS>

help
-------------------------------------------

命令功能
+++++++++++++++
运维模式下，**help** 命令用来介绍如何利用ConnetOS的help功能完成命令行的输入。  

配置模式下，**help** 命令用来介绍各类基本命令的功能。

命令格式
+++++++++++++++
**help** （运维模式）

**help** { **commit** | **delete** | **edit** | **exit** | **help** | **load** | **quit** | **rollback** | **run** | **save** | **set** | **show** | **status** | **top** | **up** }（配置模式）

参数说明
+++++++++++++++
**commit**：提交配置。

**delete**：删除配置。

**edit**：进入各级edit视图。

**exit**：从当前配置模式中退出。

**help**：命令行帮助信息。

**load**：从配置文件中加载配置信息。

**quit**：退出当前模式。

**rollback**：回退到上一次提交的配置。

**run**：执行运维模式下的命令。

**save**：把配置信息保存到文件中。

**set**：设置参数值或者创建新的配置项。

**show**：配置信息。

**status**：用户当前的配置信息。

**top**：退回到最上级配置视图。

**up**：退回到上一级配置视图。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 了解run命令的基本功能::

 ConnetOS# help run
 The "run" command allows operational-mode commands to be executed withoutleaving configuration-mode.  This is particularly important if there areuncommitted changes to the configuration.

 For example, the operational-mode command "show bgp peers" can be run from configuration-mode as "run show bgp peers".

 Navigation commands such as the operational-mode "configure" command are not available using the run command.

load
-------------------------------------------

命令功能
+++++++++++++++
**load** 命令用来加载指定配置文件中的配置。

命令格式
+++++++++++++++
**load** *local-file-name*

参数说明
+++++++++++++++
*local-file-name*：本地文件名。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 加载配置文件::

 ConnetOS# load /switch/config/connetos.conf.03
 Loading config: /switch/config/connetos.conf.03
 ConnetOS# Waiting for merging configuration.
 Load done.

quit
-------------------------------------------

命令功能
+++++++++++++++
**quit** 命令用来退出配置模式，回到运维模式。

命令格式
+++++++++++++++
**quit**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
如果当前有没有提交的配置，无法通过 **quit** 命令退出。可以先提交配置、或通过 **exit discard** 命令丢弃当前命令退出、或执行 **discard** 命令丢弃当前配置再执行 **quit** 命令退出。

配置举例
+++++++++++++++
# 退回到运维模式::

 ConnetOS# quit
 Leave configuration mode.
 ConnetOS>

rollback
-------------------------------------------

命令功能
+++++++++++++++
**rollback** 命令用来基于历史版本进行版本回退。

命令格式
+++++++++++++++
**rollback** *version-number*

参数说明
+++++++++++++++
*version-number*：回退版本数。整数形式，取值范围是1～49。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
如果在系统运行过程中发现配置错误、业务运行不正常或者配置对网络产生了超出预期的结果，用户可以通过rollback命令将系统回退到指定的版本。

历史活动配置的保存是按照倒序进行的，即序号1保存的是当前配置。

配置举例
+++++++++++++++
# 将版本回退到上一个版本::

 ConnetOS# rollback 1
 Rolling back to config: /switch/config/connetos.conf.01
 ConnetOS# Waiting for merging configuration.
 Load done.
 ConnetOS#

save
-------------------------------------------

命令功能
+++++++++++++++
**save local-file-name** 命令用来将当前配置文件保存到本地。

**save default-to-startup** 命令用来将缺省配置保存为启动配置。

**save running-to-startup** 命令用来将活动配置保存为启动配置。

命令格式
+++++++++++++++
**save** { *local-file-name* | **default-to-startup** | **running-to-startup** }

参数说明
+++++++++++++++
*loacal-file-name* ：本地文件名称。字符串形式，长度范围是1～63。支持区分大小写不支持空格。

**default-to-startup**：设置缺省配置为启动配置。

**running-to-startup**：设置当前的活动配置为启动配置。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 设置当前的活动配置为启动配置::

 ConnetOS# save running-to-startup
 Save done.

status
-------------------------------------------

命令功能
+++++++++++++++
**status** 命令用来查看当前进行配置操作的用户。

命令格式
+++++++++++++++
**status**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查看当前进行配置操作的用户::

 ConnetOS# status
 User root is also in configuration mode.

top
-------------------------------------------

命令功能
+++++++++++++++
**top** 命令用来退回到顶级视图，即配置视图下。

命令格式
+++++++++++++++
**top**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
**top** 命令是直接退回到顶级视图，如果需要逐步退回到上一级视图，执行命令 **quit**、**exit**、**up** 即可。

配置举例
+++++++++++++++
# 从ospf4视图退回到配置模式::

 ConnetOS# edit protocols ospf4
 [edit protocols ospf4]
 ConnetOS# top
 ConnetOS#

up
-------------------------------------------

命令功能
+++++++++++++++
**up** 命令用来逐步退出配置模式下的各类edit视图。

命令格式
+++++++++++++++
**up**

参数说明
+++++++++++++++
**up** 命令是逐步退出各级edit视图，如果想要直接退回到顶级视图，执行 **top** 命令。

**up** 命令只能逐步退出视图，不能退出模式。**quit** 命令、**exit** 命令既可以退出视图，又可以退出模式。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 从ospf4视图退回到配置模式::

 ConnetOS# edit protocols ospf4
 [edit protocols ospf4]
 ConnetOS# up
 [edit protocols]
 ConnetOS# up

