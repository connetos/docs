LLDP配置
=======================================

简介
---------------------------------------

LLDP概述
+++++++++++++++++++++++++++++++++++++++
目前，网络设备的种类日益繁多而且各自的配置错综复杂，为了使不同厂商的设备能够在网络中互通，就需要一个标准的信息交流平台，用于交互各自的系统及配置信息。

LLDP（Link Layer Discovery Protocol）链路层发现协议，是IEEE 802.1ab定义的二层发现协议。LLDP提供了一种标准的链路层发现方式：将本端设备的主要能力、管理地址、设备标识、接口标识等信息组织成不同的TLV（Type/Length/Value，类型/长度/值），并封装在LLDPDU（Link Layer Discovery Protocol Data Unit，链路层发现协议数据单元）中发布给自己直连的邻居，邻居设备收到这些信息后将其以标准的管理信息库MIB（Management Information Base）的形式保存起来，以供网络管理系统查询及判断链路的通信状况。

LLDP报文收发机制
+++++++++++++++++++++++++++++++++++++++

LLDP的工作模式
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
LLDP有以下四种工作模式：

 * Tx/Rx模式：既可以接收又可以发送LLDP报文。
 * Rx模式：只接收LLDP报文。
 * Tx模式：只发送LLDP报文。
 * Disabled：既不发送也不接收LLDP报文。

当端口的LLDP工作模式发生变化时，端口将对协议状态机进行初始化操作。为了避免端口模式频繁改变导致端口不断初始化，可以配置端口的初始化延迟时间，即当端口工作模式改变时延迟一段时间再执行初始化操作。

LLDP报文的发送
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
当端口工作在Tx/Rx或Tx模式时，设备会周期性地向邻居设备发送LLDP报文。如果设备的本地配置变化则会立即发送LLDP报文，通知邻居设备本地信息的变化。为了避免由于本地信息的频繁变化大量发送LLDP报文，每发送一个LLDP报文都需要延迟一段时间后再继续发送下一个报文。

当发现新的邻居设备（即收到一个新的LLDP报文且本地尚未保存发送该报文设备信息），或者设备的LLDP功能由去使能状态变为使能，或者设备的接口状态由Down变为Up的时候，该设备将自动启用快速发送机制。即将LLDP报文的发送周期缩短为1秒，并连续发送指定数量的LLDP报文后再恢复为正常的发送周期。

LLDP报文的接收
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
当端口工作在Tx/Rx或Rx模式时，设备会对收到的LLDP报文及其携带的TLV进行有效性检查，通过检查后再将邻居信息保存到本地。并根据LLDPDU报文中TLV携带的TTL值设置邻居信息在本地设备的老化时间。如果接收到的LLDPDU中的TTL值等于零，将立刻老化掉该邻居信息。

配置LLDP
---------------------------------------
缺省情况下，LLDP功能都是使能的。当需要对LLDP功能参数进行调整时，可以按照如下步骤进行。

#. 进入配置模式。

   ConnetOS> **configure**

#. 使能全局LLDP功能。
   
   ConnetOS# **set protocols lldp enable** { **false** | **true** }

   缺省情况下，全局的LLDP功能已经使能。

#. 配置接口下LLDP的工作模式。

   ConnetOS# **set protocols lldp interface** *interface-name* **status** { **disabled** | **rx-only** | **tx-only** | **tx-rx** }

   缺省情况下，接口下LLDP的工作模式为Tx/Rx。只有全局和接口下的LLDP都使能，LLDP功能才会生效。

#. 配置接口初始化延迟时间（接口下LLDP工作模式变化时，需要配置）。

   ConnetOS# **set protocols lldp reinit-delay** *reinit-delay*

#. 配置本设备允许发布的TLV类型。

   ConnetOS# **set protocols lldp tlv-select** { **mac-phy-cfg** | **management-address** | **port-description** | **port-vlan** | **system-capabilities** | **system-description** | **system-name** } **enable** { **false** | **true** }

   缺省情况下，本设备支持的TLV类型都发布。

#. 调整LLDP的相关参数
   
    * 配置邻居设备信息在本设备中保存的时间倍数
      
      ConnetOS# **set protocols lldp hold-time-multiplier** *hold-time-multiplier*

      缺省情况下，邻居设备信息在本设备中保持的时间倍数是4。

    * 配置LLDP报文的发送间隔
     
      ConnetOS# **set protocols lldp advertisement-interval** *advertisement-interval*
      
      缺省情况下，发送LLDP报文的时间间隔是30秒。

    * 配置LLDP报文的发送延迟
      
      ConnetOS# set protocols lldp transmit-delay transmit-delay

      缺省情况下，发送LLDP报文的延迟时间为2秒。

#. 提交配置

   ConnetOS# **commit**
