升级ConnetOS
=======================================

系统升级的步骤如下：

 #. 将image拷贝到/var/upgrade目录下。
 #. 重启设备，系统将自动完成升级::
 
     ConnetOS> request system reboot

.. Caution::
 * 执行 **request system reboot** 时，需要输入yes进行确认。
 * 升级image时，不会覆盖原有配置文件。

如果升级失败，重启设备进行ConnetOS的安装即可。