配置堆叠
=======================================

配置堆叠基本功能
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 配置堆叠设备的成员ID。

   ConnetOS# **set member-id** *member-id*

   一个堆叠系统内，成员设备的Member ID不能相同。

#. 配置堆叠设备的选举优先级。

   ConnetOS# **set member-id** *member-id* **priority** *priority-number*

   缺省情况下，选举优先级为1。数值越大，优先级越高

#. 配置堆叠接口。

   ConnetOS# **set interface gigabit-ethernet** *interface-name* **iss-port enable** { **false** | **true** }

   缺省情况下，堆叠接口没有使能。

#. 提交配置。

   ConnetOS# **commit**

配置MAD检测功能
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 使能ISS MAD的检测功能。

   ConnetOS# **set member-id** *member-id* **mad enable** { **false** | **true** }

   缺省情况下，MAD的检测功能没有使能

#. 配置用于ISS MAD的检测的接口。

   ConnetOS# **set member-id** *member-id* **mad interface** *interface-name*
 
#. 配置用于ISS MAD检测时不进行shutdown的接口。
  
   ConnetOS# **set member-id** *member-id* **mad excluded-interface** *interface-name*

#. 提交配置。

   ConnetOS# **commit**

查看堆叠系统情况
---------------------------------------
配置完成后，可以查看堆叠系统的信息及配置情况。

# 查看堆叠系统中的成员设备信息::

 ConnetOS 1> show iss
 Member ID   Role     Priority   Device MAC          ISS MAC             Hostname
 ---------   ------   --------   -----------------   -----------------   ----------------
 1           Master   1          00:03:0f:64:da:5f   00:03:0f:64:da:5f   BJ-YUNQI-C1020-31.Int
 2           Slave    1          00:03:0f:64:da:53   00:03:0f:64:da:5f   BJ-YUNQI-C1020-32.Int


# 查看堆叠系统中成员设备的配置信息::

 ConnetOS 1> show iss configuration
 Member ID   ISS Link Status   Interface        Interface Status   Neighbour
 ---------   ---------------   --------------   ----------------   --------------
 1           Up                qe-1/1/49        Up                 qe-2/1/49
                               qe-1/1/52(*)     Up                 qe-2/1/52

 2           Up                qe-2/1/49        Up                 qe-1/1/49
                               qe-2/1/52(*)     Up                 qe-1/1/52

 -----------------------------------------
  * indicates the control interface of ISS.

# 查看MAD的检测和处理信息::

 ConnetOS 1> show iss mad
 Member ID   Management   MAD State            MAD interface         Neighbor               Excluded interfaces
 ---------   ----------   ------------------   -------------------   --------------------   -------------------
 1           Enabled      Detect               qe-1/1/54             qe-2/1/54              N/A
 2           Enabled      Detect               qe-2/1/54             qe-1/1/54              N/A  