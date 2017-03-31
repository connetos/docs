堆叠命令
====================================

set member-id
------------------------------------
命令功能
+++++++++++++++
**set member-id** 命令用来切换设备模式及member ID。

缺省情况下，设备的member ID是0，即处于单机模式。

命令格式
++++++++++++++++
**set member-id** *member-id*

参数说明
++++++++++++++++
*member-id*：堆叠设备的member ID。整数形式，取值范围是0～2。

 * 0：表示设备处于单机模式。
 * 1：表示设备处于堆叠模式，且member ID为1。
 * 2：表示设备处于堆叠模式，且member ID为2。

命令模式
++++++++++++++++
运维模式

使用指南
+++++++++++++++
如果如果要使能堆叠特性，必须首先设置堆叠模式及设备的member ID。

配置举例
+++++++++++++++
# 设置本设备为堆叠模式，并且member ID为1::

ConnetOS> set member-id 1
Are you sure you want to change the member-id(yes/no)?

set iss member mad enable
-------------------------------------------

命令功能
+++++++++++++++
**set iss member mad enable** 命令用来配置是否使能ISS MAD检测功能。

**delete member mad enable** 命令用来删除配置的ISS MAD检测功能，恢复为缺省值。

缺省情况下，ISS MAD检测功能没有使能。

命令格式
+++++++++++++++
**set iss member** *member-id* **mad enable** { **false** | **true** }

**delete iss member** *member-id* **mad** [ **enable** ]

参数说明
+++++++++++++++
*member-id*：堆叠设备的member ID。

**false**：不使能ISS MAD的检测功能。

**true**：使能ISS MAD的检测功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
当一个堆叠好的系统发生分裂时，会成为两个独立的ISS系统，各自成为Master，这种现象的出现是会影响网络的可用性的。这时，可以使用MAD检测ISS系统是否有发生分裂，以便进行及时处理。

配置举例
+++++++++++++++
# 使能ISS MAD的检测功能::

 ConnetOS# set iss member 1 mad enable true

set iss member mad excluded-interface
-------------------------------------------

命令功能
+++++++++++++++
**set iss member mad excluded-interface** 命令用来配置ISS MAD检测时的预留接口。

**delete iss member mad excluded-interface** 命令用来删除配置的ISS MAD检测预留接口。

缺省情况下，没有配置ISS MAD的检测预留接口。

命令格式
+++++++++++++++
**set iss member** *member-id* **mad excluded-interface** *interface-name*

**delete iss member** *member-id* **mad excluded-interface**

参数说明
+++++++++++++++
*member-id*：堆叠设备的member ID。

*interface-name*：进行ISS MAD检测的预留接口，可配置多个。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
堆叠分裂时，除了预留接口，其他接口都会down。

配置举例
+++++++++++++++
# 配置进行ISS MAD检测的预留接口为te-1/1/2::

 ConnetOS# set iss member 1 mad excluded-interface te-1/1/2

set iss member mad interface
-------------------------------------------

命令功能
+++++++++++++++
**set iss member mad interface** 命令用来配置ISS MAD检测的接口。

**delete iss memberme mad interface** 命令用来删除配置的ISS MAD检测接口。

缺省情况下，没有配置ISS MAD的检测接口。

命令格式
+++++++++++++++
**set iss member** *member-id* **mad interface** *interface-name*

**delete iss member** *member-id* **mad interface**

参数说明
+++++++++++++++
*member-id*：堆叠设备的member ID。

*interface-name*：进行ISS MAD检测的接口。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置进行ISS MAD检测的接口为te-1/1/1::

 ConnetOS# set iss member 1 mad interface te-1/1/1

set iss member priority
-------------------------------------------

命令功能
+++++++++++++++
**set iss member priority** 命令用来设置堆叠系统成员设备的优先级。

**delete iss member priority** 命令用来删除配置的堆叠系统成员设备的优先级。

缺省情况下，设备成员的优先级是1。

命令格式
+++++++++++++++
**set iss member** *member-id* **priority** *priority-number*

**delete iss member** *member-id* **priority**

参数说明
+++++++++++++++
*member-id*：堆叠设备的member ID。

*priority-number*：堆叠系统的成员优先级。整数形式，取值范围是0～32。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例。
+++++++++++++++
# 设置成员编号为1的成员优先级为4::

 ConnetOS# set iss member 1 priority 4

set interface gigabit-ethernet iss-port enable
--------------------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet iss-port enable** 命令用来配置是否将指定接口配置成堆叠接口。

**delete interface gigabit-ethernet iss-port enable** 命令用来删除堆叠接口。

缺省情况下，设备上没有堆叠接口。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name* **iss-port enable** { **false** | **true**}

**delete interface gigabit-ethernet** *interface-name* **iss-port enable**

参数说明
+++++++++++++++
*interface-name*：堆叠接口。

**false**：不使能指定接口的堆叠功能。

**true**：使能指定接口的堆叠功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
堆叠接口是堆叠设备连接的接口， 一般在进行ISS配置的时候指定，配置完成重启后，成员设备进行初始化时完成端口模式的转换及进行相关配置。在运行的过程中也可以动态添加或者删除堆叠口成员。

如果指定多个物理端口为堆叠接口，那么这些堆叠接口将形成汇聚接口组，进行流量负载分担。
跨设备通信的报文需要通过堆叠接口转发。

配置举例
+++++++++++++++
# 设置接口te-1/1/13为堆叠接口::

 ConnetOS# set interface gigabit-ethernet te-1/1/13 iss-port enable true

show iss（运维模式）
-------------------------------------------

命令功能
+++++++++++++++
**show iss** 命令用来查看ISS堆叠系统中所有设备的信息。

命令格式
+++++++++++++++
**show iss**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
此命令可以查看所有设备的角色的优先级、设备MAC、桥MAC等信息。

配置举例
+++++++++++++++
# 查看ISS堆叠系统中所有设备的信息::

 ConnetOS 1> show iss
 Member ID   Role     Priority   Device MAC          ISS MAC             Hostname
 ---------   ------   --------   -----------------   -----------------   ----------------
 1           Master   1          00:03:0f:64:da:5f   00:03:0f:64:da:5f   BJ-YUNQI-C1020-31.Int
 2           Slave    1          00:03:0f:64:da:53   00:03:0f:64:da:5f   BJ-YUNQI-C1020-32.Int

show iss（配置模式）
-------------------------------------------

命令功能
+++++++++++++++
**show iss** 命令用来查看ISS堆叠的配置信息。

命令格式
+++++++++++++++
**show iss** [ **member** { **1** | **2** } ]

参数说明
+++++++++++++++
**1**：member ID为1。

**2**：member ID为2。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查看ISS堆叠系统中对member ID为2的设备的配置::

  ConnetOS 1# show iss member 2
     priority: 1
     hostname: "ConnetOS"
     mad {
         enable: true
         interface: "qe-2/1/54"
     }

show iss configuration
-------------------------------------------

命令功能
+++++++++++++++
**show iss configuration** 命令用来查看堆叠系统的的配置信息。

命令格式
+++++++++++++++
**show iss configuration**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查看设备上堆叠的配置信息::

 ConnetOS 1> show iss configuration
 Member ID   ISS Link Status   Interface        Interface Status   Neighbour
 ---------   ---------------   --------------   ----------------   --------------
 1           Up                qe-1/1/49        Up                 qe-2/1/49
                               qe-1/1/52(*)     Up                 qe-2/1/52

 2           Up                qe-2/1/49        Up                 qe-1/1/49
                               qe-2/1/52(*)     Up                 qe-1/1/52

 -----------------------------------------
  * indicates the control interface of ISS.


show iss mad
-------------------------------------------

命令功能
+++++++++++++++
**show iss mad** 用来查看MAD的检测和处理情况。

命令格式
+++++++++++++++
**show iss mad**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
MAD：Multi-Active Detection，多Active检测。是一种检测和处理堆叠分裂后产生的多个Master的机制。

配置举例
+++++++++++++++
# 查看MAD的检测和处理信息::

 ConnetOS 1> show iss mad
 Member ID   Management   MAD State            MAD interface         Neighbor               Excluded interfaces
 ---------   ----------   ------------------   -------------------   --------------------   -------------------
 1           Enabled      Detect               qe-1/1/54             qe-2/1/54              N/A
 2           Enabled      Detect               qe-2/1/54             qe-1/1/54              N/A

show iss statistics
-------------------------------------------

命令功能
+++++++++++++++
**show iss statistics** 用来查看堆叠接口上各个类型的报文收发计数统计信息。
 
命令格式
+++++++++++++++
**show iss statistics**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 来查看堆叠接口上各个类型的报文收发计数统计信息::

 ConnetOS 1> show iss statistics
 Interface           Packet Type         Input               Output
 ----------          -----------         ----------          ----------
 qe-1/1/52           Hello               166748              166748
                     Elect               0                   1
                     ElectAck            4                   0
                     Anno                0                   1
                     AnnoAck             2                   0

 qe-1/1/49           Hello               166747              166748
                     Elect               0                   0
                     ElectAck            0                   0
                     Anno                0                   0
                     AnnoAck             0                   0

show iss sync-status
-------------------------------------------

命令功能
+++++++++++++++
**show iss sync-status** 命令用来查看ISS堆叠系统内设备的配置同步状态。

命令格式
+++++++++++++++
**show iss sync-status**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查看ISS堆叠系统内设备的配置同步状态::

 ConnetOS 1> show iss sync-status
 Member ID  Role    State    Last Sync Time
 ---------  ------  -------  -------------------
 1          Master  Full     2017-03-27 20:32:10
 2          Slave   Full     2017-03-27 20:32:10
