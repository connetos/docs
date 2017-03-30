物理接口命令
=============================

set interface gigabit-ethernet description
-----------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet description** 命令用来配置接口描述。

**delete interface gigabit-ethernet description** 命令用来删除配置的接口描述

缺省情况下，接口下没有配置接口描述。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name*  **description** *description*

**delete interface gigabit-ethernet** *interface-name* **description**

参数说明
+++++++++++++++
*interface-name*：接口名称。

*description*：接口描述。字符串形式，不支持空格。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 增加对接口te-2/2/1的描述::

 ConnetOS# set interface gigabit-ethernet te-2/1/1 description test

set interface gigabit-ethernet edge-port enable
----------------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet edge-port enable** 命令用来配置是否使能指定接口为边缘接口。

**delete interface gigabit-ethernet edge-port enable** 命令用来删除接口使能功能。

缺省情况下，所有的接口都不是边缘接口。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name* **edge-port enable** { **false** | **true** }

**delete interface gigabit-ethernet** *interface-name* **edge-port** [ **enable** ]

参数说明
+++++++++++++++
*interface-name*：接口名称。

**false**：不使能边缘接口功能。

**true**：使能边缘接口功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能接口te-1/1/1为边缘接口::

 ConnetOS# set interface gigabit-ethernet te-1/1/1 edge-port enable true

set interface gigabit-ethernet enable
-------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet enable** 命令用来配置接口功能是否使能。

**delete interface gigabit-ethernet enable** 命令用来删除接口使能功能。

缺省情况下，接口功能是使能的。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name* **enable** { **false** | **true** }

**delete interface gigabit-ethernet** *interface-name* **enable**

参数说明
+++++++++++++++
*interface-name*：接口名称。

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
# 使能接口te-2/2/1接口功能::

 ConnetOS# set interface gigabit-ethernet te-2/1/1 enable true

set interface gigabit-ethernet ether-options 802.3ad
-------------------------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet ether-options 802.3ad** 命令用来将指定接口加入到汇聚接口。

**delete interface gigabit-ethernet ether-options 802.3ad** 命令用来将指定接口从汇聚接口删除。

缺省情况下，接口没有加入任何汇聚接口。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name* **ether-options 802.3ad** *ae-number*

**delete interface gigabit-ethernet** *interface-name* **ether-options 802.3ad**

参数说明
+++++++++++++++
*interface-name*：接口名称。

*ae-number*：聚合接口编号，取值范围为ae1～ae46。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
实际使用时每个汇聚接口的成员端口数建议不要超过8个。

配置举例
+++++++++++++++
# 将接口te-1/1/1加入到汇聚接口ae1中::

 ConnetOS# set interface gigabit-ethernet te-1/1/1 ether-options 802.3ad ae1

set interface gigabit-ethernet ether-options flow-control enable
-----------------------------------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet ether-options flow-control enable** 命令用来配置是否使能指定接口的流量控制功能。

**delete interface gigabit-ethernet ether-options flow-control enable** 命令用来删除聚合接口的流量控制功能。

缺省情况下，接口功能流量控制功能是不使能的。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name* **ether-options flow-control enable** { **false** | **true** }

**delete interface gigabit-ethernet** *interface-name* **ether-options flow-control** [ **enable** ]

参数说明
+++++++++++++++
*interface-name*：接口名称。

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
# 使能接口te-1/1/1的流量控制功能::

 ConnetOS# set interface gigabit-ethernet te-1/1/1 ether-options flow-control enable true

set interface gigabit-ethernet ether-options mac-learning enable
-------------------------------------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet ether-options mac-learning enable** 命令用来配置是否使能指定接口的MAC地址学习功能。

**delete interface gigabit-ethernet ether-options mac-learning enable** 命令用来删除配置的接口MAC地址学习功能，恢复为缺省值。

缺省情况下，接口的MAC地址学习功能是使能的。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name* **ether-options mac-learning enable** { **false** | **true** }

**delete interface gigabit-ethernet** *interface-name* **ether-options lacp mac-learning** [ **enable** ]

参数说明
+++++++++++++++
*interface-name*：接口名称。

**false**：去使能接口的MAC地址学习功能。

**true**：使能接口的MAC地址学习功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能接口te-1/1/1的MAC地址学习功能::

 ConnetOS# set interface gigabit-ethernet te-1/1/1 ether-options mac-learning enable true 

set interface gigabit-ethernet family ethernet-switching native-vlan-id
-------------------------------------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet family ethernet-switching native-vlan-id** 命令用来配置指定接口的Native VLAN。

**delete interface gigabit-ethernet family ethernet-switching vlan members** 命令用来将指定接口从Native VLAN中删除。

缺省情况下，接口的Native VLAN为VLAN 1。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name* **family ethernet-switching native-vlan-id** *vlan-id*

**delete interface gigabit-ethernet** *interface-name* **family ethernet-switching** [ *native-vlan-id* ]


参数说明
+++++++++++++++
*interface-name*：接口名称。

*vlan-id*：VLAN ID，整数形式，取值范围是1～4094。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无论端口模式为Access还是Trunk，都有Native VLAN ID。可以通过命令对所属的VLAN ID进行修改。

配置举例
+++++++++++++++
# 将接口te-1/1/1的Native VLAN修改为VLAN 2::

 ConnetOS# set interface gigabit-ethernet te-1/1/1 family ethernet-switching native-vlan-id 2

set interface gigabit-ethernet family ethernet-switching port-mode
-------------------------------------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet family ethernet-switching port-mode** 命令用来配置接口的链路类型。

**delete interface gigabit-ethernet family ethernet-switching port-mode** 命令用来删除用户配置的链路类型，恢复为缺省值。

缺省情况下，接口的链路类型为access。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name* **family ethernet-switching port-mode** { **access** | **trunk** }

**delete interface gigabit-ethernet** *interface-name* **family** [ **ethernet-switching** [ **port-mode** ] ]

参数说明
+++++++++++++++
*interface-name*：接口名称。

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
# 配置接口te-2/2/1的链路类型为trunk::

 ConnetOS# set interface gigabit-ethernet te-1/1/1 family ethernet-switching port-mode trunk

set interface gigabit-ethernet family ethernet-switching vlan members
-------------------------------------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet family ethernet-switching vlan members** 命令用来将指定接口加入到多个VLAN中。

**delete interface gigabit-ethernet family ethernet-switching vlan members** 命令用来讲指定接口从指定VLAN中删除。

缺省情况下，聚合接口已经加入到Native VLAN1中。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name* **family ethernet-switching vlan members** *vlan-id*

**delete interface gigabit-ethernet** *interface-name* **family ethernet-switching** [ **vlan members** *vlan-id* ]

参数说明
+++++++++++++++
*interface-name*：接口名称。

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
# 将接口te-1/1/1加入到VLAN2、VLAN3、VLAN4、VLAN5、VLAN7中::

 ConnetOS# set interface gigabit-ethernet te-1/1/1 family ethernet-switching vlan members 2:5,7

set interface gigabit-ethernet mtu
-------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet mtu** 命令用来配置接口MTU值。

**delete interface gigabit-ethernet mtu** 命令用来删除接口配置的MTU值，恢复到缺省值。

缺省情况下，接口的MTU值为1518。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name* **mtu** *mtu-value*

**delete interface gigabit-ethernet** *interface-name* **mtu**

参数说明
+++++++++++++++
*interface-name*：接口名称。

*mtu-value*：接口MTU值。整数形式，取值范围是64～9216，单位是字节。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置接口te-1/1/1的MTU为1200::

 ConnetOS# set interface gigabit-ethernet te-1/1/1 mtu 1200

set interface gigabit-ethernet rate-limiting
-------------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet rate-limiting** 命令用来配置指定接口上的报文限速。

**delete interface gigabit-ethernet rate-limiting** 命令用来删除配置的接口限速。

缺省情况下，没有配置报文限速。
 
命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name* **rate-limiting** { **egress** | **ingress** } **kilobits** *rate-limit*

**delete interface gigabit-ethernet** *interface-name* **rate-limiting** [ **egress** | **ingress** [ **kilobits** ] ] 

参数说明
+++++++++++++++
**egress**：出接口方向。

**ingress**：入接口方向。

*rate-limit*：报文速率。整数形式，取值范围是1～40000000，单位是Kbit/s。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置接口te-1/1/1的入接口的报文限速为10000000 Kbit/s::

 ConnetOS# set interface gigabit-ethernet te-1/1/1 rate-limiting ingress kilobits 10000000

set interface gigabit-ethernet speed
-------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet speed** 命令用来配置指定接口的接口速率。
缺省情况下，接口速率为10G。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name* **speed** { **1000** | **10000** | **40000** }

参数说明
+++++++++++++++
**1000**：配置接口速率为1G。

**10000**：配置接口速率为10G。

**40000**：配置接口速率为40G

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置接口te-1/1/1的接口速率为40G::

 ConnetOS# set interface gigabit-ethernet te-1/1/1 speed 40000

set interface gigabit-ethernet static-mac-address
-----------------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet static-mac-address** 命令用来配置指定接口的静态MAC地址。

**delete interface gigabit-ethernet static-mac-address** 命令用来删除指定接口的静态MAC地址。

缺省情况下，接口下没有配置静态MAC地址。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name* **static-mac-address** *static-mac-address* [ **vlan** *vlan-id* ]

**delete interface gigabit-ethernet** *interface-name* **static-mac-address** *static-mac-address* [ **vlan** *vlan-id* ]

参数说明
+++++++++++++++
*interface-name*：接口名称。

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
# 配置接口te-1/1/1的静态MAC地址为00:11:22:33:44:50::

 ConnetOS# set interface gigabit-ethernet te-1/1/1 static-mac-address 00:11:22:33:44:50

set interface gigabit-ethernet storm-control
------------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet storm-control** 命令用来配置指定接口下的风暴控制功能。

**delete interface gigabit-ethernet storm-control** 命令用来删除配置的风暴控制功能，恢复到缺省值。

缺省情况下，聚合接口下的风暴控制功能。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-name* **storm-control** { **broadcast** | **multicast** | **unicast** } **kilobits** *suppress*

**delete interface gigabit-ethernet** *interface-name* **storm-control** { **broadcast** | **multicast** | **unicast** }  [ **kilobits** ]

参数说明
+++++++++++++++
*interface-name*：接口名称。

*suppress*：对流量的限制速率。整数形式，取值范围是1～40000000，单位是Kbit/s。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置接口te-1/1/1的对广播报文的抑制速率为10000000Kbit/s::

 ConnetOS# set interface gigabit-ethernet te-1/1/1 storm-control broadcast kilobits 10000000

