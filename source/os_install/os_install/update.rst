升级
=======================================
ConnetOS是基于Debian GNU/Linux的操作系统，ConnetOS的升级分为linux升级和switch升级两部分。

云启提供如下的文件，以供升级：

* linux：connetos_*.bin，如connetos_c1020_2.1.5-30k17_amd64.bin。
* switch OS：switch_*.deb，如switch_c1020_2.1.5-30z19_amd64.deb。

switch可以单独升级，但是linux必须和switch一起升级。

.. note::
   * 执行 **request system reboot** 时，需要输入“yes“进行确认。
   * 升级时，不会覆盖原有配置文件。

如果升级失败，重启设备进行ConnetOS的安装即可。

升级linux和switch
-------------------------
以U盘升级方式为例，升级步骤如下：

#. 登录到交换机上::

    admin@ConnetOS:~$

#. 查看设备分区::

    admin@ConnetOS:~$ fdisk –l

#. 将U盘挂载到mnt下::

    admin@ConnetOS:~$ sudo mount /dev/sdc4 /mnt

#. 查看bin文件是否成功挂载到mnt下:: 
  
    admin@ConnetOS:~$ cd /mnt/

    admin@ConnetOS:/mnt$ ls

    connetos_c1020_2.1.5-30k17_amd64.bin  IxNetwork_8.20_EA.exe  System Volume Information 

    connetos_c1020_2.1.5-30w18_amd64.bin  setup.exe


#. 将connetos_*.bin拷贝到/var/upgrade目录下，例如::
    
    admin@ConnetOS:/mnt$ cp connetos_c1020_2.1.5-30k17_amd64.bin /var/upgrade/
     
#. 重启设备，系统将自动完成升级。两种重启方式选择一种即可。

   * 在linux shell下执行::

      admin@ConnetOS $ sudo reboot
 
   * 在CLI shell下，执行::

      admin@ConnetOS $ cli

      ConnetOS> request system reboot

升级switch
-------------------------
switch升级的步骤如下：

#. 登录到交换机上::

    admin@ConnetOS:~$

#. 安装升级文件::

    admin@ConnetOS:~$ sudo dpkg -i switch_c1020_2.1.5-30z19_amd64.deb

#. 重启设备，系统将自动完成升级。两种重启方式选择一种即可。

   * 在linux shell下执行::

      admin@ConnetOS $ sudo reboot
 
   * 在CLI shell下，执行::

      ConnetOS> request system reboot
