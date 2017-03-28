RSTP配置命令
=========================================

set protocols rstp bridge-priority
-------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp bridge-priority** 命令用来配置设备的根桥优先级。

**delete protocols rstp bridge-priority** 命令用来删除配置的根桥优先级。

缺省情况下，设备的根桥优先级是32768。

命令格式
+++++++++++++++
**set protocols rstp bridge-priority** *bridge-priority*

**delete protocols rstp bridge-priority**

参数说明
+++++++++++++++
*bridge-priority*：本设备的根桥优先级。整数形式，取值范围是0～61440，步长是4096。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
在一个运行STP/RSTP的网络中，每棵生成树有且仅有一个根桥，它负责发送BPDU报文并连接整个网络。由于根桥在网络中的重要性，在根桥选举过程中，通常希望性能高、网络层次高的交换设备会被选举为根桥。但是，性能高、网络层次高的交换设备其优先级不一定高，因此需要配置优先级以保证该设备成为根桥。

根桥优先级是生成树计算的重要依据，根桥优先级的高低会直接影响到生成树计算中根桥的选举。根桥优先级的数值越小，则该设备被选举为根桥的可能性越大。

配置举例
+++++++++++++++
# 配置设备的根桥优先级为6400::

 ConnetOS# set protocols rstp bridge-priority 6400

set protocols rstp enable
-------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp enable** 命令用来配置是否使能RSTP功能。

**delete protocols rstp enable** 命令用来删除RSTP功能。

缺省情况下，RSTP功能没有使能。

命令格式
+++++++++++++++
**set protocols rstp enable** { **false** | **true** }

**delete protocols rstp enable**

参数说明
+++++++++++++++
**false**：去使能RSTP功能。

**true**：使能RSTP功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 使能RSTP::

 ConnetOS# set protocols rstp enable true

set protocols rstp force-version
-------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp force-version** 命令用来配置RSTP协议的版本。

**delete protocols rstp force-version** 命令用来删除配置的RSTP协议版本，恢复为缺省值。

缺省情况下，RSTP的版本为1，即设备运行RSTP协议。

命令格式
+++++++++++++++
**set protocols rstp force-version** { **0** | **1** }

**delete protocols rstp force-version**

参数说明
+++++++++++++++
**0**：STP协议。

**1**：RSTP协议。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
RSTP协议兼容STP协议。

在运行生成树协议的网络中，运行不同生成树协议的交换设备之间报文可能无法互通，从而导致生成树不能正常计算。

交换设备提供两种工作模式： 

 * RSTP模式
 * STP模式

以解决上述可能引起的报文无法互通问题。


配置举例
+++++++++++++++
# 配置RSTP的版本为1::

 ConnetOS#  set protocols rstp force-version 1

set protocols rstp forward-delay
------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp forward-delay** 命令用来配置设备的Forward Delay时间。

**delete protocols rstp forward-delay** 命令用来删除配置的Forward Delay时间，恢复为缺省值。

缺省情况下，Forward Delay时间的缺省值是15秒。

命令格式
+++++++++++++++
**set protocols rstp forward-delay** forward-delay

delete protocols rstp forward-delay


参数说明
+++++++++++++++
forward-delay：Forward Delay时间值。整数形式，取值范围是4～30，单位是秒。大于2 × MaxAge + 1。


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
在运行生成树算法的网络中，当网络拓扑结构发生变化时，因为新的BPDU配置消息需要经过一定的时间才能传遍整个网络，所以本应被阻塞的端口可能还来不及被阻塞而之前被阻塞的端口已经不再阻塞，这样就有可能会形成临时的环路。为了避免这种情况引起的临时环路，可以通过Forward Delay定时器设置延时时间，即在这个延时时间内所有端口会临时被阻塞。

在根桥上配置的Forward Delay定时器的时间将通过BPDU传递下去，从而成为整棵生成树内所有交换设备的Forward Delay定时器的时间。

在配置Hello Time、Forward Delay和Max Age这三个时间参数值时，配置的数值应满足以下关系才能保证整个网络的生成树算法有效的工作，否则网络会频繁震荡。

 * 2 × (Forward Delay - 1s) >= Max Age
 * Max Age >= 2 × (Hello Time + 1s)

配置举例
+++++++++++++++
# 配置Forward Delay时间为20秒::

 ConnetOS# set protocols rstp forward-delay 20

set protocols rstp hello-time
-------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp hello-time** 命令用来配置设备发送BPDU的时间间隔，即定时器Hello Timer的时间值。

**delete protocols rstp hello-time** 命令用来删除配置的发送BPDU的时间间隔，恢复为缺省值。

缺省情况下，发送BPDU的时间间隔为2秒。

命令格式
+++++++++++++++
**set protocols rstp hello-time** *hello-time*

**delete protocols rstp hello-time**

参数说明
+++++++++++++++
*hello-time*：发送BPDU的时间间隔。整数形式，取值范围是1～9，取值要小于MaxAge/2 – 1。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
在运行生成树算法的网络中，以Hello Time为周期，交换设备会定时向处于同一棵生成树的其他设备发送BPDU，以此来维护生成树的稳定。

在根桥上配置的定时器Hello Timer的时间将通过BPDU传递下去，所以会成为整棵生成树内所有交换设备的定时器Hello Timer的时间。

根桥的Hello Time、Forward Delay以及Max Age三个时间参数配置的数值应满足以下关系才能保证整个网络的生成树协议有效的工作，否则网络会频繁震荡。

 * 2 × (Forward Delay - 1s) >= Max Age
 * Max Age >= 2 × (Hello Time + 1s)


配置举例
+++++++++++++++
# 配置交换设备定时器Hello Timer的时间值为4秒::

 ConnetOS# set protocols rstp force-version 1

set protocols rstp interface bpdu-filter enable
-----------------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp interface bpdu-filter enable** 命令用来使能指定接口的BPDU报文过滤功能。

**delete protocols rstp interface bpdu-filter enable** 命令用来删除配置的BPDU报文过滤功能，恢复为缺省值。

缺省情况下，接口不过滤BPDU报文。

命令格式
+++++++++++++++
**set protocols rstp interface** *interface-name* **bpdu-filter enable** { **false** | **true** }

**delete protocols rstp interface** *interface-name* **bpdu-filter enable**

参数说明
+++++++++++++++
*interface-name*：接口名称。

**false**：不使能接口的BPDU报文过滤功能。

**true**：使能接口的BPDU报文过滤功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
边缘端口不需要发送BPDU报文，可以配置BPDU报文过滤功能，使边缘端口不处理、不发送BPDU报文。减少网络震荡。

配置举例
+++++++++++++++
# 使能边缘接口te-1/1/1的BPDU报文过滤功能::

 ConnetOS# set protocols rstp interface te-1/1/1 bpdu-filter enable true

set protocols rstp interface bpdu-guard enable
-------------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp interface bpdu-guard enable** 命令用来配置是否使能边缘接口的BPDU保护功能。

**delete protocols rstp interface bpdu-guard enable** 命令用来删除配置的边缘接口BPDU保护功能，恢复为缺省情况。

缺省情况下，边缘接口的BPDU保护功能没有使能。

命令格式
+++++++++++++++
**set protocols rstp interface** *interface-name* **bpdu-guard enable** { **false** | **true** }

**delete protocols rstp interface** *interface-name* **bpdu-guard enable**

参数说明
+++++++++++++++
*interface-name*：接口名称。

**false**：不使能边缘接口的BPDU保护功能。

**true**：使能边缘接口的BPDU保护功能。


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
边缘端口直接和用户终端相连，正常情况下，边缘端口不会收到BPDU报文。如果攻击者伪造BPDU恶意攻击交换设备，当边缘端口接收到BPDU报文时，交换设备会自动将边缘端口设置为非边缘端口，并重新进行生成树计算，从而引起网络震荡。

配置BPDU保护功能后，边缘端口将不能收到BPDU报文，从而防止伪造BPDU恶意攻击，避免网络震荡。

配置举例
+++++++++++++++
# 使能接口te-1/1/1的BPDU保护功能::

 ConnetOS# set protocols rstp interface te-1/1/1 bpdu-guard enable true

set protocols rstp interface cost
-------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp interface cost** 命令用来配置当前接口的端口路径开销。

**delete protocols rstp interface cost** 命令用来删除配置的端口路径开销，恢复为缺省值。

缺省情况下，接口的端口路径开销为2000。

命令格式
+++++++++++++++
**set protocols rstp interface** *interface-name* **cost** *cost-vlaue*

**delete protocols rstp interface** *interface-name* **cost**

参数说明
+++++++++++++++
*interface-name*：接口名称。

**cost-vlaue**：端口路径开销。整数形式，取值范围是1～200000000。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
端口的路径开销是生成树计算的重要依据。端口路径开销会影响根端口的选择，在一棵生成树中，某设备所有使能生成树协议的端口中，到根桥的路径开销最小者，就是根端口。

配置举例
+++++++++++++++
# 配置接口te-1/1/1的端口路径开销为1000::

 ConnetOS# set protocols rstp interface te-1/1/1 cost 1000

set protocols rstp interface edge enable
----------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp interface edge enable** 命令用来配置是否使能接口为边缘接口。

**delete protocols rstp interface edge enable** 命令用来删除指定的边缘接口。

缺省情况下，接口不是边缘接口。

命令格式
+++++++++++++++
**set protocols rstp interface** *interface-name* **edge enable** { **false** | **true** }

**delete protocols rstp interface** *interface-name* **edge enable**

参数说明
+++++++++++++++
*interface-name*：接口名称。

**false**：不使能接口为边缘接口。

**true**：使能接口为边缘接口。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
当接口直接与用户终端相连，而没有连接到其他交换设备或共享网段上，则该接口被称为边缘接口。由于设备无法知道接口是否直接与终端连接，边缘接口需要手动配置。

边缘端口不接收处理配置BPDU报文，不参与RSTP运算，可以由Disable直接转到Forwarding状态，且不经历时延，就像在端口上将RSTP禁用。

配置为边缘端口后，端口仍然会发送BPDU报文，这可能导致BPDU报文发送到其他网络，引起其他网络产生震荡。因此可以配置边缘端口的BPDU报文过滤功能，使边缘端口不处理、不发送BPDU报文。

配置举例
+++++++++++++++
# 配置接口te-1/1/1为边缘接口::

 ConnetOS# set protocols rstp interface te-1/1/1 edge enable true

set protocols rstp interface enable
-------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp interface enable** 命令用来配置是否使能接口下的RSTP功能。

**delete protocols rstp interface enable** 命令用来删除配置的接口下的RSTP功能，恢复为缺省值。

缺省情况下，接口下的RSTP功能是使能的。

命令格式
+++++++++++++++
**set protocols rstp interface** *interface-name* **enable** { **false** | **true** }

**delete protocols rstp interface** *interface-name* **enable**

参数说明
+++++++++++++++
*interface-name*：接口名称。

**false**：不使能接口下的RSTP功能。

**true**：使能接口下的RSTP功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 使能接口te-1/1/1的RSTP功能::

 ConnetOS# set protocols rstp interface te-1/1/1 enable true

set protocols rstp interface loop-guard enable
-------------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp interface loop-guard enable** 命令用来配置是否使能指定接口的环路保护功能。

**delete protocols rstp interface loop-guard enable** 命令用来删除配置的接口环路保护功能，恢复为缺省值。

缺省情况下，接口的环路保护功能没有使能。

命令格式
+++++++++++++++
**set protocols rstp interface** *interface-name* **loop-guard enable** { **false** | **true** }

**delete protocols rstp interface** *interface-name* **loop-guard enable**

参数说明
+++++++++++++++
*interface-name*：接口名称。

**false**：不使能接口的环路保护功能。

**true**：使能接口的环路保护功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
在运行生成树协议的网络中，根端口和其他阻塞端口状态是依靠不断接收来自上游设备的BPDU报文维持。当由于链路拥塞或者单向链路故障导致这些端口收不到来自上游设备的BPDU报文时，交换设备会重新选择根端口。原先的根端口会转变为指定端口，而原先的阻塞端口会迁移到转发状态，导致网络中可能产生环路。

为了防止以上情况发生，可部署环路保护功能。 
环路保护功能和根保护功能不能同时配置在同一端口。

配置举例
+++++++++++++++
# 使能接口te-1/1/1的环路保护功能::

 ConnetOS# set firewall forwarder fd1 action routing mode load-balance

set protocols rstp interface manual-forwarding enable
------------------------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp interface manual-forwarding enable** 命令用来配置是否使能指定接口的手动转发功能。

**delete protocols rstp interface manual-forwarding enable** 命令用来删除配置的手动转发功能，恢复为缺省值。

缺省情况下，手动转发功能不使能。

命令格式
+++++++++++++++
**set protocols rstp interface** *interface-name* **manual-forwarding enable** { **false** | **true** }

**delete protocols rstp interface** *interface-name* **manual-forwarding enable**

参数说明
+++++++++++++++
*interface-name*：接口名称。

**false**：不使能手动转发功能。

**true**：使能手动转发功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 使能接口te-1/1/1的手动转发功能::

 ConnetOS# set protocols rstp interface te-1/1/1 manual-forwarding enable true

set protocols rstp interface mode
-------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp interface mode** 命令用来配置指定接口的链路类型。

**delete protocols rstp interface mode** 命令用来删除配置的接口链路类型，恢复为缺省值。

缺省情况下，接口的链路类型为point-to-point。

命令格式
+++++++++++++++
**set protocols rstp interface** *interface-name* **mode** { **point-to-point** | **shared** }

**delete protocols rstp interface** *interface-name* **mode**

参数说明
+++++++++++++++
*interface-name*：接口名称。

**point-to-point**：点对点链路。

**shared**：共享链路。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
以点对点链路相连的两个接口如果为根端口或指定端口，则接口可以通过传送同步报文快速迁移到转发状态，减少不必要的转发延迟时间。


配置举例
+++++++++++++++
# 配置接口te-1/1/1的链路类型为point-to-point::

 ConnetOS# set protocols rstp interface te-1/1/10 mode point-to-point

set protocols rstp interface port-priority
-----------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp interface port-priority** 命令用来配置指定接口的端口优先级。

**delete protocols rstp interface port-priority** 命令用来删除配置的端口优先级，恢复为缺省值。

缺省情况下，接口的端口优先级为128。

命令格式
+++++++++++++++
**set protocols rstp interface** *interface-name* **port-priority** *port-priority*

**delete protocols rstp interface** *interface-name* **port-priority**

参数说明
+++++++++++++++
*interface-name*：接口名称。

*port-priority*：端口优先级。整数形式，取值范围是0～240。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
PID：端口ID，由4位的端口优先级与12位的端口号构成。
在参与生成树计算时，对于交换设备端口，其端口PID的大小可能会影响到是否被选举为指定端口，生成树计算时，PID小者会被选举成为指定端口。

端口优先级的改变时，生成树协议会重新计算端口的角色并进行状态迁移。

端口优先级可以影响端口在指定生成树实例和进程中的角色。用户可以在不同生成树实例或进程中对同一端口配置不同的优先级，从而使不同的用户流量沿不同的物理链路转发，完成流量的负载分担。

配置举例
+++++++++++++++
# 配置接口te-1/1/1的端口优先级为16::

 ConnetOS# set protocols rstp interface te-1/1/10 port-priority 16

set protocols rstp interface root-guard enable
-------------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp interface root-guard enable** 命令用来配置是否使能指定接口的根保护功能。

**delete protocols rstp interface root-guard enable** 命令用来删除配置的接口根保护功能，恢复为缺省值。

缺省情况下，接口下的根保护功能没有使能。

命令格式
+++++++++++++++
**set protocols rstp interface** *interface-name* **root-guard enable** { **false** | **true** }

**delete protocols rstp interface** *interface-name* **root-guard enable**

参数说明
+++++++++++++++
*interface-name*：接口名称。

**false**：不使能根保护功能。

**true**：使能根保护功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
由于维护人员的错误配置或网络中的恶意攻击，根桥收到优先级更高的BPDU，会失去根桥的地位，重新进行生成树的计算。由于拓扑结构的变化，可能造成高速流量迁移到低速链路上，引起网络拥塞。

对于使能根保护功能的指定端口，其端口角色只能保持为指定端口。一旦使能根保护功能的指定端口收到优先级更高的BPDU时，端口状态将进入Discarding状态，不再转发报文。在经过一段时间（通常为两倍的Forward Delay），如果端口一直没有再收到优先级较高的BPDU，端口会自动恢复到正常的Forwarding状态。

环路保护功能和根保护功能不能同时配置在同一端口。

配置举例
+++++++++++++++
# 使能接口te-1/1/1的根保护功能::

 ConnetOS# set protocols rstp interface te-1/1/1 root-guard enable true

set protocols rstp interface tcn-guard enable
-------------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp interface tcn-guard enable** 命令用来配置是否使能指定接口的TCN BPDU保护功能。

**delete protocols rstp interface tcn-guard enable** 命令用来删除配置的接口TCN BPDU保护功能，恢复为缺省值。

缺省情况下，接口下的TCN BPDU保护功能没有使能。

命令格式
+++++++++++++++
**set protocols rstp interface** *interface-name* **tcn-guard enable** { **false** | **true** }

**delete protocols rstp interface** *interface-name* **tcn-guard enable**

参数说明
+++++++++++++++
*interface-name*：接口名称。

**false**：不使能TCN BPDU保护功能。

**true**：使能TCN BPDU保护功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
设备在收到TCN BPDU报文后，会进行转发地址表项的刷新。当受到TCN BPDU报文攻击时，设备在短时间内会收到大量的TCN BPDU报文，频繁的表项刷新操作会给设备带来很大负担。

使能TCN BPDU保护功能，可以避免频繁地刷新转发地址表项。

配置举例
+++++++++++++++
# 使能接口te-1/1/1TCN BPDU保护功能::

 ConnetOS# set protocols rstp interface te-1/1/1 tcn-guard enable true

set protocols rstp max-age
-------------------------------------------

命令功能
+++++++++++++++
**set protocols rstp max-age** 命令用来配置设备端口上的BPDU老化时间，即定时器Max Age的时间值。

**delete protocols rstp max-age** 命令用来删除配置的，恢复为缺省值。

缺省情况下，Max Age时间为20秒。

命令格式
+++++++++++++++
**set protocols rstp max-age** *max-age*

**delete protocols rstp max-age**

参数说明
+++++++++++++++
*max-age*：端口上的BPDU老化时间。整数形式，取值范围是6～40。小于2 * (ForwardDelay - 1) 。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
在运行生成树算法的网络中，交换设备会根据端口的Max Age时间判断从上游交换设备收到的BPDU是否超时。如果BPDU超时，交换设备将该BPDU老化，同时阻塞接收该BPDU的端口，并发出以自己为根桥的BPDU。

运行STP协议的网络中非根桥设备收到配置BPDU报文后，报文中的Message Age和Max Age会进行比较：

 * 如果Message Age小于等于Max Age，则该非根桥设备继续转发配置BPDU报文。
 * 如果Message Age大于Max Age，则该配置BPDU报文将被老化，即该非根桥设备直接丢弃该配置BPDU。

如果配置BPDU是根桥发出的，则Message Age为0。否则，Message Age是从根桥发送到当前桥接收到BPDU的总时间，包括传输延时等。实际实现中，配置BPDU报文经过一个桥，Message Age增加1。

根桥的Hello Time、Forward Delay以及Max Age三个时间参数配置的数值应满足以下关系才能保证整个网络的生成树协议有效的工作，否则网络会频繁震荡。
* 2 × (Forward Delay - 1s) >= Max Age
* Max Age >= 2 × (Hello Time + 1s)


配置举例
+++++++++++++++
# 配置设备的Max Age时间为10秒::

 ConnetOS# set protocols rstp max-age 10

show protocols rstp
-------------------------------------------

命令功能
+++++++++++++++
**show protocols rstp** 命令用来查看RSTP的配置信息。

命令格式
+++++++++++++++
**show protocols rstp** [ **interface** *interface-name* { **pdu-filter** | **bpdu-guard** | **cost** | **edge** | **enable** | **loop-guard** | **manual-forwarding** | **mode** | **port-priority** | **root-guard** | **tcn-guard** } ]

参数说明
+++++++++++++++
*interface-name*：接口名称。查看指定接口的RSTP的配置信息。

**bpdu-filter**：BPDU报文过滤功能。

**bpdu-guard**：BPDU保护功能。

**cost**：端口路径开销。

**edge**：边缘接口。

**enable**：RSTP是否使能。

**loop-guard**：环路保护功能。

**manual-forwarding**：手动转发功能。

**mode**：接口的链路类型

**port-priority**：接口的端口优先级。

**root-guard enable**：接口根保护功能。

**tcn-guard enable**：TCN BPDU保护功能


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查看设备上RSTP的配置信息::

 ConnetOS 1# show protocols rstp
    enable: false
    bridge-priority: 32768
    forward-delay: 15
    hello-time: 3
    max-age: 20
    force-version: 1
    interface "te-1/1/10" {
        enable: true
        cost: 20000
        port-priority: 128
        root-guard {
            enable: true
        }
        mode: "point-to-point"
    }

