系统升级
=======================================

系统升级
---------------------------------------
系统升级的步骤如下：

 #. 将image拷贝到/var/upgrade目录下。
 #. 重启设备，系统将自动完成升级::
 
     ConnetOS> request system reboot

.. Caution::
 * 执行 **request system reboot** 时，需要输入yes进行确认。
 * 升级image时，不会覆盖原有配置文件。

配置文件升级
---------------------------------------
配置文件升级主要指通过tftp方式将配置文件下载到交换机加载生效。

升级的步骤如下：
 
 #. tftp下载配置文件::

     ConnetOS> file tftp get remote-file xxx local-file connetos.boot ip-address 192.168.2.2

 #. 重启系统
 
 #. 启动后，配置文件自动加载::

     ConnetOS> request system reboot

.. Caution::
 * 上述升级命令中xxx为待升级的配置文件。
 * 上述升级命令中local-file的名字必须为connetos.boot。
 * 执行request system reboot时，需要输入yes进行确认。
 * 配置文件升级时，原有配置文件会被覆盖。

