升级
=======================================
ConnetOS是基于Debian GNU/Linux的操作系统，ConnetOS的升级分为linux升级和switch升级两部分。

云启提供如下的文件，以供升级：

* linux：connetos_*.bin，如connetos_c1020_2.1.5-30k17_amd64.bin。
* switch OS：switch_*.tgz

switch可以单独升级，但是linux必须和switch一起升级。

.. note::
   * 执行 **request system reboot** 时，需要输入“yes“进行确认。
   * 升级时，不会覆盖原有配置文件。

如果升级失败，重启设备进行ConnetOS的安装即可。

升级switch
-------------------------
switch升级的步骤如下：

 #. 安装升级文件::

     dpkg -i switch_*.tgz

 #. 重启设备，系统将自动完成升级。两种重启方式选择一种即可。

    * 在linux shell下执行::

       admin@ConnetOS $ sudo reboot
 
    * 在CLI shell下，执行::

       ConnetOS> request system reboot

升级linux和switch
-------------------------
升级步骤如下：

 #. 将connetos_*.bin拷贝到/var/upgrade目录下，解压缩。
 #. 安装switch升级文件::

     dpkg -i switch_*.tgz
     
 #. 重启设备，系统将自动完成升级。两种重启方式选择一种即可。

    * 在linux shell下执行::

       admin@ConnetOS $ sudo reboot
 
    * 在CLI shell下，执行::

       ConnetOS> request system reboot
