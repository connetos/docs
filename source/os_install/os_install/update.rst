ConnetOS升级
=======================================
ConnetOS是基于Debian GNU/Linux的操作系统，所以ConnetOS的升级分为linux升级和 switch OS升级两部分。

云启提供如下的文件，以供升级：

* linux：xxxxx.bin
* switch OS：xxxxx.deb、xxxxxx.tgz

switch OS可以单独升级，但是linux升级时必须和switch OS一起升级。

.. note::
   * 执行 **request system reboot** 时，需要输入yes进行确认。
   * 升级时，不会覆盖原有配置文件。

如果升级失败，重启设备进行ConnetOS的安装即可。

升级switch OS
-------------------------
switch OS升级的步骤如下：

 #. 安装升级文件，如下方式选择一种即可。

    * 将xxxxx.tgz文件拷贝到/var/upgrade目录下，直接解压缩。

    * 使用”dpkg -i xxxxx.deb“命令将xxxxx.deb安装到/var/upgrade目录下

 #. 重启设备，系统将自动完成升级。两种重启方式选择一种即可。

    * 在linux shell下执行::

       admin@ConnetOS $ sudo reboot
 
    * 在CLI shell下，执行::

       ConnetOS> request system reboot

升级linux和 switch OS
-------------------------
升级步骤如下：

 #. 将xxxxx.bin拷贝到/var/upgrade目录下，解压缩。
 #. 将xxxxx.tgz文件拷贝到/var/upgrade目录下解压缩，或将xxxxx.deb安装到/var/upgrade目录下。
 #. 重启设备，系统将自动完成升级。两种重启方式选择一种即可。

    * 在linux shell下执行::

       admin@ConnetOS $ sudo reboot
 
    * 在CLI shell下，执行::

       ConnetOS> request system reboot
