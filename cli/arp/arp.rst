ARP命令
=======================

set protocols arp aging-time
-------------------------------------------

命令功能
+++++++++++++++
**set protocols arp aging-time** 命令用来配置ARP的老化时间。

**delete protocols arp aging-time** 命令用来删除配置的ARP的老化时间，恢复到缺省值。

缺省情况下，ARP的老化时间是1200秒。

命令格式
+++++++++++++++
**set protocols arp aging-time** *aging-tim**

**delete protocols arp aging-time**

参数说明
+++++++++++++++
*aging-time*：ARP的老化时间。整数形式，取值范围是300～14400，单位是秒。


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
为适应网络的变化，ARP表需要不断更新。在达到老化时间时，如果仍不得到刷新的ARP表项将被从ARP表中删除。如果在到达老化时间前记录被刷新，则重新计算老化时间。用户可以根据网络实际情况调整老化时间。 

配置举例
+++++++++++++++
# 配置ARP的老化时间为600s::

 ConnetOS# set protocols arp aging-time 600

set protocols arp interface proxy enable
-------------------------------------------

命令功能
+++++++++++++++
**set protocols arp interface proxy enable** 命令用来配置是否使能指定三层接口的ARP代理功能。

**delete protocols arp interface proxy enable** 命令用来删除接口下的ARP代理功能。

缺省情况下，ARP代理功能没有使能。

命令格式
+++++++++++++++
**set protocols arp interface** *vlan-interface* **proxy enable** { **false** | **true** }

**delete protocols arp interface** *vlan-interface* [ **proxy** [ **enable** ] ]

参数说明
+++++++++++++++
*vlan-interface*：已经配置好的三层接口。接口形式为vlan100。

**false**：去使能ARP代理功能。

**true**：使能ARP代理功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能三层接口vlan100上的ARP代理功能::

 ConnetOS# set protocols arp interface vlan100 proxy enable true

set protocols arp interface proxy address
-------------------------------------------

命令功能
+++++++++++++++
**set protocols arp interface proxy address** 命令用来配置静态ARP表项。

**delete protocols arp interface proxy address** 命令用来删除配置的静态ARP表项。

缺省情况下，没有配置静态ARP表项。

命令格式
+++++++++++++++
**set protocols arp interface** *vlan-interface* **address** *ip-address* **mac-address** *mac-address*

**delete protocols arp interface** *vlan-interface* [ **address** *ip-address* [ *mac-address* ] ]

参数说明
+++++++++++++++
*vlan-interface*：已经配置好的三层接口。接口形式为vlan100。

*mac-address*：MAC地址。形式是hh:hh:hh:hh:hh:hh，比如：00:10:94:00:00:01。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置静态ARP表项::

 ConnetOS# set protocols arp interface vlan100 address 1.1.1.1 mac-address cc:37:ab:f4:82:f3

show arp
-------------------------------------------

命令功能
+++++++++++++++
**show arp** 命令用来查看设备上的ARP信息。

命令格式
+++++++++++++++
**show arp**

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
# 查看设备上的的ARP信息::

 ConnetOS# ConnetOS> show arp
 Aging-time(seconds): 1200
 Total count        : 1
 Address          	HW Address       Type     	Interface  	Age
 ---------------  		-----------------  		-------  		---------  	-----
 5.5.5.5          	00:00:00:12:78:19  	Dynamic  	vlan5      10 	

show protocols arp
-------------------------------------------

命令功能
+++++++++++++++
**show protocols arp** 命令用来查看ARP的配置信息。

命令格式
+++++++++++++++
**show protocols arp** [ **interface** *vlan-interface* [ **address** *ip-address* | **proxy** ] ]

参数说明
+++++++++++++++
**vlan-interface**：已经配置好的三层接口。接口形式如vlan100。

**address**：查看接口上的指定IP地址的静态ARP表项。

**proxy**：查看ARP代理功能是否使能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查看用户配置的ARP信息::

 ConnetOS# show protocols arp
 Waiting for building configuration.
    aging-time: 1200
    interface vlan100 {
        address 1.1.1.1 {
            mac-address: cc:37:ab:f4:82:f3
        }
        proxy {
            enable: true
        }
    }
