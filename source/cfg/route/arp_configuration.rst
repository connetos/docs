ARP配置
=======================================

ARP简介
---------------------------------------
在局域网中，当主机或其它网络设备有数据要发送给另一个主机或设备时，它必须知道对方的网络层地址（即IP地址）。因为IP数据报文必须封装成帧才能通过物理网络发送，所以发送方还必须有接收方的物理地址（MAC地址），所以需要一个从IP地址到物理地址的映射。

ARP（Address Resolution Protocol）地址解析协议，就是用来将IP地址解析为MAC地址的协议。
设备通过ARP解析到目的MAC地址后，将会在自己的ARP表中增加IP地址到MAC地址的映射表项，用于后续到同一目的地报文的转发。

ARP 表项分为：

 * 静态ARP表项

   由用户手动配置和维护，不会被老化，不会被动态ARP覆盖。

 * 动态ARP表项

   由ARP协议自动生成和维护，可以被老化，被新的ARP报文更新，被静态ARP覆盖。

静态ARP
+++++++++++++++++++++++++++++++++++++++
静态ARP表项可以限制和指定IP地址的设备通信时只使用指定的MAC地址，此时攻击报文无法修改此表项的IP地址和MAC地址的映射关系，从而保护了本设备和指定设备间的正常通信。

动态ARP
+++++++++++++++++++++++++++++++++++++++
ARP表项动态学习是交换机本身就具有的功能，并且设备的缺省状态即为ARP表项动态学习，不需要使用命令启动此功能。

为适应网络的变化，ARP表需要不断更新。在达到老化时间时，如果仍不得到刷新的ARP表项将被从ARP表中删除。如果在到达老化时间前记录被刷新，则重新计算老化时间。用户可以根据网络实际情况调整老化时间。

ARP代理
+++++++++++++++++++++++++++++++++++++++
如果ARP请求是从一个网络的主机发往另一个网络上的主机，连接这两个网络的设备就可以回答该请求，这个过程称作ARP代理（Proxy ARP）。ConnetOS支持ARP代理功能。

配置静态ARP
---------------------------------------
配置静态ARP表项虽然可以保护ARP表不被改写，但是配置工作量大，不适用于主机IP地址可能发生更改的网络环境，建议在比较小的网络里使用。 

#. 进入配置模式。

   ConnetOS> **configure**

#. 配置静态ARP表项。

   ConnetOS# **set protocols arp interface** *vlan-interface* **address** *ip-address* **mac-address** *mac-address*

   配置静态ARP表项时，ARP所在的vlan-interface必须已经创建好。

#. 提交配置。

   ConnetOS# **commit**

（可选）配置动态ARP老化时间
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 配置动态ARP老化时间

   ConnetOS# **set protocols arp aging-time** *aging-time*
   
   缺省情况下，ARP老化时间为1200s。

#. 提交配置。

   ConnetOS# **commit**

配置ARP代理
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 配置ARP代理

   ConnetOS# **set protocols arp interface** *vlan-interface* **proxy enable** { **false** | **true** }

   缺省情况下，ARP代理没有使能。

#. 提交配置。

   ConnetOS# **commit**

查看ARP的配置信息
---------------------------------------
执行 **show arp** 命令，可以查看ARP表项信息::

 ConnetOS> show arp
 Aging-time(seconds): 1200
 Total count        : 1
 Address          HW Address                   Type                   Interface           Age         
 ---------------  ---------------------------  ---------------------  ------------------  ------------------
 5.5.5.5          00:E0:EC:38:E1:BD            Dynamic                vlan5               550        

通过 **show route forward-host ipv4 all** 命令，查看与ARP表对应的主机路由表::

 ConnetOS> show route forward-host ipv4 all
 Address                HWaddress                  Port           
 --------------------   ------------------------   ----------------------
 5.5.5.5                00:E0:EC:38:E1:BD          te-1/1/5        
 Total host count:1

