MAC地址表配置
=======================================

MAC地址表简介
---------------------------------------

MAC地址
+++++++++++++++++++++++++++++++++++++++
MAC（Media Access Control）地址用来定义网络设备的位置。MAC地址由48比特长、12位的16进制数字组成，其中从左到右开始，0到23bit是厂商向IETF等机构申请用来标识厂商的代码，24到47bit由厂商自行分派，是各个厂商制造的所有网卡的一个唯一编号。

MAC地址可以分为3种类型：

 * 物理MAC地址：这种类型的MAC地址唯一的标识了以太网上的一个终端，该地址为全球唯一的硬件地址；
 * 广播MAC地址：全1的MAC地址为广播地址（FF-FF-FF-FF-FF-FF），用来表示LAN上的所有终端设备；
 * 组播MAC地址：除广播地址外，第8bit为1的MAC地址为组播MAC地址（例如01-00-00-00-00-00），用来代表LAN上的一组终端。

ConnetOS支持的MAC地址格式是12位的十六进制数，用“:”分隔。比如：00:22:22:22:22:22。

MAC地址表
+++++++++++++++++++++++++++++++++++++++
MAC地址表记录了目的MAC 地址、MAC地址对应的出接口以及所属的VLAN ID，用于指导报文进行单播转发。在转发数据时， 设备根据报文中的目的 MAC 地址查询 MAC 地址表，快速定位出接口，从而减少广播。

MAC 地址表项的生成方式有两种：

 * 自动生成：设备根据收到的数据帧里的源MAC地址自动学习而建立。
   
   如果MAC地址表中不存在该MAC地址表项，设备则将这个新MAC地址以及该MAC地址对应的PortA和VLAN ID作为一个新的表项加入到MAC地址表中。

 * 手工配置：手工在MAC地址表中加入特定MAC地址表项，将设备与接口绑定。
   
   MAC格式为12位的16进制数，用“：”分隔，同时需要设置MAC对应的VLAN。例如：配置VLAN100下的te-1/1/1口静态MAC地址为00:22:22:22:22:22。

为适应网络的变化，MAC地址表需要不断更新。MAC表中自动生成的表项（即动态表项）并非永远有效，每一条表项都有一个生存周期，到达生存周期仍得不到更新的表项将被删除，这个生存周期被称作老化时间。如果在到达生存周期前记录被更新，则该表项的老化时间重新计算。

配置静态MAC地址表
---------------------------------------

#. 进入配置模式。

   ConnetOS> **configure**

#. 配置静态MAC地址表

   ConnetOS# **set interface gigabit-ethernet** *interface-name* **static-ethernet-switching mac-address** *mac-address* **vlan** *vlan-id*

#. 提交配置

   ConnetOS# **commit**

配置MAC地址表老化时间
---------------------------------------

#. 进入配置模式。

   ConnetOS> **configure**

#. 配置MAC地址的老化时间。

   ConnetOS# **set forwarding-options mac-aging-time** *aging-time*

   缺省情况下，MAC地址表老化时间是300s。

#. 提交配置

   ConnetOS# **commit**

清空MAC地址表
---------------------------------------

#. 进入配置模式。

   ConnetOS> **configure**

#. 清空指定接口MAC表。

   ConnetOS# **run clear ethernet-switching table** *interface-name*

#. 清空全部MAC表

   ConnetOS# **run clear ethernet-switching table all**

#. 提交配置

   ConnetOS# **commit**
