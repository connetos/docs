堆叠命令
====================================

set member-id
------------------------------------
命令功能
+++++++++++++++
**set member-id** 命令用来设置堆叠系统成员设备的编号。

缺省情况下，设备的堆叠编号是0，即处于单机模式。

命令格式
++++++++++++++++
**set member-id** *member-id*

参数说明
++++++++++++++++
*member-id*：堆叠系统的成员设备编号。整数形式，取值范围是0～2。0：表示设备处于单机模式；非0表示设备处于堆叠模式。

命令模式
++++++++++++++++
运维模式

使用指南
+++++++++++++++
如果要使能堆叠特性，必须首先配置这个，这个应该是用来进行堆叠主备设备的选择。

配置举例
+++++++++++++++
# 设置本设备的堆叠设备的成员编号为1::

ConnetOS> set member-id 1
Are you sure you want to change the member-id(yes/no)?

set member-id mad enable
-------------------------------------------

命令功能
+++++++++++++++
**set member-id mad enable** 命令用来配置是否使能ISS MAD的检测功能。

**delete member-id mad enable** 命令用来删除配置的ISS MAD检测功能是否使能。

缺省情况下，ISS MAD的检测功能没有使能。

命令格式
+++++++++++++++
**set member-id** *member-id* **mad enable** { **false** | **true** }

**delete member-id** *member-id* **mad** [ **enable** ]

参数说明
+++++++++++++++
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

set member-id mad excluded-interface
-------------------------------------------

命令功能
+++++++++++++++
**set member-id mad excluded-interface** 命令用来配置ISS MAD检测的预留接口。

**delete member-id mad excluded-interface** 命令用来删除配置的ISS MAD检测预留接口。

缺省情况下，没有配置ISS MAD的检测预留接口。

命令格式
+++++++++++++++
**set member-id** *member-id* **mad excluded-interface** *interface-name*

**delete member-id** *member-id* **mad excluded-interface**

参数说明
+++++++++++++++
*interface-name*：进行ISS MAD检测的预留接口。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置进行ISS MAD检测的预留接口为te-1/1/2::

 ConnetOS# set iss member 1 mad excluded-interface te-1/1/2

set member-id mad interface
-------------------------------------------

命令功能
+++++++++++++++
**set member-id mad interface** 命令用来配置ISS MAD检测的接口。

**delete member-id mad interface** 命令用来删除配置的ISS MAD检测接口。

缺省情况下，没有配置ISS MAD的检测接口。

命令格式
+++++++++++++++
**set member-id** *member-id* **mad interface** *interface-name*

**delete member-id** *member-id* **mad interface**

参数说明
+++++++++++++++
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

set member-id priority
-------------------------------------------

命令功能
+++++++++++++++
**set member-id priority** 命令用来设置堆叠系统成员设备的优先级。

**delete member-id priority** 命令用来删除配置的堆叠系统成员设备的优先级。

缺省情况下，设备成员的优先级是。

命令格式
+++++++++++++++
**set member-id** *member-id* **priority** *priority-number*

**delete member-id** *member-id* **priority**

参数说明
+++++++++++++++
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

show iss
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

 ConnetOS> show iss
 MemberId    Role      Priority      Device-Mac
 *+1        Master       1          00:E0:EC:38:E1:BD

 --------------------------------------------------------
 * indicates the device is the master.
 + indicates the device through which the user logs in.

 The Bridge MAC of the ISS is: (00:E0:EC:38:E1:BD)
 Mac persistent              :  Always

show iss configuration
-------------------------------------------

命令功能
+++++++++++++++
**show iss configuration** 命令用来查看堆叠的配置信息。

命令格式
+++++++++++++++
**show iss configuration**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查看设备上堆叠的配置信息::

 ConnetOS 1> show iss configuration
 Member ID   	ISS Link Status   	Interface      	 Interface Status     Neighbour
 ---------   	---------------   	--------------   ----------------     --------------
 1           	Up                  te-1/1/31(*)     Up                   te-2/1/31

 2          	Up                  te-2/1/31(*)     Up                   te-1/1/31

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
 Member ID 	 Status  	State  	   Local MAD interface  	     Remote MAD interface             Excluded interfaces
 ---------   --------   -------    ---------------------------   -----------------------------    -------------------
 1         	 Disabled   Init       N/A                  		 N/A                    		  N/A
 2         	 Disabled   Init       N/A                  		 N/A                   			  N/A

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
# ::

 ConnetOS 1> show iss statistics
 Interface          	Packet Type       	Input           Output
 ----------          	-----------         ----------      ----------
 te-1/1/31          	Hello             	14899           14900
                  		Elect             	0               1
                 		ElectAck          	4               0
                  		Anno            	0               1
                  		AnnoAck         	2               0


show iss sync-status
-------------------------------------------

命令功能
+++++++++++++++
**show iss sync-status** 命令用来查看ISS角色数据库信息。

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
# ::

 ConnetOS 1> show iss sync-status
 Member ID  Role    State    Last Sync Time
 ---------  ------  -------  -------------------
 1          Master  Full     2016-12-19 15:46:43
 2          Slave   Full     2016-12-19 15:46:43

