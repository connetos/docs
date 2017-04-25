安装ConnetOS
=======================================

简介
---------------------------------------
交换机在出厂时并不附带完整OS，而是仅预安装了ONIE（Open Network Install Environment）。ONIE在设备首次部署时运行，用于安装部署完整的ConnetOS。

ConnetOS安装完成后，设备启动后直接载入ConnetOS运行，ONIE不再运行。当然在需要时，仍然可以激活ONIE用于OS的升级、重装等安装部署操作。

.. note::
 如果设备没有预装ONIE，也可以通过安装在U盘的ONIE进行安装。

安装步骤
---------------------------------------

#. 查看设备盘::

    fdisk -l

#. 对设备盘进行分区::

    fdisk /dev/sda

#. 创建分区::

    1

    p +22G

    2 p

    2 t 82

#. 设置分区标签::

    mkfs.ext4 /dev/sda1 -L /;mkswap /dev/sda2 -L SWAP;e2label /dev/sda1;swaplabel /dev/sda2;

#. 挂载分区到目录，并拷贝bin文件到目录下，并进行解压::

    mount /dev/sda1 /mnt;cd /mnt;cp /ConnetOS_C1020_2.0.1_43D18.bin .;sed -i 1d ConnetOS_C1020_2.0.1_43D18.bin;

#. 设置设备时间，防止解压出错::

    date -s 20170101;tar zxf ConnetOS_C1020_2.0.1_43D18.bin;ls;

#. 安装引导，进行重启

    grub-install --boot-directory=/mnt/boot /dev/sda;rm -rf ConnetOS_C1020_2.0.1_43D18.bin;sync;reboot;

#. 重启成功，软件安装完成。

   软件安装之后，请继续进行配置文件的安装。

