配置设备的基本信息
=======================================

#. 进入配置模式。

   ConnetOS> **configure**

#. 设置设备设备名称。

    * 单机模式：**set system hostname** *hostname*
    * 堆叠模式：**set iss member** *member-id* **hostname** *hostname*

#. 设置设备欢迎语。

   ConnetOS# **set system login announcement** *announcement-message*

#. 提交配置

   ConnetOS# **commit**
