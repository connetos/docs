OSPF配置
===================

OSPF简介
--------------------------
OSPF（Open Shortest Path First）开放式最短路径优先协议，是基于链路状态的内部网关协议。

OSPF采用最短路径SPF（Shortest Path First）算法，通过链路状态通告LSA（Link State Advertisement）描述网络拓扑，依据网络拓扑生成一棵最短路径树SPT（Shortest Path Tree），计算出到网络中所有目的地的最短路径，进行路由信息的交换。

目前针对IPv4协议使用的是OSPFv2。如果没有特别说明，文中的OSPF都是指OSPFv2（RFC 2328）。

OSPF建立过程
++++++++++++++++++++++++++

OSPF建立过程如下：

#. 建立邻接关系。

   * 本端设备通过接口向外发送Hello报文与对端设备建立邻居关系。
   * 两端设备进行主/从关系协商和DD报文交换。
   * 两端设备通过更新LSA完成链路数据库LSDB（Link State Database）的同步。
   邻接关系建立成功。

#. OSPF采用SPF算法计算路由。

   OSPF协议路由的计算过程如下：
   
   #. 每台OSPF设备根据自己周围的网络拓扑结构生成链路状态通告LSA，并通过更新报文将LSA发送给网络中的其它OSPF设备。
   #. 每台OSPF设备都会收集其它设备发来的LSA，所有的LSA放在一起便组成了链路状态数据库LSDB。LSA是对设备周围网络拓扑结构的描述，LSDB则是对整个自治系统的网络拓扑结构的描述。
   #. OSPF设备将LSDB转换成一张带权的有向图，这张图便是对整个网络拓扑结构的真实反映。同一区域内各个设备得到的有向图是完全相同的。

OSPF优点
++++++++++++++++++++++++++

OSPF协议具有以下优点：

 * 快速收敛：在网络的拓扑结构发生变化后立即发送更新报文，使这一变化在自治系统中同步。
 * 无自环：根据收集到的LSA用最短路径树算法计算路由，从算法本身保证了不会生成自环路由。
 * 区域划分：把自治系统AS（Autonomous System）划分成逻辑意义上的一个或多个区域来管理。链路状态数据库只需要和区域内的设备保持一致，降低网络带宽。
 * 等价路由：支持到同一目的地址的多条等价路由。
 * 支持验证：支持基于区域和接口的报文验证，以保证报文交互的安全性。

常见概念
--------------------------

AS（Autonomous System）自治系统
+++++++++++++++++++++++++++++++++++++++++
一组使用相同路由协议交换路由信息的路由设备。 

Router ID
+++++++++++++++++++++++++++++++++++++++++
Router ID是一个32比特无符号整数，用于在AS中唯一标识一台路由设备。如果要运行OSPF协议，必须存在Router ID。建议将Router ID配置为与该设备某个接口的IP地址一致。

Router ID通过两种方式获得：

 * 命令行手动配置。
 * 自动选取。
  如果没有手动配置Router ID，ConnetOS会从当前接口的IP地址中自动选取一个最大值作为Router ID。 

只有重新配置系统的Router ID或OSPF的Router ID，并且重新启动OSPF进程后，才会进行Router ID的重新选取。

路由设备类型
+++++++++++++++++++++++++++++++++++++++++
OSPF路由设备根据在AS中的不同位置，可以分为以下四类: 

 * 区域内路由器（Internal Router）

   该类路由器的所有接口都属于同一个OSPF区域。

 * ABR（Area Border Router）区域边界路由器

   该类路由设备可以同时属于两个以上的区域，但其中一个必须是骨干区域。ABR用来连接骨干区域和非骨干区域，它与骨干区域之间既可以是物理连接，也可以是逻辑上的连接。

 * 骨干路由器（Backbone Router）

   该类路由设备至少有一个接口属于骨干区域。因此，所有的 ABR 和位于 Area0 的内部路由设备都是骨 干路由器。

 * ASBR（Autonomous System Boundary Router）自治系统边界路由器 

   与其他AS交换路由信息的路由设备称为ASBR。ASBR并不一定位于AS的边界，它有可能是区域内路由设备，也有可能是ABR。只要一台OSPF路由设备引入了外部路由的信息，它就成为 ASBR。 

路由类型
+++++++++++++++++++++++++++++++++++++++++
OSPF 将路由分为四类，按照优先级从高到低的顺序依次为： 

 * 区域内路由（Intra Area）
 * 区域间路由（Inter Area）
 * 第一类外部路由（Type1 External）
 * 第二类外部路由（Type2 External)

区域内和区域间路由描述的是AS内部的网络结构，外部路由则描述了应该如何选择到AS以外目的地址的路由。

OSPF将引入的AS外部路由分为两类:Type1和Type2。

 * Type1是指接收的是IGP（Interio rGateway Protocol，内部网关协议）路由（例如静态路由）。由于这类路由的可信程度较高，并且和OSPF自身路由的开销具有可比性，所以到第一类外部路由的开销等于本路由器到相应的ASBR的开销与ASBR到该路由目的地址的开销之和。
 * Type2是指接收的是EGP（Exterior Gateway Protocol，外部网关协议）路由。由于这类路由的可信度比较低，所以OSPF协议认为从ASBR到自治系统之外的开销远远大于在自治系统之内到达ASBR的开销。所以计算路由开销时将主要考虑前者，即到第二类外部路由的开销等于ASBR到该路由目的地址的开销。如果计算出开销值相等的两条路由，再考虑本路由器到相应的ASBR的开销。

OSPF的认证方式
+++++++++++++++++++++++++++++++++++++++++
OSPF支持报文验证功能，只有通过验证的OSPF报文才能接收，否则将不能正常建立邻居。交换机采用接口验证的方式验证报文。

路由引入
+++++++++++++++++++++++++++++++++++++++++
当OSPF网络中的设备需要访问运行其他协议的网络中的设备时，需要将其他协议的路由引入到OSPF网络中。

OSPF可以引入其它路由协议学习到的路由。在引入时通过配置路由策略来过滤路由，只引入满足条件的路由。由于只有ASBR才能引入路由，因此该过滤规则只在ASBR上配置才有效。

OSPF报文类型
+++++++++++++++++++++++++++++++++++++++++
OSPF有五种类型的协议报文: 

 * Hello报文

   周期性发送，用来发现和维持OSPF邻居关系。包括：定时器的数值、DR（Designated Router，指定路由器）、BDR（Backup Designated Router，备份指定路由器）以及已知的邻居。

 * DD（Database Description，数据库描述）报文

   描述本地LSDB中每一条LSA的摘要信息，用于两台路由器进行数据库同步。 

 * LSR（Link State Request，链路状态请求）报文
 
   向对方请求所需的LSA。两台路由器互相交换DD报文之后，得知对端的路由器有哪些LSA是本地的LSDB所缺少的之后，发送LSR报文向对方请求所需的LSA。内容包括所需要的LSA的摘要。
 
 * LSU（Link State Update，链路状态更新）报文

   向对方发送其所需要的LSA。

 * LSAck（Link State Acknowledgment，链路状态确认）报文

   用来对收到的LSA进行确认。内容是需要确认的LSA的Header（一个报文可对多个LSA 进行确认）。

LSA类型
+++++++++++++++++++++++++++++++++++++++++
OSPF中对链路状态信息的描述都是封装在LSA中发布出去，常用的LSA有以下几种类型：

  * Router LSA（Type1）：由每个路由设备产生，描述路由设备的链路状态和开销，在其始发的区域内传播。
  * Network LSA（Type2）：由DR产生，描述本网段所有路由设备的链路状态，在其始发的区域内传播。
  * Network Summary LSA（Type3）：由ABR（Area Border Router，区域边界路由器）产生，描述区域内某个网段的路由，并通告给其他区域。
  * ASBR Summary LSA（Type4）：由ABR产生，描述到ASBR的路由，通告给相关区域。 
  * AS External LSA（Type5）：由ASBR产生，描述到AS外部的路由，通告到所有的区域（除了Stub区域和NSSA区域）。
  * NSSA External LSA（Type7）：由NSSA（Not-So-Stubby Area）区域内的ASBR产生，描述到AS外部的路由，仅在NSSA区域内传播。
  * Opaque LSA：是一个被提议的LSA类别，由标准的LSA头部后面跟随特殊应用的信息组成，可以直接由OSPF协议使用，或者由其它应用分发信息到整个OSPF域间接使用。

   Opaque LSA分为 Type9、Type10、Type11三种类型，泛洪区域不同。其中，Type9的OpaqueLSA仅在本地链路范围进行泛洪，Type10的Opaque LSA仅在本地区域范围进行泛洪，Type11的LSA可以在一个自治系统范围进行泛洪。 

选路规则
+++++++++++++++++++++++++++++++++++++++++
OSPF协议有RFC2328和RFC1583两种不同的选路规则。在如何选择最优路由的问题上，RFC1583和RFC2328所定义的优先规则是不相同的：

 * 当RFC1583选路规则被使能时，设备会根据开销值选择发布到相同目的地址的路由。
 * 当RFC1583选路规则被关闭时，设备会先根据路由类型来选择发布到相同目的地址的路由，其次才是路由的开销值。

OSPF路由域中的所有设备应统一配置同一种选路规则。目前大部分OSPF路由域都配置成RFC2328规定的选路规则。

区域Area
--------------------------

区域分类
+++++++++++++++++++++++++++++++++++++++++
随着网络规模的扩大，当网络中运行OSPF的路由设备较多时，会导致LSDB非常庞大，占用大量的存储空间。而随着SPF算法复杂度的增加，CPU负担也变得很重。而网络规模的增大，拓扑结构发生变化的概率也增大，造成大量的OSPF传递及路由重新计算，网路经常处于“动荡”之中。

OSPF协议通过将AS划分成不同的区域（Area）来解决这个问题。区域是从逻辑上将路由器划分为不同的组，每个组用区域号（Area ID）来标识。区域的边界不是链路，而是路由设备。一个路由设备可以属于不同的区域，但是一个网段（链路）只能属于一个区域，即每个运行OSPF的接口必须指明属于哪一个区域。

划分区域后，可以在区域边界路由设备上进行路由聚合，以减少通告到其他其他区域的LSA 数量，还可以将网络拓扑变化带来的影响最小化。 

OSPF的区域类型分为：

 * Normal：普通区域，分为标准区域和骨干区域。
 * Stub区域：不传播它们接收到的自治系统外部路由，只允许发布区域内路由。
 * NSSA区域：能够将自治域外部路由引入并传播到整个OSPF自治域中，同时又不会学习来自OSPF网络其它区域的外部路由。

Normal区域
+++++++++++++++++++++++++++++++++++++++++
普通区域，分为标准区域和骨干区域：
 
 * 标准区域是最通用的区域，它传输区域内路由，区域间路由和外部路由。
 * 骨干区域是连接所有其他OSPF区域的中央区域，用Area 0表示。骨干区域负责区域之间的路由，非骨干区域之间的路由信息必须通过骨干区域来转发。

区域必须满足：
 
 * 所有非骨干区域必须与骨干区域保持连通。
 * 骨干区域自身也必须保持连通。 

在实际应用中，如果因为各方面条件的限制，无法满足所有非骨干区域与骨干区域保持连通的要求，此时可以通过配置OSPF虚连接（Virtual Link）来解决这个问题。

虚连接是指在两台ABR之间通过一个非骨干区域而建立的一条逻辑上的连接通道。虚连接相当于在两个ABR之间形成了一个点到点的连接，两端接口上配置的参数必须一致，如Hello报文间隔。为虚连接两端提供一条非骨干区域内部路由的区域称为传输区（Transit Area）。

Stub区域
+++++++++++++++++++++++++++++++++++++++++
Stub区域是一些特定的区域，Stub区域的ABR不允许注入Type5 LSA。对于位于AS边缘的非骨干区域，可以将区域配置为Stub区域，能避免Type5 LSA在Stub区域的泛洪，减少路由表的规模。

为保证到本自治系统的其他区域或者自治系统外的路由依旧可达，该区域的ABR将生成一条缺省路由，并发布给本区域中的其他非ABR路由器。

Totally Stub（完全Stub）区域的ABR不会将区域间的路由信息和外部路由信息传递到本区域，Stub区域中的路由表规模以及路由信息传递的数量进一步减少。

配置（Totally）Stub区域时需要注意：

 * 骨干区域不能配置成Stub区域。
 * 如果要将一个区域配置成Stub区域，则该区域中的所有路由设备必须都要配置stub命令。
 * （Totally）Stub区域内不能存在ASBR，即自治系统外部的路由不能在本区域内传播。
 * 虚连接不能穿过（Totally）Stub区域。

NSSA区域
+++++++++++++++++++++++++++++++++++++++++
NSSA（Not-So-Stubby Area）区域是Stub区域的变形。NSSA区域也不允许Type5 LSA注入，但可以允许Type7 LSA注入。

Type7 LSA由NSSA区域的ASBR产生，在NSSA区域内传播。当Type7 LSA到达NSSA的ABR时。由ABR将Type7 LSA转换成Type5 LSA。传播到其他区域。

网络类型
++++++++++++++++++++++++++++++++
链路两端的OSPF接口的网络类型必须一致，否则双方不能建立起邻居关系。根据链路层协议类型，OSPF支持以下四种类型的网络：

 * 广播（Broadcast）

   链路层协议是Ethernet、FDDI时，OSPF缺省认为网络类型是Broadcast。

   * 通常以组播形式（224.0.0.5）发送Hello报文和LSAck报文。
   * 对于LSU报文，通常以组播形式首次发送，以单播形式进行重传。
   * 以单播形式发送DD报文和LSR报文。

 * NBMA（Non-Broadcast Multi-Access）

   当链路层协议是ATM时，OSPF缺省认为网络类型是NBMA。

   * NBMA网络必须是全连通的，即网络中任意两台交换机之间都必须直接可达。
   * 以单播形式发送协议报文（Hello报文、DD报文、LSR报文、LSU报文、LSAck报文）。

 * 点到多点P2M（point-to-multipoint）

   没有一种链路层协议缺省是P2M，P2M类型是由其他的网络类型强制更改的。通常将NBMA网络改为P2M网络。

   * P2M网络中的掩码长度必须一致。
   * 以组播形式（224.0.0.5）发送Hello报文，以单播形式发送DD报文、LSR报文、LSU报文、LSAck报文。

 * 点到点P2P（point-to-point）
  
   NBMA网络必须是全连通的，即网络中任意两台路由器之间都必须有一条虚电路直接可达。

   * 如果部分路由器之间没有直接可达的链路时，应将接口配置成P2M类型。
   * 如果路由器在NBMA网络中只有一个对端，也可将接口类型配置为P2M类型。 

配置OSPF基本功能
--------------------------
#. 进入配置模式。
   
   ConnetOS> **configure**

#. 配置Router ID。

   ConnetOS# **set protocols ospf4 router-id** *router-id*
  
   缺省情况下，Router ID是0.0.0.0。
   
   修改router-id后必须重启系统或者在修改router-id之前先删除所有OSPF配置。

#. 创建OSPF区域。
   
   ConnetOS# **set protocols ospf4 area** *area-id*

   缺省情况下，创建OSPF区域后，区域类型为normal。
   
   骨干区域的Area ID为0。

#. 配置OSPF区域所包含的网段。
  
   ConnetOS# **set protocols ospf4 area** *area-id* **area-range** *network-address* **advertise enable** { **false** | **true** }
  
   一个网段只能属于一个区域。

#. 使能接口的OSPF功能

   ConnetOS# **set protocols ospf4 area** *area-id* **interface** *l3-interface-name* [ **vif** *l3-interface-name.1* ] **addres** *ip-address* **enable** { **false** | **true** }
   
   如果 **vlan-interface** 下配置了两个或多个IP地址，则选择参数 *vif l3-interface-name.1* ，发布除第一个以外的IP地址。
   
   一个网段只能属于一个区域，每个运行OSPF协议的接口必须指明所属的区域。

#. 提交配置。
   
   ConnetOS# **commit**

配置OSPF区域
--------------------------
当对整个网络划分区域完毕后，可以根据组网需要进一步将区域配置成Stub区域或者NSSA区域。 

当非骨干区域不能与非骨干区域保持连通，或者骨干区域因为各方面的限制无法保持连通时，可以通过配置OSPF虚连接解决。

#. 配置区域类型。

   ConnetOS# **set protocols ospf4 area** *area-id* **area-type** { **normal** | **nssa** | **stub** }

   对于位于AS边缘的非骨干区域，可以将区域配置为Stub区域。

#. 使能在stub区域中生成缺省路由的功能。

   ConnetOS# **set protocols ospf4 area default-lsa enable** { **false** | **true** }

   缺省情况下，此功能已经使能。

#. 配置OSPF发送到Stub区域的缺省路由开销。

   ConnetOS# **set protocols ospf4 area** *area-id* **default-lsa metric** *metric*

   本命令只能在Stub区域的ABR上配置才能生效。

#. 配置虚连接。

   ConnetOS# **set protocols ospf4 area** *area-id* **virtual-link** *ip-address* **authentication** { **md5** *key-id* | **simple-password** *password* } | **hello-interval** *hello-interval* | **retransmit-interval** *retransmit-interval* | **router-dead-interval** *router-dead-interval* | **transmit-area** *transmit-area-id* | **transmit-delay** *transmit-delay* }

   为使虚连接生效，虚连接的另一端也需要配置此命令，并且 **hello-interval** 和 **router-dead-interval** 的值必须一致。

#. 提交配置。

   ConnetOS# **commit**

配置OSPF的网络类型
--------------------------
#. 配置接口的网络类型。
   
   ConnetOS# **set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **link-type** { **broadcast** | **p2m** | **p2p** }

#. （可选）配置OSPF选举时的DR优先级。

   ConnetOS# **set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *ip-address* **priority** *priority-value*

   只有在接口的网络类型是广播时，才会选举DR，其他网络类型不需要。

#. 提交配置。

   ConnetOS# **commit**

配置OSPF选路信息
--------------------------
#. 配置OSPF接口的开销值。

   ConnetOS# **set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *vif-ip-address* **interface-cost** *interface-cost*

#. 配置兼容RFC1583的外部路由选择规则。

   ConnetOS# **set protocols ospf4 rfc1583-compatibility enable** { **false** | **true** }

   OSPF路由域中的所有设备应统一配置同一种选路规则。

#. 提交配置。
   
   ConnetOS# **commit**

配置OSPF的路由信息控制
--------------------------
#. 配置应用路由策略

   ConnetOS# **set protocols ospf4** { **export** *import-policy* | **mport** *import-policy* }

#. 配置路由聚合。
   
   ConnetOS# **set protocols ospf4 area** *area-id* **summaries enable** { **false** | **true** }

#. 配置只通告，但是不运行OSPF协议。

   ConnetOS# **set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *ip-address* **passive** [ **host** ] **enable** { **false** | **true** }

#. 配置邻居OSPF路由设备。

   ConnetOS# **set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *ip-address* **neighbor** *ip-address* [ **router-id** *router-id* ] 

#. 提交配置。

   ConnetOS# **commit**

调整和优化OSPF网络
--------------------------

#. 配置接口发送hello报文的时间间隔。
   
   ConnetOS# **set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *ip-address* **hello-interval** *hello-interval*

   缺省情况下，接口发送hello报文的时间间隔为10秒。

#. 配置相邻邻居失效时间间隔。

   ConnetOS# **set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *ip-address* **router-dead-interval** *router-dead-interval*

   缺省情况下，OSPF邻居失效时间间隔为40秒。

#. 配置接口的LSA传送延迟时间。

   ConnetOS# **set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *ip-address* **transmit-delay** *transmit-delay*
 
   缺省情况下，LSA传送的延迟时间为1秒。

#. 配置相邻交换机重传LSA的时间间隔。

   ConnetOS# **set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *ip-address* **retransmit-interval** *retransmit-interval*

   缺省情况下，LSA重传的时间间隔为5秒。

#. 配置OSPF接口的验证方式。

   ConnetOS# **set protocols ospf4 area** *area-id* **interface** *l3-interface-name* **address** *ip-address* **authentication** { **md5** *md5* | **simple-password** }

#. 提交配置。

   ConnetOS# **commit**



