概述
=======================================

Shell视图简介
---------------------------------------
ConnetOS系统（以下简称为ConnetOS）为用户提供两个shell视图：

 * Linux shell：Linux界面视图，用户初始登录的视图，亦即Debian Linux系统的缺省shell环境。
 * CLI shell：命令行接口（Command-line Interface）视图，用于对交换机的网络操作和管理。

用户登录到设备后，输入账户和密码，进入到Linux shell，输入cli，即可进入CLI shell::

 ConnetOS login: admin
 Password:
 Last login: Wed Mar 15 16:55:27 CST 2017 from 192.168.1.132 on pts/0
 Linux ConnetOS 3.16.7-ckt25+ #1 SMP Thu Mar 2 10:28:57 CST 2017 x86_64

 The programs included with the Debian GNU/Linux system are free software;
 the exact distribution terms for each program are described in the
 individual files in /usr/share/doc/*/copyright.

 Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
 permitted by applicable law.
     ______                            __   ____  _____
    / ____/____   ____   ____   ___   / /_ / __ \/ ___/
   / /    / __ \ / __ \ / __ \ / _ \ / __// / / /\__ \
  / /___ / /_/ // / / // / / //  __// /_ / /_/ /___/ /
  \____/ \____//_/ /_//_/ /_/ \___/ \__/ \____//____/
 
 admin@ConnetOS:~$ cli
 Welcome to switch CLI shell.
 ConnetOS>

命令行视图特点
---------------------------------------
ConnetOS CLI的命令行有如下特点：

 * 简洁的命令行模式
   视图只有运维模式（operational mode）和配置模式（configuration mode）两种，命令行操作过程中避免频繁的视图跳转。
 * 逻辑清晰的树形结构
   命令行按照操作类型，划分为show、set、delete等种类，作为根节点；各类功能（如OSPF、LLDP）作为下一层节点，此功能的相关配置都在此节点下。

在使用命令行时，请注意：

 * ConnetOS CLI只有在输入完整命令行时，才能执行命令。
 * 命令自动补齐时，如果符合条件的命令行不唯一，会出现无法自动补齐的情况。您可以输入“？”或按Tab查看，手动进行选择、输入。

命令模式
=======================================

运维模式
---------------------------------------
登录ConnetOS CLI后会自动进入运维模式，运维模式用于管理和监控设备操作。例如：查看配置信息、查看设备状态、设置系统时间。

运维模式的命令提示符为“>”::
 
 ConnetOS>

.. note::
   运维模式下的操作，不需要commit，执行后立即生效。

配置模式
---------------------------------------
配置模式用于对设备进行各项配置，例如：管理用户、控制设备访问权限、配置各类协议、配置设备安全功能、设置系统硬件属性。

配置模式的命令提示符为“#”，例如::
 
 ConnetOS#

.. note::
 * 运维模式下的命令前输入关键字 **run**，即可在配置模式下执行（不包括在运维模式和配置模式下都可以执行的命令）。例如::

    ConnetOS#run ping 192.168.1.1
 * 配置模式下的任何配置（**set** 或 **delete**）操作，必须执行 **commit** 才会生效。而运维模式下的set操作执行后立即生效。

模式切换
---------------------------------------

进入配置模式
+++++++++++++++++++++++++++++++++++++++
在运维模式下执行 **configure** 命令，进入配置模式。例如::

 ConnetOS> configure 
 Entering configuration mode.
 There are no other users in configuration mode.
 ConnetOS#

如果用户只希望自己在设备上进行配置，可以通过执行 **congfigure exclusive** 命令，将配置模式锁定，避免其他用户的配置干扰。例如::

 ConnetOS> configure exclusive 
 Entering configuration mode.
 There are no other users in configuration mode.
 ConnetOS#

.. note::
 * 如果设备当前有其他用户正在登录，不允许锁定当前配置模式。例如::

   ConnetOS> configure exclusive 
   ERROR: Exclusive config mode requested， but there are already other configuration mode users: admin.
   ConnetOS>

 * 如果要解除锁定，直接退出配置模式即可。

退出配置模式
+++++++++++++++++++++++++++++++++++++++
从配置模式退回到运维模式，可以执行 **exit** 命令或 **quit** 命令。例如::

 ConnetOS# exit
 ConnetOS>

或::

 ConnetOS# quit
 ConnetOS>

从配置模式退回运维模式时，如果想丢弃当前尚未 **commit** 的配置，有两种方式:

* 执行 **exit** 命令时，使用 **discard** 参数::

   ConnetOS# exit discard  
   ConnetOS>

* 直接执行 **discard** 命令，再执行 **exit** 命令或 **quit** 命令退出::

   ConnetOS# discard
   ConnetOS# exit
   Leave configuration mode.
   ConnetOS>

.. note::
 如果有配置尚未commit，使用 **exit** 命令是无法退出的。

配置方式介绍
=======================================

配置类型介绍
---------------------------------------
ConnetOS中一共包含如下4种配置：

 * 缺省配置：ConnetOS首次启动时的默认配置；
 * 候选配置：ConnetOS系统只进行了配置，尚未提交的配置；候选配置没有提交前，使用show命令查看，会有“＋”的提示。
 * 活动配置：候选配置进行提交，系统检查验证通过后，候选配置会转为活动配置。
 * 启动配置：ConnetOS系统下次重启时加载的配置。ConnetOS支持对当前的活动配置进行保存。

配置转换介绍
---------------------------------------
设备上电后：
 #. 首先加载缺省配置，再比较启动配置和缺省配置的区别，如果检查无误后，将有差异的配置进行加载。
 #. 如果用户对配置进行了修改，配置其实并没有立即生效，而是作为候选配置存在于设备上。
 #.  当用户对修改内容执行commit命令，ConnetOS系统将验证用户修改的内容，验证通过后，候选配置变为活动配置。
 #. 如果用户想下次设备启动时采用当前配置，可以将当前配置保存为启动配置。

候选配置转变为活动配置的过程如下图所示。
 
选配置转变为活动配置过程

.. image:: active_config.png

保存启动配置
---------------------------------------
如果要将当前活动配置保存为启动配置，可以使用 **save running-to-startup** 命令保存。当ConnetOS系统重启后，将恢复到重启前的活动配置。

配置回滚
---------------------------------------
ConnetOS可以基于历史活动配置，通过执行命令 **rollback version-number** 进行回滚操作。ConnetOS最多可以保持49个历史配置，因此可以实现最多49级回滚。

历史活动配置的保存是按照倒序进行的，即序号1保存的是当前配置。

 * 用户执行 **rollback 1** 命令可以恢复到上一个活动配置。
 * 当用户没有保存当前配置而设备重启时，使用 **rollback 1** 命令可以恢复到重启前的配置::

    ConnetOS# rollback 1 
    Rolling back to config: /switch/config/connetos.conf.01
    ConnetOS# Waiting for merging configuration.
    Load done.

.. note::
 rollback后使用“？”命令可以列出所有的历史存档配置。

配置删除
---------------------------------------
在ConnetOS中，通过执行 **delete** 命令删除配置或将配置恢复到默认值。例如：

当前系统的hostname为test，删除系统的hostname，使其恢复为缺省的ConnetOS::

 test# delete system hostname 
 Deleting: 
     hostname: "test"
 OK 
 test# commit 
 Waiting for merging configuration.
 Commit OK.
 ConnetOS#

.. note::
 如果要恢复成出厂空配置，可以先后执行 **save default-to-startup** 命令和 **request system reboot** 命令。

配置查询
=======================================

使用命令行查询配置结果
---------------------------------------
采用 **show** 命令查看设备上的配置结果。例如查看service节点的配置情况::

 ConnetOS# show system services
 Waiting for building configuration.
     telnet {
         connection-limit: 15
         enable: true
     }
     ssh {
         connection-limit: 15
         enable: true
     }

过滤显示信息
---------------------------------------
ConnetOS CLI支持管道符“|”来过滤显示信息，并支持多级管道。

管道符“|”用来过滤命令行显示信息，帮助用户快速找到所需要的信息。管道符左边的命令输出将作为管道符右边的命令或文件的输入内容。 

可以通过“？”或Tab键查询当前管道支持的参数，例如::

 ConnetOS# show protocols | ?
 Possible completions:
   count                         Count occurrences
   except                        Show only text that does not match a pattern
   find                          Search for the first occurrence of a pattern
   hold                          Hold text without exiting the --More-- prompt
   match                         Show only text that matches a pattern
   no-more                       Don't paginate output

more提示信息
---------------------------------------
ConnetOS CLI下执行 **show** 命令输出的结果超过一屏时，命令行界面有提示“--More--”。
在“--More--”提示符后：

 * 输入空格，可以自动下翻一屏。
 * 输入回车，可以自动下翻一行。
 * 输入“h”，查看显示选项列表。

例如，**show interface brief** 命令显示信息的“--More--”后输入h，可以看到如下选项列表::
 
                    SUMMARY OF MORE COMMANDS

     -- Get Help --
   h                 *  Display this help.

     -- Scroll Down --
   Enter   Return  j   *  Scroll down one line.
   ^M  ^N  DownArrow
   Tab d   ^D  ^X    *  Scroll down one-half screen.
   Space   ^F          *  Scroll down one whole screen.
   ^E  G             *  Scroll down to the bottom of the output.
   N                 *  Display the output all at once instead of one
                        screen at a time. (Same as specifying the
                        | no-more command.)

     -- Scroll Up --
   k   ^H  ^P        *  Display the previous line of output.
   UpArrow
   u   ^U            *  Scroll up one-half screen.
   b   ^B            *  Scroll up one whole screen.
   ^A  g             *  Scroll up to the top of the output.

     -- Misc Commands --
   ^L                *  Redraw the output on the screen.
  --More--

快捷键
=======================================
在使用命令行接口时，ConnetOS CLI提供了许多快捷键，用于快速输入命令行，简化操作。

ConnetOS CLI下支持的快捷方式有：

==============================   ==============================
内容                              快捷方式
==============================   ==============================
转到下一条命令记录                  Down arrow或Ctrl + n
转到上一条命令记录                  Up arrow或Ctrl + p
转到行首                           Ctrl + a
转到行尾                           Ctrl + e
向左移动一个字符                    Ctrl + b
向右移动一个字符                    Ctrl + f
向前移动一个字                      Esc + f
向后移动一个字                      Esc + b
删除光标位置上的字符                 Ctrl + d
删除光标后的字                      Esc + d
删除光标前面的字                    Esc + backspace
删除从光标开始至行尾的文本            Ctrl + k
删除行                             Ctrl + u
将删除的文本粘贴到光标处             Ctrl + y
==============================   ==============================

获取帮助
=======================================

命令行自动补齐功能
---------------------------------------
在设备上进行命令行操作时，必须输入完整的命令行，否则命令行不能执行。

ConnetOS提供命令行自动补齐功能，输入命令时，只需要输入前几位字符，按空格或Tab键，系统会自动进行命令行的补齐。

 * 空格键用于补齐大部分CLI命令。
 * Tab键既可以用于补齐CLI命令，还可以用于补齐用户自定义的变量，例如ACL的名字，IP地址等。

当待补齐的命令或参数意义模糊时，请在列表中选择可能的补齐内容。例如::
 
 ConnetOS> show v?
 Possible completions:
   version                       Display system version
   vlan-interface                Show vlan interface information
   vlans                         Show vlan information

系统预设帮助
---------------------------------------
ConnetOS提供了命令功能解释，在CLI上输入“help ？”及具体命令，可以查看命令功能的详细说明。

ConnetOS CLI提供了两种方式的命令行帮助：

 * 完整帮助
   直接输入“？” ，查看当前模式支持的命令及命令的完整格式。
 * 部分帮助
   输入命令行的部分字符或输入部分命令行，通过不断的“？”获取完整的命令行及命令行释义。

命令行错误信息提示
---------------------------------------
ConnetOS CLI在命令行输入时会逐字检查语法。当在CLI中输入一个字符串并按下空格键时，如果输入的内容不是命令的有效组成部分，CLI会进行信息提示，同时命令行将无法执行。

常见的提示错误的信息有：

======================================================    ==============================
常见提示信息                                                错误原因
======================================================    ==============================
syntax error， command "ci" is not recognized.             输入错误的命令，按“？”寻求帮助。
unknown command.                                           输入错误的命令，按“Tab”进行命令行补全。
ERROR: path "interface traceoptions fo" is not valid.      输入错误的命令，直接执行。
ERROR: There are uncommitted changes.                      退出配置模式时，有未提交的配置。
======================================================    ==============================

常用命令行介绍
=======================================

配置命令关键字
---------------------------------------

set
+++++++++++++++++++++++++++++++++++++++
**set** 命令用来进行各项功能的配置。

配置模式下，修改配置后必须commit，修改才能生效。

运维模式下，**set** 命令直接生效。

delete
+++++++++++++++++++++++++++++++++++++++
**delete** 命令用来删除各类配置。如果要将当前的活动配置全部删除，即清空所有配置恢复成出厂空配置，可以使用 **save default-to-startup** 命令并执行 **request system reboot** 命令进行系统重启。

注意：**delete** 命令会删除配置节点，相关命令下会不显示此功能配置项，需要set后才能显示。

edit
+++++++++++++++++++++++++++++++++++++++
**edit** 命令用来进入不同层级的视图，只显示本功能相关的命令，同时简化命令行。如果要退出各类edit视图，执行 **top**、**up**、**quit**、**exit** 等命令即可。

运维命令关键字
---------------------------------------

show
+++++++++++++++++++++++++++++++++++++++
**show** 命令用来查看设备上的各种配置，输入show后，键入“？”，可以方便地查阅各类设备信息。同时可以运用管道符“｜”的过滤功能，进行查看。在显示信息过多，想要中断显示信息的输出时，可以通过输入“q”退回到配置模式。

clear
+++++++++++++++++++++++++++++++++++++++
**clear** 命令用来清除各项统计信息。

run
+++++++++++++++++++++++++++++++++++++++
运维模式下的命令，增加 **run** 前缀可以用在配置模式下。

.. note::
 在运维模式和配置模式下都能执行的命令，不支持运行**run**命令。


