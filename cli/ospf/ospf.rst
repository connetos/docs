OSPF命令
============================

set protocols ospf4 area
-------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area** 命令用来配置OSPF区域。

**delete protocols ospf4 area** 命令用来删除配置好的OSPF区域。

缺省情况下，没有配置OSPF区域。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id*

**delete protocols ospf4 area** *area-id*

参数说明
+++++++++++++++
*area-id*：OSPF区域ID。IP地址形式，取值为点分十进制。建议和某个接口的IP地址保持一致。0.0.0.0表示骨干区域。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
创建好区域后，区域的缺省类型是normal。

配置举例
+++++++++++++++
# 创建区域ID为1.1.1.1的OSPF区域::

 ConnetOS# set protocols ospf4 area 1.1.1.1

set protocols ospf4 area area-range advertise enable
---------------------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area area-range advertise enable** 命令用来配置是否使能聚合路由通告功能。

**delete protocols ospf4 area area-range** 命令用来删除配置的聚合路由通告功能。

缺省情况下，没有使能聚合路由通告功能。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **area-range** *network-address* **advertise enable** { **false** | **true** }

**delete protocols ospf4 area** *area-id* **area-range** *network-address* [ **advertise** [ **enable** ] ]

参数说明
+++++++++++++++
*area-id*：OSPF区域标识，点分十进制形式。

*network-addres*：区域所包含的网段。取值形式是网段地址／掩码。

**false**：去使能聚合路由通告功能。

**true**：使能聚合路由通告功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
一个网段只能属于一个区域，或者说每个运行OSPF协议的接口必须指明属于某一个特定的区域。该处的网段是指运行OSPF协议接口的IP地址所在的网段。

OSPF需要对接收到的Hello报文做网络掩码检查，当接收到的Hello报文中携带的网络掩码和本设备不一致时，则丢弃这个Hello报文，即不能建立邻居关系。

配置举例
+++++++++++++++
# 在OSPF区域1.1.1.1上使能路由聚合通告功能::

 ConnetOS# set protocols ospf4 area 1.1.1.1 area-range 2.2.2.0/24 advertise enable

set protocols ospf4 area area-type
-------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area-type** 命令用来配置OSPF的区域类型。

**delete protocols ospf4 area area-type** 用来删除配置的OSPF区域类型。

缺省情况下，OSPF的网络类型是normal。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **area-type** { **normal** | **nssa** | **stub** }

**delete protocols ospf4 area** *area-id* **area-type**

参数说明
+++++++++++++++
*area-id*：区域标识，点分十进制形式。

**normal**：标准区域。

**nssa**：NSSA区域。

**stub**：Stub区域。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
对于位于AS边缘的非骨干区域，可以将区域配置为Stub区域，避免Type5 LSA在Stub区域的泛洪，减少路由表的规模。

在配置位于区域时需要注意：

 * 骨干区域不能被配置成Stub区域。
 * 如果要将一个区域配置成Stub区域，那么需要把区域中的所有路由设备的区域类型都配置成stub区域。 
 * 虚连接不能穿过Stub区域和NSSA区域。

配置举例
+++++++++++++++
# 配置OSPF的区域类型为Stub::

 ConnetOS# set protocols ospf4 area 1.1.1.1 area-type stub 

set protocols ospf4 area default-lsa enable
--------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area default-lsa enable** 命令用来配置是否使能在stub区域中生成缺省路由的功能。

**delete protocols ospf4 area default-lsa enable** 用来删除配置的在stub区域中生成缺省路由功能。

缺省情况下，没有使能stub区域生成缺省路由功能。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **default-lsa enable** { **false** | **true** }

**delete protocols ospf4 area** *area-id* **default-lsa enable**

参数说明
+++++++++++++++
**false**：不使能。

**true**：使能

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 在stub区域1.1.1.1中使能生成缺省路由的功能::

 ConnetOS# set protocols ospf4 area 1.1.1.1 default-lsa enable true

set protocols ospf4 area default-lsa metric
------------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 default-lsa metric** 命令用来指定OSPF发送到Stub区域的Type3缺省路由的开销。

**delete set protocols ospf4 default-lsa metric** 命令用来删除配置的缺省路由开销。

缺省情况下，发送到STUB区域的Type3缺省路由的开销为0。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **default-lsa metric** *metric*

**delete protocols ospf4 area** *area-id* **default-lsa metric**

参数说明
+++++++++++++++
*metric*：发送到STUB区域的Type3缺省路由的开销。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
本命令只能配置到连接到Stub区域的ABR上。

配置举例
+++++++++++++++
# 设置Stub区域1.1.1.1到缺省路由的开销为32::

 ConnetOS# set protocols ospf4 area 1.1.1.1 default-lsa metric 32

set protocols ospf4 area interface address authentication
-------------------------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area interface address authentication** 命令用来配置OSPF区域的接口认证方式。

**delete rotocols ospf4 area interface address authentication** 命令用来删除配置的接口认证方式。

缺省情况下，接口不对OSPF报文进行认证。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *vif-ip-address*  **authentication** { **md5** *key-id* | **simple-password** *password* }

**delete protocols ospf4 area** *area-id* **interface** *l3-interface-name* [ **address** *vif-ip-address*  [ **authentication** [ **md5** | **simple-password** ] ] ]

参数说明
+++++++++++++++
*area-id*：区域标识。IP地址形式，取值为点分十进制。

*l3-interface-name*：三层接口的名称，比如vlan100。必须为每个运行OSPF的接口指明所属的区域。

*vif-ip-address*：三层接口的IP地址。

*key-id*：MD5验证字标识符，必须和对端的验证字标识符一致。整数形式，取值范围是0～255。

*password*：简单密码。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
接口验证方式可以提高OSPF网络的安全性。用于在相邻的设备之间设置验证模式和口令，优先级高于区域验证方式。

配置举例
+++++++++++++++
# 在接口vlan100上配置OSPF的接口认证方式为MD5::

 ConnetOS# set protocols ospf4 area 1.1.1.1 interface vlan100 address 3.3.3.3 authentication md5 5

set protocols ospf4 area interface address enable
---------------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area interface address enable** 命令用来配置是否使能接口的OSPF功能。

**delete rotocols ospf4 area interface address enable** 命令用来删除配置OSPF。

缺省情况下，接口下的OSPF功能没有使能。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *vif-ip-address* **enable** { **false** | **true** }

**delete protocols ospf4 area** *area-id* **interface** *l3-interface-name* [ **address** *vif-ip-address* [ **enable** ] ]

参数说明
+++++++++++++++
*area-id*：区域标识。IP地址形式，取值为点分十进制。

*l3-interface-name*：三层接口的名称，比如vlan100。必须为每个运行OSPF的接口指明所属的区域。

*vif-ip-address*：三层接口的IP地址。

**false**：不使能OSPF功能。

**true**：使能OSPF功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
区域的边界是设备，而不是链路。必须为每一个运行OSPF的接口指明所属的区域。

当此接口使能了OSPF功能之后，OSPF将把这个接口的直连路由宣告出去。

配置举例
+++++++++++++++
# 使能三层接口vlan100的OSPF功能::

 ConnetOS# set protocols ospf4 area 1.1.1.1 interface vlan100 address 6.6.6.6 enable true

set protocols ospf4 area interface address hello-interval
--------------------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area interface address hello-interval** 命令用来配置接口发送Hello报文的时间间隔。

**delete rotocols ospf4 area interface address hello-interval** 命令用来删除配置的接口发送Hello报文的时间间隔，恢复为缺省值。

缺省情况下，接口发送Hello报文的时间间隔为10秒。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *vif-ip-address* **hello-interval** *hello-interval*

**delete protocols ospf4 area** *area-id* **interface** *l3-interface-name* [ **address** *vif-ip-address* [ **hello-interval** ] ]

参数说明
+++++++++++++++
*area-id*：区域标识。IP地址形式，取值为点分十进制。

*l3-interface-name*：三层接口的名称，比如vlan100。

*vif-ip-address*：三层接口的IP地址。

*hello-interval*：发送Hello报文的时间间隔。整数形式，取值范围是1～65535，单位是秒。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
Hello报文周期性的发送给邻居路由设备，用于维持邻居关系以及DR/BDR的选举。

**hello-interval** 的值越小，发现网络拓扑改变的速度越快，路由开销也就越大。本接口和邻接设备的 **hello-interval** 要保持一致。

配置举例
+++++++++++++++
# 设置Hello报文发送的时间间隔是30s::

 ConnetOS# set protocols ospf4 area 1.1.1.1 interface vlan100 address 7.7.7.7 hello-interval 30 

set protocols ospf4 area interface address interface-cost
---------------------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area interface address interface-cost** 命令用来配置接口上运行OSPF协议所需要的开销值。

**delete rotocols ospf4 area interface address interface-cost** 命令用来删除配置的开销值，恢复为缺省值。

缺省情况下，OSPF接口的开销值为1。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *vif-ip-address* **interface-cost** *interface-cost*

**delete protocols ospf4 area** *area-id* **interface** *l3-interface-name* [ **address** *vif-ip-address* [ **interface-cost** ] ]

参数说明
+++++++++++++++
*area-id*：区域标识。IP地址形式，取值为点分十进制。

*l3-interface-name*：三层接口的名称，比如vlan100。必须为每个运行OSPF的接口指明所属的区域。

*vif-ip-address*：三层接口的IP地址。

*interface-cost*：整数形式，取值范围是1～65535。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
当有多条发现协议、开销值、目的地址都相同的路由时，这几条路由就满足负载分担的条件。请根据实际组网情况，通过修改接口开销值来选择是否需要进行负载分担。

配置举例
+++++++++++++++
# 配置接口vlan100的开销值为10::

 ConnetOS# set protocols ospf4 area 1.1.1.1 interface vlan100 address 7.7.7.7 interface-cost 10 

set protocols ospf4 area interface address neighbor
----------------------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area interface address neighbor** 命令用来指定邻居路由设备。

**delete rotocols ospf4 area interface address neighbor** 命令用来删除指定的邻居路由设备。

缺省情况下，没有指定邻居路由设备。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *vif-ip-address* **neighbor** *ip-address* **router-id** *router-id*

**delete protocols ospf4 area** *area-id* **interface** *l3-interface-name* [ **address** *vif-ip-address* [ **neighbor** *ip-address* [ **router-id** ] ] ]

参数说明
+++++++++++++++
*area-id*：区域标识。IP地址形式，取值为点分十进制。

*l3-interface-name*：三层接口的名称，比如vlan100。必须为每个运行OSPF的接口指明所属的区域。

*vif-ip-address*：三层接口的IP地址。

*ip-address*：邻居路由设备的IP地址。

*router-id*：邻居路由设备的Router ID。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 指定邻居OSPF为2.2.2.2::

 ConnetOS# set protocols ospf4 area 1.1.1.1 interface vlan100 address 7.7.7.7 neighbor 2.2.2.2 router-id 2.2.2.2

set protocols ospf4 area interface address passive enable
-------------------------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area interface address passive enable** 命令用来配置是否使能只广播不运行OSPF协议功能。

**delete rotocols ospf4 area interface address passive enable** 命令用来恢复为缺省值。

缺省情况下，既不运行也不广播OSPF协议。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *vif-ip-address* **passive** [ **host** ] **enable** { **false** | **true** }

**delete protocols ospf4 area** *area-id* **interface** *l3-interface-name* [ **address** *vif-ip-address* [ **passive**  [ **host** ] [ **enable** ] ] ]

参数说明
+++++++++++++++
*area-id*：区域标识。IP地址形式，取值为点分十进制。

*l3-interface-name*：三层接口的名称，比如vlan100。必须为每个运行OSPF的接口指明所属的区域。

*vif-ip-address*：三层接口的IP地址。

**host**：只通告本机的OSPF路由。

**false**：不使能。

**true**：使能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能三层接口vlan100只广播不运行OSPF协议::

 ConnetOS# set protocols ospf4 area 1.1.1.1 interface vlan100 address 7.7.7.7 passive enable true  

set protocols ospf4 area interface address priority
-----------------------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area interface address priority** 命令用来配置广播网络中接口的DR选举优先级。

**delete rotocols ospf4 area interface address priority** 命令用来删除配置的DR选举优先级，恢复为缺省值。

缺省情况下，DR选举优先级为128。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *vif-ip-address* **priority** *priority*

**delete protocols ospf4 area** *area-id* **interface** *l3-interface-name* [ **address** *vif-ip-address* [ **priority** ] ]

参数说明
+++++++++++++++
*area-id*：区域标识。IP地址形式，取值为点分十进制。

*l3-interface-name*：三层接口的名称，比如vlan100。必须为每个运行OSPF的接口指明所属的区域。

*vif-ip-address*：三层接口的IP地址。

*priority*：本设备在DR选举时的优先级。整数形式，取值范围是0～255。值越大，优先级越高。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
接口的优先级决定了该接口在选举DR时所具有的资格，优先级高的接口在DR选举时被首先考虑。

如果一台设备的接口优先级为0，则它不会被选举为DR或BDR。在广播网络中，可以通过配置接口的DR优先级来影响网络中DR或BDR的选择。

当网段上选举出DR和BDR之后，它们就会向所有的邻居发送DD报文，建立邻接关系。

配置举例
+++++++++++++++
# 配置接口vlan100的DR优先级是20::

 ConnetOS# set protocols ospf4 area 1.1.1.1 interface vlan100 address 3.3.3.3 priority 20

set protocols ospf4 area interface address retransmit-interval
----------------------------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area interface address retransmit-interval** 命令用来配置LSA重传时间间隔。

**delete rotocols ospf4 area interface address retransmit-interval** 命令用来删除配置的LSA重传时间间隔，恢复为缺省值。

缺省情况下，LSA重传的时间间隔为5秒。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *vif-ip-address* **retransmit-interval** *retransmit-interval*

**delete protocols ospf4 area** *area-id* **interface** *l3-interface-name* [ **address** *vif-ip-address* [ **retransmit-interval** ]

参数说明
+++++++++++++++
*area-id*：区域标识。IP地址形式，取值为点分十进制。

*l3-interface-name*：三层接口的名称，比如vlan100。必须为每个运行OSPF的接口指明所属的区域。

*vif-ip-address*：三层接口的IP地址。

*retransmit-interval*：LSA重传的时间间隔。整数形式，取值范围是1～65535，单位是秒。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
在网络相对稳定、对路由收敛时间要求较高的组网环境中，可以指定LSA的更新时间间隔为0来取消LSA的更新时间间隔，使得拓扑或者路由的变化可以立即通过LSA发布到网络中，从而加快网络中路由的收敛速度。

如果对网络没有特殊要求，建议使用命令的缺省值。

配置举例
+++++++++++++++
# 配置LSA重传的时间间隔为3秒::

 ConnetOS# set protocols ospf4 area 1.1.1.1 interface vlan100 address 3.3.3.3 retransmit-interval 3

set protocols ospf4 area interface address router-dead-interval
----------------------------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area interface address router-dead-interval** 命令用来配置OSPF的邻居失效时间间隔。

**delete rotocols ospf4 area interface address retransmit-interval** 命令用来删除配置的OSPF邻居失效时间间隔，恢复为缺省值。

缺省情况下，OSPF的邻居失效时间间隔是40秒。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *vif-ip-address* **router-dead-interval** *router-dead-interval*

**delete protocols ospf4 area** *area-id* **interface** *l3-interface-name* [ **address** *vif-ip-address* [ **router-dead-interval** ]

参数说明
+++++++++++++++
*area-id*：区域标识。IP地址形式，取值为点分十进制。

*l3-interface-name*：三层接口的名称，比如vlan100。必须为每个运行OSPF的接口指明所属的区域。

*vif-ip-address*：三层接口的IP地址。

*router-dead-interval*：OSPF的邻居失效时间间隔。整数形式，取值范围是1～4294967295，单位是秒。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
OSPF邻居的失效时间间隔是指：在该时间间隔内，若未收到邻居的Hello报文，就认为该邻居已失效。运行OSPF接口上的邻居失效时间dead interval必须大于发送Hello报文的时间间隔hello interval，且同一网段上的设备的dead interval值也必须相同。

缺省情况下，邻居失效时间为发送Hello报文时间间隔的4倍。

配置举例
+++++++++++++++
# 配置接口vlan100上的OSPF的邻居失效时间间隔::

 ConnetOS# set protocols ospf4 area 1.1.1.1 interface vlan100 address 2.2.2.2 router-dead-interval 250

set protocols ospf4 area interface address transmit-delay
---------------------------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area interface address transmit-delay** 命令用来配置接口上发送LSA过程中的传输延迟时间。

**delete rotocols ospf4 area interface address transmit-delay** 命令用来删除配置的LSA传输延迟时间，恢复为缺省值。

缺省情况下，LSA过程中的传输延迟时间为1秒。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *vif-ip-address* **transmit-delay** *transmit-delay*

**delete protocols ospf4 area** *area-id* **interface** *l3-interface-name* [ **address** *vif-ip-address* [ **transmit-delay** ]

参数说明
+++++++++++++++
*area-id*：区域标识。IP地址形式，取值为点分十进制。

*l3-interface-name*：三层接口的名称，比如vlan100。必须为每个运行OSPF的接口指明所属的区域。

*vif-ip-address*：三层接口的IP地址。

*transmit-delay*：LSA过程中的传输延迟时间。整数形式，取值范围是1～3600，单位是秒。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
LSA在本设备的链路状态数据库（LSDB）中会随时间老化，但在网络的传输过程中却不会，所以有必要在发送之前在LSA的老化时间上增加本命令所设置的一段时间。此配置对低速率的网络尤其重要。

配置举例
+++++++++++++++
# 配置接口vlan100上的LSA传输延迟时间为2秒::

 ConnetOS# set protocols ospf4 area 1.1.1.1 interface vlan100 address 2.2.2.2 transmit-delay 2

set protocols ospf4 area interface link-type
------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area interface link-type** 命令用来配置OSPF接口的网络类型。

**delete rotocols ospf4 area interface link-type** 用来删除配置的OSPF接口网络类型，恢复为缺省值。

缺省情况下，接口的网络类型根据物理接口而定。以太网接口的网络类型为Broadcast，串口的网络类型为P2P。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **link-type** { **broadcast** | **p2m** | **p2p** }

**delete protocols ospf4 area** *area-id* **interface** *l3-interface-name* [ **link-type** ] 

参数说明
+++++++++++++++
*area-id*：区域标识。IP地址形式，取值为点分十进制。

*l3-interface-name*：三层接口的名称，比如vlan100。

**broadcast**：将接口的网络类型修改为广播。

**p2m**：将接口的网络类型修改为点到多点。

**p2p**：将接口的网络类型修改为点到点。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
一般情况下，链路两端的OSPF接口的网络类型必须一致，否则不能正确的计算路由。
根据实际情况配置接口的网络类型，例如：

 * 如果接口的网络类型是NBMA，但网络不是全连通的，必须将接口的网络类型改为P2M。这样，两台不能直接可达的交换机就可以通过一台与两者都直接可达的交换机来交换路由信息。

 * 如果同一网段内只有两台路由器运行OSPF协议，建议将接口的网络类型改为P2MP。

当接口配置成NBMA类型，由于无法通过广播Hello报文的形式动态的发现相邻路由设备，必须手动为接口指定相邻接口的IP地址、是否有选举权等。

配置举例
+++++++++++++++
# 设置接口vlan100的OSPF网络类型是P2MP::

 ConnetOS# set protocols ospf4 area 1.1.1.1 interface vlan100 link-type p2m

set protocols ospf4 area interface vif
-------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area interface address enable** 命令用来配置OSPF的虚接口。

**delete rotocols ospf4 area interface address enable** 用来删除配置的虚接口。

缺省情况下，没有配置OSPF虚接口。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **vif** *virtual-interface* [ **address** *ip-address* ]

**delete protocols ospf4 area** *area-id* **interface** *l3-interface-name* **vif** *virtual-interface*

参数说明
+++++++++++++++
*area-id*：区域标识。IP地址形式，取值为点分十进制。

*l3-interface-name*：三层接口的名称，比如vlan100。

*virtual-interface*：OSPF的虚接口。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 设置虚接口::

 ConnetOS# set protocols ospf4 area 1.1.1.1 interface vlan100 vif vlan100.1 address 7.7.7.

set protocols ospf4 area summaries enable
-------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area summaries enable** 命令用来配置是否使能向Stub区域发送聚合LSA功能。

**delete protocols ospf4 area summaries enable** 用来删除配置的向Stub区域发送聚合LSA功能。

缺省情况下，ABR会向Stub区域发送聚合LSA。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **summaries enable** { **false** | **true** }

**delete protocols ospf4 area** *area-id* **summaries enable**

参数说明
+++++++++++++++
*area-id*：区域标识。IP地址形式，取值为点分十进制。

**false**：去使能向Stub区域发送聚合LSA功能。

**true**：使能向Stub区域发送聚合LSA功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
该命令需要在ABR上配置。

配置举例
+++++++++++++++
# 使能向Stub区域发送聚合LSA功能::

 ConnetOS# set protocols ospf4 area 1.1.1.1 summaries enable true

set protocols ospf4 area virtual-link
-------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 area virtual-link** 命令用来创建并配置虚连接。

**delete protocols ospf4 area virtual-link** 
用来删除虚连接或恢复虚连接的参数为缺省值。

缺省情况下，OSPF没有创建虚连接。

命令格式
+++++++++++++++
**set protocols ospf4 area** *area-id* **virtual-link** *ip-address* **authentication** { **md5** *key-id* | **simple-password** *password* } | **hello-interval** *hello-interval* | **retransmit-interval** *retransmit-interval* | **router-dead-interval** *router-dead-interval*| **transmit-area** *transmit-area-id* | **transmit-delay** *transmit-delay* }

**delete protocols ospf4 area** *area-id* **virtual-link** *ip-address* **authentication** { **md5** | **simple-password** } | **hello-interval** | **retransmit-interval** | **router-dead-interval** | **transmit-area** | **transmit-delay** }

参数说明
+++++++++++++++
*ip-address*：指定建立虚连接的对端交换机IP地址。

*key-id*：MD5验证字标识符，必须与对端的标识符一致。整数形式，取值范围是0～255。

*password*：简单密码。

*hello-interval*：接口发送hello报文的时间间隔，该值必须与建立虚连接设备上的hello-interval值相同。整数形式，取值范围是1～65535，单位是秒。缺省值是10秒。

*retransmit-interval*：接口重传LSA的时间间隔。整数形式，取值范围是1～65535，单位是秒。缺省值是5秒。

*router-dead-interval*：失效时间间隔，该值必须与建立虚连接设备上的router-dead-interval值相同。取值范围1～4294967295。单位是秒。缺省值是40秒。

*transmit-area-id*：虚连接传输经过的区域ID。

*transmit-delay*：接口延迟发送LSA的时间间隔。整数形式，取值范围是1～3600，单位是秒。缺省值是1秒。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
在划分OSPF区域之后，非骨干区域之间的OSPF路由更新是通过骨干区域来交换完成的。因此，OSPF要求所有非骨干区域必须与骨干区域保持连通，并且骨干区域之间也要保持连通。但在实际应用中，因为各方面条件的限制，可能无法满足这个要求，这时可以通过配置OSPF虚连接解决。

配置参数值时有以下几点建议：

 * hello参数值越小，交换机感知网络变化的速度越快，消耗的网络资源也会越多。
 * retransmit参数值设置的太小会引起不必要的LSA重传，建议在网络速度较慢的网络中，该值可以设置得大一些。
 * 虚连接的验证模式必须与骨干区域的验证方式一致。

配置举例
+++++++++++++++
# 创建虚连接，对端设备ID为2.2.2.2::

 ConnetOS# set protocols ospf4 area 1.1.1.1 virtual-link 2.2.2.2

set protocols ospf4 export
-------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 export** 命令用来路由发布时的应用策略。

**delete protocols ospf4 export** 用来删除配置的路由发布策略。

缺省情况下，发布时没有应用路由策略。

命令格式
+++++++++++++++
**set protocols ospf4 export** *export-policy*

**delete protocols ospf4 export**

参数说明
+++++++++++++++
*exort-policy*：策略名称。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 设置路由发布应用策略::

 ConnetOS# set protocols ospf4 export p1

set protocols ospf4 import
-------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 import** 命令用来配置路由接收时的应用策略，控制引入的路由信息。

**delete protocols ospf4 import** 用来删除配置的路由策略。

缺省情况下，接收路由时没有应用发布策略。

命令格式
+++++++++++++++
**set protocols ospf4 import** *import-policy*

**delete protocols ospf4 import**

参数说明
+++++++++++++++
*import-policy*：路由策略。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 设置路由接收时的应用策略为p2::

 ConnetOS# set protocols ospf4 import p2

set protocols ospf4 ip-router-alert enable
-------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 ip-router-alert enable** 命令用来配置是否识别IP报文中携带的Router-Alert选项。

**delete set protocols ospf4 ip-router-alert enable** 用来删除设置的识别IP报文中携带的Router-Alert选项功能。

缺省情况下，设备不识别报文中携带的Router-Alert选项。

命令格式
+++++++++++++++
**set protocols ospf4 ip-router-alert enable** { **false** | **true** }

**delete protocols ospf4 ip-router-alert enable**

参数说明
+++++++++++++++
**false**：不识别IP报文中携带的Router-Alert选项。只有目的地址属于本设备的接口地址时，报文才会上送给路由协议层处理。

**true**：识别IP报文中携带的Router-Alert选项。带有Router-Alert选项的IP报文才会被上送到路由协议层处理。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
Router-Alert是一种标识协议报文的特殊机制。通常情况下，只有目的地址属于本设备的接口地址时，报文才会上送给路由协议层处理。如果一个报文中带有Router-alert选项，则表示该报文需要被上送到路由协议层去处理。

配置举例
+++++++++++++++
# 设置设备识别IP报文中携带的Router-Alert选项::

 ConnetOS# set protocols ospf4 ip-router-alert enable true

set protocols ospf4 rfc1583-compatibility enable
-----------------------------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 ip-router-alert enable** 命令用来配置是否兼容RFC1583选路规则。

**delete set protocols ospf4 ip-router-alert enable** 用来删除配置的是否兼容RFC1583选路规则。

缺省情况下，不兼容RFC1583选路规则。

命令格式
+++++++++++++++
**set protocols ospf4 rfc1583-compatibility enable** { **false** | **true** }

**set protocols ospf4 rfc1583-compatibility enable**

参数说明
+++++++++++++++
**false**：不兼容RFC1583选路规则。

**true**：兼容RFC1583选路规则。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
为了避免路由环路，对于是否兼容RFC1583的选路规则，同一路由域内的交换机建议配置相同，即要么配置所有交换机都兼容RFC1583的选路规则，要么配置所有交换机都不兼容RFC1583的选路规则。 

配置举例
+++++++++++++++
# 设置ConnetOS兼容RFC1583的选路规则::

 ConnetOS# set protocols ospf4 rfc1583-compatibility enable true

set protocols ospf4 router-id
-------------------------------------------

命令功能
+++++++++++++++
**set protocols ospf4 router-id** 命令用来配置运行OSPF协议设备的Router ID。

缺省情况下，Router ID为0.0.0.0。

命令格式
+++++++++++++++
**set protocols ospf4 router-id** *route-id* 

参数说明
+++++++++++++++
*route-id*：是一个32比特无符号整数，是一台交换机在自治系统中的唯一标识。自治系统中任意两台Router ID都不能相同。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
通常将Router ID配置为与交换机某个接口的IP地址一致。

修改Router ID后必须重启系统或者在修改Router ID之前先删除所有OSPF配置。

配置举例
+++++++++++++++
# 设置设备的Router ID为1.1.1.1::

 ConnetOS# set protocols ospf4 router-id 1.1.1.1
