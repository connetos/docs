Firewall命令
====================================

set firewall term
------------------------------------

命令功能
+++++++++++++++
**set firewall term** 命令用来设置过滤规则组的各项过滤规则。

**delete firewall term** 命令用来删除设置的过滤规则组。

缺省情况下，设备上没有设置好的过滤规则组。

命令格式
+++++++++++++++
**set firewall term** *term-name*\［  **cos value**\  *priority-value* | **dest-ipv4 network** *ipv4-network-address* | **dest-mac hwaddr** *mac-address* | **dscp value** *dscp-value* | **ether-type** { **name** { **arp** | **ipv4** | **rarp** } | **number** *ether-type-number* } | **l4-dest-port** { **name** { **bgp** | **bootpc** | **bootps** | **dns** | **finger** | **ftp** | **ftp-data** | **http** | **https** | **msdp** | **ntp** | **oob-ws-http** | **pop3** | **radius** | **rip** | **smtp** | **snmp** | **telnet** | **tftp** } | **number** *dest-port-number* | **range** *port-range* } | **l4- source-port** { **name** { **bgp** | **bootpc** | **bootps** | **dns** | **finger** | **ftp** | **ftp-data** | **http** | **https** | **msdp** | **ntp** | **oob-ws-http** | **pop3** | **radius** | **rip** | **smtp** | **snmp** | **telnet** | **tftp** } | **number** *source-number* | **range** *port-range* } | **protocol** { **name** { **ah** | **dstopts** | **egp** | **esp** | **fragment** | **gre** | **hop-by-hop** | **icmp** | **igmp** | **ipip** | **no-next-header** | **ospf** | **pim** | **routing** | **rsvp** | **sctp** | **tcp** | **udp** } | **number** *protocol-number* } | **source-ipv4 network** *ipv4-network-address* | **source-mac hwaddr** *mac-address* | **vlan number** *vlan-id* ］

**delete firewall term** *term-name*\［  **cos value**\  *priority-value* | **dest-ipv4 network** *ipv4-network-address* | **dest-mac hwaddr** *mac-address* | **dscp value** *dscp-value* | **ether-type** [ **name** { **arp** | **ipv4** | **rarp** } | **number** *ether-type-number* ] | **l4-dest-port** [ **name** { **bgp** | **bootpc** | **bootps** | **dns** | **finger** | **ftp** | **ftp-data** | **http** | **https** | **msdp** | **ntp** | **oob-ws-http** | **pop3** | **radius** | **rip** | **smtp** | **snmp** | **telnet** | **tftp** } | **number** *dest-port-number* | **range** *port-range* ] | **l4- source-port** [ **name** { **bgp** | **bootpc** | **bootps** | **dns** | **finger** | **ftp** | **ftp-data** | **http** | **https** | **msdp** | **ntp** | **oob-ws-http** | **pop3** | **radius** | **rip** | **smtp** | **snmp** | **telnet** | **tftp** } | **number** *source-number* | **range** *port-range* ] | **protocol** [ **name** { **ah** | **dstopts** | **egp** | **esp** | **fragment** | **gre** | **hop-by-hop** | **icmp** | **igmp** | **ipip** | **no-next-header** | **ospf** | **pim** | **routing** | **rsvp** | **sctp** | **tcp** | **udp** } | **number** *protocol-number* ] | **source-ipv4 network** *ipv4-network-address* | **source-mac hwaddr** *mac-address* | **vlan number** *vlan-id* ］

参数说明
+++++++++++++++
*term-name*：过滤规则组名称。

*priority-value*：CoS优先级。整数形式，取值范围是0～7。

*ipv4-network-address*：目的IPv4地址，IPv4地址/掩码的形式。

*mac-address*：目的MAC地址。

*dscp-value*：DSCP值。整数形式，取值范围是0～63。

*ether-type-number*：整数形式，取值范围是0～65535。

*dest-port-number*：目的端口编号。整数形式，取值范围是0～65535。

*port-range*：目的端口范围，取值形式为1:10。

*protocol-number*：协议编号。整数形式，取值范围是0～255。

*vlan-id*：VLAN ID，整数形式，取值范围是1～4094。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
配置过滤规则组的各项功能前，需要先创建过滤规则组。即必须先执行 **set firewall term** *term-name* 后，才能进行规则的设置。

只有配置了的过滤规则组，执行 **delete** 命令时才会显示。

在同一个term下，可以同时配置多种过滤规则。报文在进行规则匹配时，只要命中了一个过滤规则就不再进行匹配。

配置举例
+++++++++++++++
# 设置过滤规则组term1，用于过滤VLAN100的报文::

 ConnetOS# set firewall term term1 vlan number 100

set firewall filter input/output interface
-------------------------------------------------

命令功能
+++++++++++++++
**set firewall filter input/output interface** 命令用来将创建好的过滤策略应用到接口上。

**delete firewall filter input/output interface** 命令用来删除接口上应用的过滤策略。

缺省情况下，接口上没有应用任何过滤策略。

命令格式
+++++++++++++++
**set firewall filter** *filter-name* { **input** | **output** } { **gigabit-ethernet** | **vlan-interface** } *interface-name*

**delete firewall filter** *filter-name* [ **input** | **output** ] [ [ **gigabit-ethernet** | **vlan-interface** ] *interface-name* ]

参数说明
+++++++++++++++
*filter-name*：过滤策略名称。

**input**：将过滤策略应用在接口的入方向。

**output**：将过滤策略应用在接口的出方向。

*interface-name*：应用过滤规则的接口名称。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
同一个过滤策略可以应用在不同接口的入方向或者出方向，但是不能配置在同一个接口的入方向和出方向。

删除过滤规则时，设备上只显示已经配置的过滤内容。

配置举例
+++++++++++++++
# 将过滤规则应用在接口te-1/1/1的入方向上::

 ConnetOS# set firewall filter filter-dest input gigabit-ethernet te-1/1/1

set firewall filter matching term action
------------------------------------------------

命令功能
+++++++++++++++
**set firewall filter matching term action** 命令用来创建过滤策略，对符合过滤规则组的报文采取指定的动作。

**delete firewall filter matching term action** 命令用来删除建立的过滤策略。

缺省情况下，设备上没有建立过滤策略。

命令格式
+++++++++++++++
**set firewall filter** *filter-name* **matching term** *term-name* [ **action** { **discard** | **forward** } ]

**delete firewall filter** *filter-name* [ **matching term** *term-name* [ **action** ] ]

参数说明
+++++++++++++++
*filter-name*：过滤策略名称。

*term-name*：过滤规则组名称。

**discard**：丢弃符合过滤规则组的报文。

**forward**：转发符合过滤规则组的报文。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
过滤规则组需要先配置，才能关联成功。一个过滤策略，可以关联多个过滤规则组。

配置举例
+++++++++++++++
# 对符合过滤规则组term1的报文进行丢弃::

 ConnetOS# set firewall filter f1 matching term t1 action discard

set firewall forwarder
------------------------------------

命令功能
+++++++++++++++
**set firewall forwarder** 命令用来创建转发策略。

**delete firewall forwarder** 命令用来删除已经配置的转发策略。

缺省情况下，没有设置好的转发策略。

命令格式
+++++++++++++++
**set firewall forwarder** *forwarder-name*

**delete firewall forwarder** *forwarder-name*

参数说明
+++++++++++++++
*forwarder-name*：转发策略名称。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
配置转发策略的各项功能前，需要先创建转发策略。

配置举例
+++++++++++++++
# 设置转发策略fd1::

 ConnetOS# set firewall forwarder fd1 action classifying new-cos 5 

set firewall forwarder action classifying
--------------------------------------------------------

命令功能
+++++++++++++++
**set firewall forwarder action classifying** 命令用来设置转发策略的报文分类动作，对符合过滤规则的报文进行分类。

**delete firewall forwarder action classifying** 命令用来删除转发策略的报文分类动作。

缺省情况下，转发策略的报文分类动作没有设置。

命令格式
+++++++++++++++
**set firewall forwarder** *forwarder-name* **action classifying** { **new-cos** *cos-modify-value* | **new-dscp** *dscp-modify-value* } 

**delete firewall forwarde** *forwarder-name* **action classifying** [ **new-cos** | **new-dscp** ]

参数说明
+++++++++++++++
*forwarder-name*：转发策略名称。

*cos-modify-value*：CoS的修改值，用于修改报文优先级映射到设备优先级的值。

*dscp-modify-value*：DSCP的修改值。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 设置对符合过滤规则组的报文进行转发时，修改cos值为5::

 ConnetOS# set firewall forwarder fd1 action classifying new-cos 5

set firewall forwarder action mirroring
----------------------------------------------

命令功能
+++++++++++++++
**set firewall forwarder action mirroring** 命令用来设置转发策略的镜像动作，用于将符合指定过滤规则组的报文镜像到指定端口。

**delete firewall forwarder action mirroring** 命令用来删除转发策略的镜像动作。
缺省情况下，转发策略的镜像动作没有设置。

命令格式
+++++++++++++++
**set firewall forwarder** *forwarder-name* **action mirroring interface gigabit-ethernet** *ge-interface-name* 

**delete firewall forwarder** *forwarder-name* **action** [ **mirroring** [ **interface** [ **gigabit-ethernet** ] ] ]

参数说明
+++++++++++++++
*forwarder-name*：转发策略名称。

*ge-interface-name*：GE接口名称。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 将符合过滤规则组的报文镜像到接口te-1/1/1上::

 ConnetOS# set firewall forwarder fd1 action mirroring interface gigabit-ethernet te-1/1/1

set firewall forwarder action routing
-------------------------------------------

命令功能
+++++++++++++++
**set firewall forwarder action routing** 命令用来设置转发策略的三层转发行为，用于将符合指定过滤规则组的报文进行三层转发。

**delete firewall forwarder action routing** 命令用来删除转发策略的三层转发。

缺省情况下，转发策略的三层转发行为没有设置。

命令格式
+++++++++++++++
**set firewall forwarder** *forwarder-name* **action routing** { **mode** { **load-balance** | **redundancy** } | **nexthopv4 address** *ipv4-address* | **vlan-interface** *vlan-interfac* }

**delete firewall forwarder** *forwarder-name* **action routing** { **mode** | **nexthopv4 address** *ipv4-address* | **vlan-interface** *vlan-interface* }

参数说明
+++++++++++++++
*forwarder-name*：转发策略名称。

**mode**：设置三层转发的模式。

**load-balance**：进行负载分担转发，从多条活动链路转发。

**redundancy**：进行冗余备份转发，只从一条活动链路转发。

*ipv4-address*：目的IPv4地址，点分十进制格式。

*vlan-interface*：VLAN接口编号。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 对符合过滤规则组的报文，转发时进行负载分担转发::

 ConnetOS# set firewall forwarder fd1 action routing mode load-balance

set firewall forwarder action switching
-----------------------------------------------------

命令功能
+++++++++++++++
**set firewall forwarder action switching** 命令用来设置转发策略的二层转发行为，用于将符合指定过滤规则组的报文按照指定接口进行转发。

**delete firewall forwarder action switching** 命令用来删除设置的转发策略的二层转发行为。

缺省情况下，转发策略的二层转发行为没有设置。

命令格式
+++++++++++++++
**set firewall forwarder** *forwarder-name* **action switching interface** { **aggregate-ethernet** *ae-interface-name* | **gigabit-ethernet** *ge-interface-name* }

**delete firewall forwarder** *forwarder-name* **action** [ **switching** [ **interface** [ **aggregate-ethernet** | **gigabit-ethernet** ] ] ]

参数说明
+++++++++++++++
*forwarder-name*：转发策略名称。

*ae-interface-name*：汇聚组接口名称。

*ge-interface-name*：GE接口名称。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
此命令为覆盖式命令，即最后一次配置的接口生效。同时，同一个转发策略，只能指定一个接口进行转发，汇聚组接口和GE接口不能同时配置。


配置举例
+++++++++++++++
# 对符合过滤规则组的报文，进行二层转发时从接口te-1/1/10转进行转发::

 ConnetOS# set firewall forwarder fd1 action switching interface gigabit-ethernet te-1/1/10

set firewall forwarder input
-------------------------------------------

命令功能
+++++++++++++++
**set firewall forwarder input** 命令用来将转发策略应用到接口上。

**delete firewall forwarder input** 命令用来删除接口上应用的转发策略。

缺省情况下，接口上没有应用转发策略。

命令格式
+++++++++++++++
**set firewall forwarder** *forwarder-name* **input** { **gigabit-ethernet** *ge-interface-name* | **vlan-interface** *vlan-interface-name* }

**delete firewall forwarder** *forwarder-name* **input** [ **gigabit-ethernet** *interface-name* | **vlan-interface** vlan-interface-name ]

参数说明
+++++++++++++++
*forwarder-name*：转发策略名称。

*ge-interface-name*：GE接口编号。

*vlan-interface-name*：VLAN接口编号。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 在接口te-1/1/1上应用转发策略::

 ConnetOS# ConnetOS# set firewall forwarder fd1 input gigabit-ethernet te-1/1/1

set firewall forwarder match-mode
-------------------------------------------

命令功能
+++++++++++++++
**set firewall forwarder match-mode** 命令用来设置进行转发的报文的匹配模式。

**delete firewall forwarder match-mode** 命令用来删除配置匹配模式。

缺省情况下，对符合过滤规则的报文进行转发。

命令格式
+++++++++++++++
**set firewall forwarder** *forwarder-name* **match-mode** { **matched** | **unmatched** }

**delete firewall forwarder** *forwarder-name* [ **match-mode** ]

参数说明
+++++++++++++++
*forwarder-name*：转发策略名称。

**matched**：对符合过滤规则的报文进行策略转发。

**unmatched**：对不符合过滤规则的报文进行转发。


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 对不符合过滤规则的报文进行重定向::

 ConnetOS# set firewall forwarder fd1 match-mode unmatched

set firewall forwarder matching term
-------------------------------------------

命令功能
+++++++++++++++
**set firewall forwarder matching term**
命令用来将转发策略和过滤规则组关联。

**delete firewall forwarder matching term** 命令用来删除转发策略关联的过滤规则组。

缺省情况下，转发策略没有绑定过滤规则组。

命令格式
+++++++++++++++
**set firewall forwarder** *forwarder-name* **matching term** *term-name*

**delete firewall forwarder** *forwarder-name* **matching** [ **term** *term-name* ]

参数说明
+++++++++++++++
*forwarder-name*：转发策略名称。

*term-name*：过滤规则组名称。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 将重定向策略fd1和过滤规则组term1进行关联::

 ConnetOS# set firewall forwarder fd1 matching term term1

show firewall forwarder（运维模式）
-------------------------------------------

命令功能
+++++++++++++++
**show firewall forwarder** 命令用来查看转发策略的信息。

命令格式
+++++++++++++++
**show firewall forwarder** [ *forwarder-name* ]

参数说明
+++++++++++++++
*forwarder-name*：转发策略名称。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
必须先进行转发策略的设置，才能用show查看到相关配置。

配置举例
+++++++++++++++
# 查看转发策略fd1的配置信息::

 ConnetOS 1> show firewall forwarder
 Total ingress HW Entries    :   5120
 Consumed ingress HW Entries :   1
 Total egress HW Entries     :   1280
 Consumed egress HW Entries  :   0
 ======================== Policy Based Forwarding ====================
 Forwarder : f1

show firewall forwarder（配置模式）
-------------------------------------------

命令功能
+++++++++++++++
**show firewall forwarder** 命令用来查看转发策略的配置信息。

命令格式
+++++++++++++++
**show firewall forwarder** *forwarder-name* [ **action** { **classifying** | **mirroring** [ **interface** ] | **routing** [ **mode** | **nexthopv4 address** *ipv4-address* | **vlan-interface** *vlan-interface* ] | **switching** [ **interface** ] } | **input** [ **gigabit-ethernet** *ge-interface-name* | **vlan-interface** *vlan-interface* ] | **matching** [ **term** *term-name* ] ]

参数说明
+++++++++++++++
*forwarder-name*：转发策略名称。

*ipv4-address*：下一跳IP地址。

*ge-interface-name*：GE接口名称。

*vlan-interface*：VLAN接口。

*term-name*：过滤规则组名称。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
必须先进行转发策略的设置，才能用show查看到相关配置。

配置举例
+++++++++++++++
# 查看转发策略fd1的配置信息::

 ConnetOS# show firewall forwarder fd1
 Waiting for building configuration.
    match-mode: "matched"
    matching {
        term t1
    }
    action {
        routing {
            mode: "load-balance"
        }
    }
    input {
        gigabit-ethernet "te-1/1/1"
    }

show firewall term（配置模式）
-------------------------------------------

命令功能
+++++++++++++++
**show firewall term** 命令用来查看过滤规则组的配置信息。

命令格式
+++++++++++++++
**show firewall term** *term-name*\［ **cos value**\ *priority-value* | **dest-ipv4 network** *ipv4-network-address* | **dest-mac hwaddr** *mac-address* | **dscp value** *dscp-value* | **ether-type** { **name** { **arp** | **ipv4** | **rarp** } | **number** *ether-type-number* } | **l4-dest-port** { **name** { **bgp** | **bootpc** | **bootps** | **dhcp** | **domain** | **dns** | **finger** | **ftp** | **ftp-data** | **http** | **https** | **msdp** | **ntp** | **oob-ws-http** | **pop3** | **radius** | **rip** | **smtp** | **snmp** | **telnet** | **tftp** } | **number** *dest-port-number* | **range** *port-range* } | **l4- source-port** { **name** { **bgpv | **bootpc** | **bootps** | **dhcp** | **domain** | **finger** | **ftp** | **ftp-data** | **http** | **https** | **msdp** | **ntp** | **oob-ws-http** | **pop3** | **radius** | **rip** | **smtp** | **snmp** | **telnet** | **tftp** } | **number** *source-number* | **range** *port-range* } | **protocol** { **name** { **ah** | **dstopts** | **egp** | **esp** | **fragment** | **gre** | **hop-by-hop** | **icmp** | **igmp** | **ipip** | **no-next-header** | **ospf** | **pim** | **routing** | **rsvp** | **sctp** | **tcp** | **udp** } | **number** *protocol-number* } | **source-ipv4 network** *ipv4-network-address* | **source-mac hwaddr** *mac-address* | **vlan number** *vlan-id* ］

参数说明
+++++++++++++++
*priority-value*：CoS优先级。

*ipv4-network-address*：目的IPv4地址。

*mac-address*：目的MAC地址。

*dscp-value*：DSCP值。

*ether-type-number*：以太类型编号。

*dest-port-number*：目的端口编号。

*port-range*：目的端口范围。

*protocol-number*：协议编号。

*vlan-id*：VLAN ID。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
使用本命令进行查看时，只能看到已经配置了的term规则信息。

配置举例
+++++++++++++++
# 查看term1的配置信息::

 ConnetOS# show firewall term term1
 Waiting for building configuration.
    protocol {
        name gre
    }

show firewall filter（运维模式）
-------------------------------------------

命令功能
+++++++++++++++
**show firewall filter** 命令用来查看过滤信息。

命令格式
+++++++++++++++
**show firewall filter** [ *filter-name* ]

参数说明
+++++++++++++++
*filter-name*：已经配置的过滤策略名称。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
必须先配置过滤策略，才能用show查看。

配置举例
+++++++++++++++
# 查看设备的过滤情况::

 ConnetOS 1> show firewall filter
 Total ingress HW Entries    :   5120
 Consumed ingress HW Entries :   1
 Total egress HW Entries     :   1280
 Consumed egress HW Entries  :   0
 ======================== Policy Based Filtering ====================
 Filter : f1
     Term : t1
         Term-size       : 1
         Action          : Forward
         Matched packets : 0
         Match-condition :
             dscp :                    value 2
     Input interface     : te-1/1/10

show firewall filter（配置模式）
-------------------------------------------

命令功能
+++++++++++++++
**show firewall filter** 命令用来查看过滤策略的配置信息。

命令格式
+++++++++++++++
**show firewall filter** *filter-name* [ { **input** | **output** } [ [ **gigabit-ethernet** | **vlan-interface** ] *interface-name* ] | **matching term** *term-name* ]

参数说明
+++++++++++++++
*filter-name*：已经配置的过滤策略名称。

*interface-name*：应用过滤策略的接口名称。

*term-name*：过滤规则组名称。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
必须先进行过滤策略的设置，才能用show查看到相关配置。

配置举例
+++++++++++++++
# 对符合过滤规则组的报文，转发时进行负载分担转发::

 ConnetOS# show firewall filter f1
 Waiting for building configuration.
    term t1 {
        action: "discard"
    }
    input {
        gigabit-ethernet "te-1/1/1"
        gigabit-ethernet "te-1/1/40"
    }

