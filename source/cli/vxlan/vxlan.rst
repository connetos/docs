VXLAN命令
============================

set vsi vsi-id
-------------------------------------------

命令功能
+++++++++++++++
**set vsi vsi-id** 命令用来创建VSI。

**delete vsi vsi-id** 命令用来删除创建的VSI。

缺省情况下，设备上没有创建好的VSI。

命令格式
+++++++++++++++
**set vsi vsi-id** *vsi-id*

**delete vsi vsi-id** *vsi-id*

参数说明
+++++++++++++++
*vsi*：VSI ID，用于标识VSI。整数形式，取值范围是1～8192。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
报文是否进入VXLAN隧道是根据报文是否匹配到VSI（Virtual Switching Instance，虚拟交换实例）来决定的，VSI可以看做是VTEP上的一台基于VXLAN进行二层转发的虚拟交换机，它具有传统以太网交换机的所有功能，包括源MAC地址学习、MAC地址老化、泛洪等。VSI与VXLAN一一对应。可以用VSI来标识VXLAN。

配置举例
+++++++++++++++
# 配置VSI ID为1的VSI::

 ConnetOS# set vsi vsi-id 1 

set vsi vsi-id description
-------------------------------------------

命令功能
+++++++++++++++
**set vsi vsi-id description** 命令用来增加对VSI的描述。

**delete vsi vsi-id description** 命令用来删除指定VSI的描述。

缺省情况下，VSI创建后没有描述。

命令格式
+++++++++++++++
**set vsi vsi-id** *vsi-id* **description** *description*

**delete vsi vsi-id** *vsi-id* **description**

参数说明
+++++++++++++++
*vsi-id*：当前已经创建好的VSI ID。

*description*：对VSI的描述。字符串形式，不支持空格。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 增加对VSI 1的描述::

 ConnetOS# set vsi vsi-id 1 description toswtichb

set vsi vsi-id flooding enable
-------------------------------------------

命令功能
+++++++++++++++
**set vsi vsi-id flooding enable** 命令用来配置是否使能VSI向tunnel方向的泛洪抑制功能，向本地的业务接入点泛洪不受抑制。

**delete vsi vsi-id** 命令用来删除VSI向tunnel方向的泛洪抑制功能。

缺省情况下，VSI向tunnel方向的泛洪抑制功能没有使能。

命令格式
+++++++++++++++
**set vsi vsi-id** *vsi-id* **flooding enable** { **false** | **true** }

**delete vsi vsi-id** *vsi-id* **flooding** [ **enable** ]

参数说明
+++++++++++++++
*vsi-id*：VSI ID。整数形式，取值范围是1～8192。

**false**：不使能VSI泛洪抑制功能。

**true**：使能VSI泛洪抑制功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
缺省情况下，VTEP从本地站点内接收到BUM数据帧后，会在该VXLAN内除接收接口外的所有本地接口和VXLAN隧道上泛洪该数据帧，将该数据帧发送给VXLAN内的所有站点。如果用户希望把该类数据帧限制在本地站点内，不通过VXLAN隧道将其转发到远端站点，则可以通过配置命令手工禁止VXLAN对应VSI的泛洪功能。

配置举例
+++++++++++++++
# 使能VSI泛洪抑制功能::

 ConnetOS# set vsi vsi-id 1 flooding enable true 

set vsi vsi-id tunnel-ethernet
-------------------------------------------

命令功能
+++++++++++++++
**set vsi vsi-id tunnel-ethernet** 命令用来关联VSI和VXLAN隧道。

**delete vsi vsi-id tunnel-ethernet** 命令用来删除VSI关联的VXLAN隧道。

缺省情况下，VSI没有关联VXLAN隧道。

命令格式
+++++++++++++++
**set vsi vsi-id** *vsi-id* **tunnel-ethernet** *tunnel-name*

**delete vsi vsi-id** *vsi-id* **tunnel-ethernet** *tunnel-name*

参数说明
+++++++++++++++
*vsi-id*：VSI ID。整数形式，取值范围是1～8192。

*tunnel-name*：VXLAN隧道名称，取值范围是tunnel1~tunnel4094。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
VTEP必须与相同VNI内的其它VTEP建立VXLAN隧道，ConnetOS通过将VNI和VSI绑定，再将VSI和VXLAN隧道绑定实现。

配置举例
+++++++++++++++
# 配置VSI 1关联隧道tunnel1::

 ConnetOS# set vsi vsi-id 1 tunnel-ethernet tunnel1 

set vsi vsi-id vni
-------------------------------------------

命令功能
+++++++++++++++
**set vsi vsi-id vni** 命令用来给指定的VSI关联VNI。

**delete vsi vsi-id vni** 命令用来删除VSI关联的VNI。

缺省情况下，VSI没有关联VNI。

命令格式
+++++++++++++++
**set vsi vsi-id** *vsi-id* **vni** *vni-id*

**delete vsi vsi-id** *vsi-id* **vni**

参数说明
+++++++++++++++
*vsi-id*：VSI ID。整数形式，取值范围是1～8192。

*vni-id*：VNI ID。整数形式，取值范围是1～16777215。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
VSI与VNI一一对应，一个VSI只能关联一个VNI，一个VNI只能被一个VSI绑定。

配置举例
+++++++++++++++
# 将vsi 1和vni 1关联::

 ConnetOS#  set vsi vsi-id 1 vni 1

set interface tunnel-ethernet
-------------------------------------------

命令功能
+++++++++++++++
**set interface tunnel-ethernet** 命令用来新创建一条隧道。

**delete interface tunnel-ethernet** 命令用来删除已经配置好的隧道。

缺省情况下，没有创建隧道。

命令格式
+++++++++++++++
**set interface tunnel-ethernet** *tunnel-name*

**delete interface tunnel-ethernet** *tunnel-name*

参数说明
+++++++++++++++
*tunnel-name*：隧道名称。字符串形式，取值形式为tunnelx。x为整数，取值范围是1～4094。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 创建名字为tunnel1的隧道::

 ConnetOS＃ set interface tunnel-ethernet tunnel1

set interface tunnel-ethernet description
-------------------------------------------

命令功能
+++++++++++++++
**set interface tunnel-ethernet description** 命令用来增加对隧道的描述。

**delete interface tunnel-ethernet description** 命令用来删除已经配置的隧道描述。

缺省情况下，隧道创建后没有配置描述。

命令格式
+++++++++++++++
**set interface tunnel-ethernet** *tunnel-name* **description** *description*

**delete interface tunnel-ethernet** *tunnel-name* **description**

参数说明
+++++++++++++++
*tunnel-name*：隧道名称。字符串形式，取值形式为tunnelx。x为整数，取值范围是1～4094。

*description*： 对隧道的描述。字符串形式，取值范围是1～32。区分大小写，支持特殊字符，但不支持空格。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 增加对隧道的描述::

 ConnetOS# set interface tunnel-ethernet tunnel1 description toswitcha


set interface tunnel-ethernet destination address
---------------------------------------------------------------

命令功能
+++++++++++++++
**set interface tunnel-ethernet destination address** 命令用来配置隧道的目的端IP地址。

**delete interface tunnel-ethernet destination** 命令用来删除已经配置的隧道目的端IP地址。

缺省情况下，隧道创建后没有配置目的端IP地址。

命令格式
+++++++++++++++
**set interface tunnel-ethernet** *tunnel-name* **destination address** *ip-address*

**delete interface tunnel-ethernet** *tunnel-name* **destination**

参数说明
+++++++++++++++
*tunnel-name*：隧道名称。字符串形式，取值形式为tunnelx。x为整数，取值范围是1～4094。

*ip-address*：目的端IP地址。点分十进制形式。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置隧道tunnel1的目的端IP地址为2.2.2.2::

 ConnetOS# set interface tunnel-ethernet tunnel1 destination address 2.2.2.2

set interface tunnel-ethernet mode vxlan 
-------------------------------------------

命令功能
+++++++++++++++
**set interface tunnel-ethernet mode vxlan** 命令用来将隧道模式配置成VXLAN模式。

**delete interface tunnel-ethernet mode** 命令用来删除隧道的模式。

缺省情况下，隧道的模式是VXLAN。

命令格式
+++++++++++++++
**set interface tunnel-ethernet** *tunnel-name* **mode vxlan**

**delete interface tunnel-ethernet** *tunnel-name* **mode**

参数说明
+++++++++++++++
*tunnel-name*：隧道名称。字符串形式，取值形式为tunnelx。x为整数，取值范围是1～4094。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 将隧道tunnel1配置成为VXLAN隧道::

 ConnetOS# set interface tunnel-ethernet tunnel1 mode vxlan


set interface tunnel-ethernet source address
-----------------------------------------------------

命令功能
+++++++++++++++
**set interface tunnel-ethernet source address** 命令用来配置隧道的源端IP地址。

**delete interface tunnel-ethernet source address** 命令用来删除用户配置的隧道源端IP地址。

缺省情况下，隧道创建后没有配置源端IP地址。

命令格式
+++++++++++++++
**set interface tunnel-ethernet** *tunnel-name* **source address** *ip-address*

**delete interface tunnel-ethernet** *tunnel-name* **source** [ **address** ]

参数说明
+++++++++++++++
*tunnel-name*：隧道名称。字符串形式，取值形式为tunnelx。x为整数，取值范围是1～4094。

*ip-address*：源端IP地址。点分十进制形式。用户最多可以配置510个不同的源IP地址。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
隧道的源端IP地址将作为封装后报文的源IP地址。

配置举例
+++++++++++++++
# 配置隧道tunnel1的源端IP地址为1.1.1.1::

 ConnetOS# set interface tunnel-ethernet tunnel1 source address 1.1.1.1

set interface tunnel-ethernet static-mac-address
-----------------------------------------------------

命令功能
+++++++++++++++
**set interface tunnel-ethernet static-mac-address** 命令用来为隧道配置远端的静态MAC地址表项。

**delete interface tunnel-ethernet static-mac-address** 命令用来删除隧道配置远端的MAC地址表项。

缺省情况下，隧道上不存在任何远端的静态MAC地址表项。


命令格式
+++++++++++++++
**set interface tunnel-ethernet** *tunnel-name* **static-mac-address** *mac-address* [ **vsi** *vsi-id* ]

**delete interface tunnel-ethernet** *tunnel-name* [ **static-mac-address** *mac-address* [ **vsi** *vsi-id* ] ]

参数说明
+++++++++++++++
*tunnel-name*：隧道名称。字符串形式，取值形式为tunnelx。x为整数，取值范围是1～4094。

*mac-address*：MAC地址。

*vsi*：VSI ID。整数形式，取值范围是1～8192。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
VXLAN隧道必须与vsi参数指定的VSI关联，且该VSI必须已经创建，否则配置将失败。

VSI与tunnel的关联之前需要先删除对应的静态MAC。

配置举例
+++++++++++++++
# 配置VSI 1中VXLAN隧道1的远端MAC地址为00:00:00:00:00:22::

 ConnetOS# set interface tunnel-ethernet tunnel1 static-mac-address 00:11:22:33:44:55 vsi 1 

set interface family ethernet-switching vsi
---------------------------------------------------

命令功能
+++++++++++++++
**set interface family ethernet-switching vsi** 命令用来配置VTEP上端口的VXLAN接入点。

**delete interface family ethernet-switching vsi** 命令用来删除配置的接口的VXLAN接入点。

缺省情况下，没有创建接口的VXLAN接入点。

命令格式
+++++++++++++++
**set interface** { **gigabit-ethernet** | **aggregate-ethernet** } *interface-name* **family ethernet-switching vsi** *vsi-id* { **ethernet-mode enable true** | **vlan-mode dot1q** *vlan-id* }

**delete interface** { **gigabit-ethernet** | **aggregate-ethernet** } *interface-name* **family ethernet-switching vsi** { **ethernet-mode enable** | **vlan-mode dot1q** }

参数说明
+++++++++++++++
*interface-name*：接口名称。

*vsi-id*：VSI ID。整数形式，取值范围是1～8192。

*vlan-id*：VLAN ID，允许进入VXLAN隧道的指定VLAN Tag。整数形式，取值范围为1～4094。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
缺省情况下，端口未配置VXLAN业务接入点。业务接入点有两种模式：

 * VLAN模式
 * Ethernet模式

同一个端口只能配置一种模式。

VLAN模式时一个端口可以配置不同的匹配规则关联不同的VSI，一个端口只能有一个VLAN关联到某个VSI，如果一个VSI已经关联了某个VLAN，该端口再配置VSI关联其它VLAN时，需要先会先删掉前面的关联之后再配置后面的关联，如果这个VLAN已经关联到了其它的VSI，则下发失败，需要先手动删除之前关联之后才能下发。

端口一旦配置成了VXLAN业务接入点之后就与传统的VLAN隔离了，不能在原有的VLAN内做二层转发，不能再配置VLAN的静态MAC，同样配置了VLAN静态MAC的端口需要先删除端口静态MAC配置之后再配置VXLAN业务接入点。

物理接口和汇聚接口配置VXLAN接入点互斥，即已经配置了业务接入点的物理接口不能加入汇聚接口，已经在汇聚接口中的物理接口不能配置业务接入点。

配置举例
+++++++++++++++
# 配置端口te-1/1/1收到的VLAN 1的报文映射到VSI 1中::
  
  ConnetOS# set interface gigabit-ethernet te-1/1/1 family ethernet-switching vsi 1 vlan-mode dot1q 1

show ethernet-switching table vxlan
-------------------------------------------

命令功能
+++++++++++++++
**show ethernet-switching table vxlan** 命令用来查看VXLAN的FDB信息。

命令格式
+++++++++++++++
**show ethernet-switching table vxlan**

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
# 查看VXLAN的FDB信息::

 ConnetOS> show ethernet-switching table vxlan
 VSI       MAC address             Type         Age       Interfaces
 ----     -----------------        -------      ----      ----------
 1         00:00:00:00:00:23       Dynamic      0         ae1

show interface tunnel-ethernet
-------------------------------------------

命令功能
+++++++++++++++
**show interface tunnel-ethernet** 命令用来查看隧道的信息。

命令格式
+++++++++++++++
**show interface tunnel-ethernet** { *tunne-name* | **detail** } 

参数说明
+++++++++++++++
*tunnel-name*：隧道名称。

**detail**：查看隧道的详细信息。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
如果不指定detail，就显示所有tunnel的概要信息。

配置举例
+++++++++++++++
# 查看VXLAN隧道tunnel1的信息::

 ConnetOS> show interface tunnel-ethernet tunnel1 detail
 Tunnel: tunnel1,   State: Up,   Description:
 Source IP: 2.2.2.1,   Destination IP: 3.3.3.3
 Mode: VXLAN
 VNI ID:
   100,
 Traffic statistics:
   5 sec input rate 0 packets/sec
   5 sec output rate 0 packets/sec
   Input Packets........................0
   Output Packets.......................8133931727

show vsi
-------------------------------------------

命令功能
+++++++++++++++
**show vsi** 命令用来查看VSI的信息。

命令格式
+++++++++++++++
**show vsi** [ **vsi-id** *vsi-id* | **detail** ]

参数说明
+++++++++++++++
*vsi-id*：当前已经创建好的VSI ID。

**detail**：查看VSI的详细信息。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
如果不指定 **detail**，就显示所有VSI的概要信息。

配置举例
+++++++++++++++
# 查看VSI的详细信息::

 BConnetOS> show vsi detail
 VSI ID: 1
 VNI: 100
 Description:
 Tunnel Flooding: true
 VxLAN access ports:
   Interface   Dot1q   Mode
   ---------   -----  --------
   te-1/1/2    2       Vlan
   te-2/1/2    3       Vlan
 Tunnel interface:
   tunnel1
   tunnel10
 

