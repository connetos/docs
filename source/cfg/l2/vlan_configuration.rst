VLAN配置
=======================================

简介
---------------------------------------

VLAN概述
+++++++++++++++++++++++++++++++++++++++
VLAN（Virtual Local Area Network）虚拟局域网，是将一个物理的LAN在逻辑上划分成多个广播域的通信技术。VLAN内的主机间可以直接通信，而VLAN间不能直接互通，从而将广播报文限制在一个VLAN内。

VLAN有如下优势：

 * 限制广播域：广播域被限制在一个VLAN内，节省了带宽，提高了网络处理能力。
 * 增强局域网的安全性：不同VLAN内的报文在传输时是相互隔离的。
 * 提高了网络的健壮性：故障被限制在一个VLAN内，本VLAN内的故障不会影响其他VLAN的正常工作。
 * 灵活构建虚拟工作组：用VLAN可以划分不同的用户到不同的工作组，同一工作组的用户也不必局限于某一固定的物理范围，网络构建和维护更方便灵活。

常见概念
+++++++++++++++++++++++++++++++++++++++

VLAN的帧格式
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
IEEE 802.1Q是虚拟桥接局域网的正式标准，对Ethernet帧格式进行了修改，在源MAC地址字段和协议类型字段之间加入4字节的802.1Q Tag。每台支持802.1Q协议的交换机发送的数据包都会包含VLAN ID，以指明交换机属于哪一个VLAN。

在一个VLAN交换网络中，以太网帧有以下两种形式：

 * 有标记帧（tagged frame）：加入了4字节802.1Q Tag的帧
 * 无标记帧（untagged frame）：原始的、未加入4字节802.1Q Tag的帧

链路类型
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
VLAN中有以下两种链路类型：

 * 接入链路（Access Link）：用于连接用户主机和交换机的链路。通常情况下，主机并不需要知道自己属于哪个VLAN，主机硬件通常也不能识别带有VLAN标记的帧。因此，主机发送和接收的帧都是untagged帧。
 * 干道链路（Trunk Link）：用于交换机间的互连或交换机与路由器之间的连接。干道链路可以承载多个不同VLAN数据，数据帧在干道链路传输时，干道链路的两端设备需要能够识别数据帧属于哪个VLAN，所以在干道链路上传输的帧都是Tagged帧。

接口类型
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
ConnetOS支持两种类型的接口：

 * Access接口：交换机上用来连接用户主机的接口，它只能连接接入链路。仅仅允许唯一的VLAN ID通过本接口，这个VLAN ID与接口的缺省VLAN ID相同，Access接口发往对端设备的以太网帧永远是不带标签的帧。
 * Trunk接口：是交换机上用来和其他交换机连接的接口，它只能连接干道链路，允许多个VLAN的帧（带Tag标记）通过。

VLAN接口
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
不同VLAN间的主机不能直接通信，通过在设备上配置VLAN接口，可以实现 VLAN 间的三层互通。 VLANIF 接口是一种三层逻辑接口，每个VLAN 对应一个 VLANIF。在为VLANIF接口配置了 IP 地址后，该IP 地址即可作为本 VLAN 内网络设备的网关地址，对需要跨网段的报文进行基于IP地址的三层转发。 

缺省VLAN
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
ConnetOS除了可以设置接口允许通过的VLAN，还可以设置接口的缺省VLAN，即 PVID（Port VLAN ID，native-vlan-id）。

在缺省情况下，所有端口的缺省VLAN均为1。用户可以根据需要进行配置。 

 * Access类型接口的缺省VLAN就是它所在的VLAN。 

 * Trunk类型接口可以允许多个 VLAN 通过，能够配置缺省 VLAN。 

配置VLAN的基本功能
---------------------------------------

#. 进入配置模式。

    ConnetOS> **configure**

#. 创建VLAN。
	
	ConnetOS# **set vlans vlan-id** *vlan-id*

#. （可选）配置VLAN的名称。

	ConnetOS# **set vlans vlan-id** *vlan-id* **vlan-name** *vlan-name*

#. （可选）为指定VLAN配置描述信息
	
	ConnetOS# **set vlans vlan-id** *vlan-id* **description** *description*

#. 提交配置。
	
	ConnetOS# **commit**

配置基于接口的VLAN接口
---------------------------------------

#. 进入配置模式。
	
	ConnetOS> **configure**

#. 配置接口类型。
	
	ConnetOS# **set interface gigabit-ethernet** *interface-name* **family ethernet-switching port-mode** { **access** | **trunk** }
	
	Access模式下，一个接口只能属于一个VLAN，即Native VLAN。

	trunk模式下，可以设置一个接口属于多个VLAN。多个VLAN包括缺省VLAN和其他VLAN。

#. 配置接口的缺省VLAN 。
    
    ConnetOS# **set interface gigabit-ethernet** *interface-name* **family ethernet-switching native-vlan-id** *vlan-id*
	
	缺省情况下，所有接口的native-vlan-id都为1。

#. 将接口加入VLAN ID。
	
	ConnetOS# **set interface gigabit-ethernet** *interface-name* **family ethernet-switching vlan members** *vlan-member&<1-n>*

#. 提交配置。
	
	ConnetOS# **commit**

查看VLAN
---------------------------------------
在配置模式下，执行 **show vlans** 命令，查看VLAN的配置信息::
 
 ConnetOS # show vlans
 Waiting for building configuration.
     vlan-id 1 {
         description: ""
         vlan-name: "default"
         l3-interface: ""
     }
     vlan-id 10 {
         description: ""
         vlan-name: "default"
         l3-interface: "vlan10"
     }

在运维模式下，执行 **show vlans** 命令，查看VLAN信息::

 ConnetOS > show vlans
 Vlan ID   Tag        Interfaces
 -------   --------   ------------------------------------------------------
 1         tagged
           untagged   te-1/1/1，  te-1/1/2，  te-1/1/3，  te-1/1/4，  te-1/1/5，
                      te-1/1/6，  te-1/1/7，  te-1/1/8，  te-1/1/9，  te-1/1/10，
                      te-1/1/11， te-1/1/12， te-1/1/13， te-1/1/14， te-1/1/16，
                      te-1/1/17， te-1/1/18， te-1/1/19， te-1/1/20， te-1/1/21，
                      te-1/1/22， te-1/1/23， te-1/1/24， te-1/1/25， te-1/1/26，
                      te-1/1/27， te-1/1/28， te-1/1/29， te-1/1/30， te-1/1/31，
                      te-1/1/32， te-1/1/33， te-1/1/34， te-1/1/35， te-1/1/36，
                      te-1/1/37， te-1/1/38， te-1/1/39， te-1/1/40， te-1/1/41，
                      te-1/1/42， te-1/1/43， te-1/1/44， te-1/1/45， te-1/1/46，
                      te-1/1/47， te-1/1/48， qe-1/1/49， qe-1/1/50， qe-1/1/51，
                      qe-1/1/52， qe-1/1/53， qe-1/1/54， te-2/1/1，  te-2/1/2，
                      te-2/1/3，  te-2/1/4，  te-2/1/5，  te-2/1/6，  te-2/1/7，
                      te-2/1/8，  te-2/1/9，  te-2/1/10， te-2/1/11， te-2/1/12，
                      te-2/1/13， te-2/1/14， te-2/1/15， te-2/1/16， te-2/1/17，
                      te-2/1/18， te-2/1/19， te-2/1/20， te-2/1/21， te-2/1/22，
                      te-2/1/23， te-2/1/24， te-2/1/25， te-2/1/26， te-2/1/27，
                      te-2/1/28， te-2/1/29， te-2/1/30， te-2/1/32， te-2/1/33，
                      te-2/1/34， te-2/1/35， te-2/1/36， te-2/1/37， te-2/1/38，
                      te-2/1/39， te-2/1/40， te-2/1/41， te-2/1/42， te-2/1/43，
                      te-2/1/44， te-2/1/45， te-2/1/46， te-2/1/47， te-2/1/48，
                      qe-2/1/49， qe-2/1/50， qe-2/1/51， qe-2/1/52， qe-2/1/53，
                      qe-2/1/54，
 10        tagged
           untagged   ae1，
