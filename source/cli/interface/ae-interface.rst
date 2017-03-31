汇聚接口命令
====================================

set interface aggregate-ethernet description
-------------------------------------------------

命令功能
+++++++++++++++
**set interface aggregate-ethernet description** 命令用来配置汇聚接口的描述。

**delete interface aggregate-ethernet description** 命令用来删除配置的汇聚接口描述

缺省情况下，接口下没有配置汇聚接口的描述。

命令格式
+++++++++++++++
**set interface aggregate-ethernet** *ae-number* **description** *description*

**delete interface aggregate-ethernet** *ae-number* **description**

参数说明
+++++++++++++++
*ae-number*：汇聚接口编号，取值范围为ae1～ae46。

*description*：接口描述。字符串形式，不支持空格。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 增加对汇聚接口ae1的描述::

 ConnetOS# set interface aggregate-ethernet ae1 description test

set interface aggregate-ethernet enable
-------------------------------------------

命令功能
+++++++++++++++
**set interface aggregate-ethernet enable** 命令用来配置汇聚接口功能是否使能。

**delete interface aggregate-ethernet enable** 命令用来删除汇聚接口使能功能。

缺省情况下，接口功能是使能的。

命令格式
+++++++++++++++
**set interface aggregate-ethernet** *ae-number* **enable** { **false** | **true** }

**delete interface aggregate-ethernet** *ae-number* **enable**

参数说明
+++++++++++++++
*ae-number*：汇聚接口编号，取值范围为ae1～ae46。

**false**：去使能接口功能。

**true**：使能接口功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能ae1的汇聚接口功能::

 ConnetOS# set interface aggregate-ethernet ae1 enable true

set interface aggregate-ethernet ether-options flow-control enable
-----------------------------------------------------------------------

命令功能
+++++++++++++++
**set interface aggregate-ethernet ether-options flow-control enable** 命令用来配置是否使能汇聚接口的流量控制功能。

**delete interface aggregate-ethernet ether-options flow-control enable** 命令用来删除汇聚接口的流量控制功能。

缺省情况下，汇聚接口的流量控制功能没有使能。

命令格式
+++++++++++++++
**set interface aggregate-ethernet** *ae-number* **ether-options flow-control enable** { **false** | **true** }

**delete interface aggregate-ethernet** *ae-number* **ether-options flow-control** [ **enable** ]

参数说明
+++++++++++++++
*ae-number*：汇聚接口编号，取值范围为ae1～ae46。

**false**：去使能接口的流量控制功能。

**true**：使能接口的流量控制功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能ae1接口的流量控制功能::

 ConnetOS# set interface aggregate-ethernet ae1 ether-options flow-control enable true

set interface aggregate-ethernet ether-options lacp enable
---------------------------------------------------------------

命令功能
+++++++++++++++
**set interface aggregate-ethernet ether-options lacp enable** 命令用来配置汇聚接口的LACP功能是否使能。

**delete interface aggregate-ethernet ether-options lacp enable** 命令用来删除汇聚接口的LACP功能。

缺省情况下，汇聚接口的LACP功能是不使能的。

命令格式
+++++++++++++++
**set interface aggregate-ethernet** *ae-number* **ether-options lacp enable** { **false** | **true** }

**delete interface aggregate-ethernet** *ae-number* **ether-options lacp** [ **enable** ]

参数说明
+++++++++++++++
*ae-number*：汇聚接口编号，取值范围为ae1～ae46。

**false**：去使能接口的LACP功能。

**true**：使能接口的LACP功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能ae1接口的LACP功能::

 ConnetOS# set interface aggregate-ethernet ae1 ether-options lacp enable true

set interface aggregate-ethernet ether-options mac-learning enable
-----------------------------------------------------------------------

命令功能
+++++++++++++++
**set interface aggregate-ethernet ether-options mac-learning enable** 命令用来配置汇聚接口的MAC地址学习功能是否使能。

**delete interface aggregate-ethernet ether-options mac-learning enable** 命令用来删除配置的汇聚接口MAC地址学习功能，恢复为缺省值。

缺省情况下，汇聚接口的MAC地址学习功能是使能的。

命令格式
+++++++++++++++
**set interface aggregate-ethernet** *ae-number* **ether-options mac-learning enable** { **false** | **true** }

**delete interface aggregate-ethernet** *ae-number* **ether-options lacp mac-learning** [ **enable** ]

参数说明
+++++++++++++++
*ae-number*：汇聚接口编号，取值范围为ae1～ae46。

**false**：去使能接口的MAC地址学习功能。

**true**：使能接口的MAC地址学习功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 使能ae1接口的MAC地址学习功能::

 ConnetOS# set interface aggregate-ethernet ae1 ether-options mac-learning enable true

set interface aggregate-ethernet ether-options min-selected-port
-------------------------------------------------------------------------

命令功能
+++++++++++++++
**set interface aggregate-ethernet ether-options min-selected-port** 命令用来配置LACP的最小选中接口数量。

**delete interface aggregate-ethernet ether-options min-selected-port** 命令用来删除配置的最小选中接口数量，恢复到缺省值。

缺省情况下，端口选举时的最小选中接口数量为1。

命令格式
+++++++++++++++
**set interface aggregate-ethernet** *ae-number* **ether-options min-selected-port** *port-number*

**delete interface aggregate-ethernet** *ae-number* **ether-options min-selected-port**

参数说明
+++++++++++++++
*ae-number*：汇聚接口编号，取值范围为ae1～ae46。

*port-number*：最小选中接口数量。整数形式，取值范围是1～72。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置LACP选举端口时最小的选中接口数量为5::

 ConnetOS# set interface aggregate-ethernet ae1 ether-options min-selected-port 5

set interface aggregate-ethernet family ethernet-switching native-vlan-id
---------------------------------------------------------------------------------

命令功能
+++++++++++++++
**set interface aggregate-ethernet family ethernet-switching native-vlan-id** 命令用来修改汇聚接口的Native VLAN。

**delete interface aggregate-ethernet family ethernet-switching vlan members** 命令用来将汇聚接口从Native VLAN中删除。

缺省情况下，汇聚接口的Native VLAN为VLAN1

命令格式
+++++++++++++++
**set interface aggregate-ethernet** *ae-number* **family ethernet-switching native-vlan-id** *vlan-id*

**delete interface aggregate-ethernet** *ae-number* **family ethernet-switching** [ **native-vlan-id** ]

参数说明
+++++++++++++++
*ae-number*：汇聚接口编号，取值范围为ae1～ae46。

*vlan-id*：VLAN ID，整数形式，取值范围是1～4094。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无论端口模式为Access还是Trunk，都有Native VLAN ID。可以通过命令对所属的VLAN ID进行修改。

配置举例
+++++++++++++++
# 将汇聚接口ae1的Native VLAN修改为VLAN 2::

 ConnetOS# set interface aggregate-ethernet ae1 family ethernet-switching native-vlan-id 2 

set interface aggregate-ethernet family ethernet-switching port-mode
------------------------------------------------------------------------

命令功能
+++++++++++++++
**set interface aggregate-ethernet family ethernet-switching port-mode** 命令用来配置汇聚接口的链路类型。

**delete interface aggregate-ethernet family ethernet-switching port-mode** 命令用来删除用户配置的链路类型，恢复为缺省值。

缺省情况下，接口的链路类型为access。

命令格式
+++++++++++++++
**set interface aggregate-ethernet** *ae-number* **family ethernet-switching port-mode** { **access** | **trunk** }

**delete interface aggregate-ethernet** *ae-number* **family** [ **ethernet-switching** [ **port-mode** ] ]

参数说明
+++++++++++++++
*ae-number*：汇聚接口编号，取值范围为ae1～ae46。

**access**：此类型的接口主要用来连接用户主机，用于连接接入链路，且接入链路上通过的帧为不带Tag的以太网帧。仅仅允许唯一的VLAN ID通过本接口，这个VLAN ID与接口的缺省VLAN ID相同，Access接口发往对端设备的以太网帧永远是不带标签的帧。

**trunk**：此类型的接口主要用来和其他交换机进行连接，用于连接干道链路，允许多个VLAN的帧（带Tag标记）通过。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置接口ae1的链路类型为access::

 ConnetOS# ConnetOS# set interface aggregate-ethernet ae1 family ethernet-switching port-mode access

set interface aggregate-ethernet family ethernet-switching vlan members
-------------------------------------------------------------------------

命令功能
+++++++++++++++
**set interface aggregate-ethernet family ethernet-switching vlan members** 命令用来将汇聚接口加入到多个VLAN中。

**delete interface aggregate-ethernet family ethernet-switching vlan members** 命令用来将汇聚接口从指定VLAN中删除。

缺省情况下，汇聚接口已经加入到Native VLAN1中。

命令格式
+++++++++++++++
**set interface aggregate-ethernet** *ae-number* **family ethernet-switching vlan members** *vlan-id*

**delete interface aggregate-ethernet** *ae-number* **family ethernet-switching** [ **vlan members** *vlan-id* ]

参数说明
+++++++++++++++
*ae-number*：汇聚接口编号，取值范围为ae1～ae46。

*vlan-id*：VLAN ID，整数形式，取值范围是1～4094。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
如果要让一个接口属于多个VLAN，该接口的接口模式必须是Trunk。
Access模式下，一个端口只能属于一个VLAN，即Native VLAN。在Trunk模式下，可以设置一个端口属于多个VLAN。多个VLAN包括Native VLAN和其他VLAN。

配置举例
+++++++++++++++
# 将汇聚接口ae1加入到VLAN2、VLAN3、VLAN4、VLAN5、VLAN7中::

 ConnetOS#  set interface aggregate-ethernet ae1 family ethernet-switching vlan members 2:5,7

set interface aggregate-ethernet mtu
-------------------------------------------

命令功能
+++++++++++++++
**set interface aggregate-ethernet mtu** 命令用来配置汇聚接口的MTU值。

**delete interface aggregate-ethernet mtu** 命令用来删除汇聚接口配置的MTU值，恢复到缺省值。

缺省情况下，接口的MTU值为1518。

命令格式
+++++++++++++++
**set interface aggregate-ethernet** *ae-number* **mtu** *mtu-value*

**delete interface aggregate-ethernet** *ae-number* **mtu**

参数说明
+++++++++++++++
*ae-number*：汇聚接口编号，取值范围为ae1～ae46。

*mtu-value*：接口MTU值。整数形式，取值范围是64～9216，单位是字节。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置接口ae1的MTU值为1200::

 ConnetOS# set interface gigabit-ethernet te-1/1/1 mtu 1200

set interface aggregate-ethernet static-mac-address
------------------------------------------------------

命令功能
+++++++++++++++
**set interface aggregate-ethernet static-mac-address** 命令用来配置汇聚接口的静态MAC地址。

**delete interface aggregate-ethernet static-mac-address** 命令用来删除汇聚接口配置的静态MAC地址。

缺省情况下，汇聚接口下没有配置静态MAC地址。

命令格式
+++++++++++++++
**set interface aggregate-ethernet** *ae-number* **static-mac-address** *static-mac-address* [ **vlan** *vlan-id* ]

**delete interface aggregate-ethernet** *ae-number* **static-mac-address** *static-mac-address* [ **vlan** *vlan-id* ]

参数说明
+++++++++++++++
*ae-number*：汇聚接口编号，取值范围为ae1～ae46。

*static-mac-address*：静态MAC地址。取值形式为00:11:22:33:44:55。

*vlan-id*：VLAN ID，整数形式，取值范围是1～4094。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置汇聚接口ae1的静态MAC地址为00:11:22:33:44:55::

 ConnetOS# set interface aggregate-ethernet ae1 static-mac-address 00:11:22:33:44:55

set interface aggregate-ethernet storm-control
--------------------------------------------------

命令功能
+++++++++++++++
**set interface aggregate-ethernet storm-control** 命令用来配置汇聚接口下的风暴控制功能。

**delete interface aggregate-ethernet 
storm-control** 命令用来删除配置的风暴控制功能，恢复到缺省值。

缺省情况下，汇聚接口下的风暴控制功能。

命令格式
+++++++++++++++
**set interface aggregate-ethernet** *ae-number* **storm-control** { **broadcast** | **multicast** | **unicast** } **kilobits** *suppress*

**delete interface aggregate-ethernet** *ae-number* **storm-control** { **broadcast** | **multicast** | **unicast** }  [ **kilobits** ]

参数说明
+++++++++++++++
*ae-number*：汇聚接口编号，取值范围为ae1～ae46。

*suppress*：对流量的限制速率。整数形式，取值范围是1～40000000，单位是Kbit/s。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置接口ae1的对广播报文的抑制速率为10000000Kbit/s::

 ConnetOS# set interface aggregate-ethernet ae1 storm-control broadcast kilobits 10000000
