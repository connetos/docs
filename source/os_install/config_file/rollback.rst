配置文件回退
=======================================

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

