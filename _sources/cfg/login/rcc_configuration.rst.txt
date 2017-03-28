RCC远程控制交换机
=======================================

RCC（Remote CLI Call）远程CLI调用，通过此功能，用户在本地就可以实现对交换机的远程配置。

RCC的使用极其简单，在本地编译之后，即可直接使用。

RCC有如下两种方式执行命令：

* 直接输入命令行。

  采用“-c”，输入命令行字符串，命令以“;“隔开。例如::
   
   [yunqi@host-a remote_cli_client]$./RCC -s 192.168.1.31 -u admin -p admin -c "configure;
   show vlans;exit;exit"


* 输入命令行文件名。
   
  将要执行的命令保存在文件中，以回车隔开。输入"-f 命令行文件名"，例如::
 
   [yunqi@host-a remote_cli_client]$./RCC -s 192.168.1.31 -u admin -p admin -f a.txt  

RCC可执行如下操作::
 
 [yunqi@host-a remote_cli_client]$ ./RCC
 Usage: RCC -s < device addr > -u < username> -p < password > [-c < command >] [-f < commands 
 file >] [-h]

            -s < device addr >            : device addr
            -u < username >               : the user name to login in
            -p < password >               : the password for the given user
            -c < commands >               : the command string containing multiple commands to be executed
            -f < commands file >          : the file name of the excecuting commands
            -h                            : usage (this message)

==============  ========================================
项目             含义
==============  ========================================
-s              需要远程控制的设备IP地址
-u              可登录的用户名
-p              用户密码
-c              命令行。以“;"隔开
-f              文件名。要执行的命令列表，在文件中以回车隔开。
==============  ========================================

操作举例::

 [yunqi@host-a remote_cli_client]$ ./RCC -s 192.168.1.31 -u admin -p admin -c "show version"
 Try to connect remote CLI 192.168.1.31:8080...
 Connected successfully.
 Doing user authentication...
 Sending username...
 From remote CLI: Begin to authenticate

 Sending password...
 From remote CLI: User authentication OK

 Sending command: show version
 ...
 From remote CLI:
 Copyright (C) 2015-2017 YUNQI TECH, Inc.
 PN             : C1020
 OS             : ConnetOS GENERAL
 Version ID     : 2.1.2
 Build Code     : r2146 (13V21)
 Switch MAC     : 00:03:0f:64:da:5f
 Management MAC : 00:03:0f:64:da:60
 Release Time   : 2017-03-21 11:41:52
 Operational mode CLI OK.
