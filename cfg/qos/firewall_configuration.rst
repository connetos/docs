firewall配置
=======================================

firewall简介
---------------------------------------
通过配置firewall功能，可以实现对特定报文进行过滤、重定向、策略路由、流镜像功能。

过滤规则组term，是一条或者多条规则的集合，用于识别报文流，对流量进行分类。规则是指描述报文匹配条件的判断语句，这些条件可以是报文的源地址、目的地址、端口号等。设备依照这些规则识别出特定的报文，并根据预先设定的策略对其进行处理。

报文过滤就是对符合过滤规则的流量配置过滤动作，从而达到过滤的目的。

流量重定向就是将符合流分类的流重定向到其他地方进行处理。目前支持将二层转发报文重定向到接口，即对于接收到的需要某个接口处理的报文，可以通过配置重定向到此接口。

策略路由通过识别不同的网络数据包，然后按照预先设定好的策略进行转发，从而可以有效的控制网络用户数据包的流向和行为。策略路由位于IP层，在做IP转发前，如果报文命中某个策略路由对应的规则，则要进行相应的策略路由的动作，动作包括重定向到指定下一跳，以及remark标记（如TOS、IP优先级或DSCP），然后根据重定向的下一跳代替报文的目的IP去查FIB表，做IP转发。

流镜像就是将符合过滤条件的报文流量镜像到指定端口。通过制定不同的过滤条件，对报文类型进行了精确区分，获得更精确的统计信息。

配置报文过滤功能
---------------------------------------
#. 进入配置模式。
    
   ConnetOS> **configure**

#. 设置过滤规则组。

   ConnetOS# **set firewall term** *term-name*

#. 配置过滤规则组，对需要过滤的流量进行分类。请根据网络环境需要，选择执行以下命令，进行流量的分类

   * 按照报文携带的COS值，对报文进行分类

     ConnetOS# **set firewall term** *term-name* **cos value** *priority-value*

   * 按照目的IP地址，对报文进行分类
    
     ConnetOS# **set firewall term** *term-name* **dest-ipv4 network** *ipv4-network-address*

   * 按照目的MAC地址，对报文行分类
 
     ConnetOS# **set firewall term** *term-name* **dest-mac hwaddr** *dest-mac-address*

   * 按照报文的DSCP值，对报文进行分类
    
     ConnetOS# **set firewall term** *term-name* **dscp value** *dscp-value*

   * 按照以太网报文类型，对流量进行分类
    
     ConnetOS# **set firewall term** *term-name* **ether-type** { **name** { **arp** | **ipv4** | **rarp** } | **number** *ether-type-number* }

   * 按照目的端口号，对报文进行分类

     ConnetOS# **set firewall term** *term-name* **l4-dest-port** { **name** { **bgp** | **bootpc** | **bootps** | **dns** | **finger** | **ftp** | **ftp-data** | **http** | **https** | **msdp** | **ntp** | **oob-ws-http** | **pop3** | **radius** | **rip** | **smtp** | **snmp** | **telnet** | **tftp** } | **number** *dest-port-numbe* | **range** *port-range* }

   * 按照源端口号，对报文进行分类

     ConnetOS# **set firewall term** *term-name* **l4-source-port** { **name** { **bgp** | **bootpc** | **bootps** | **dns** | **finger** | **ftp** | **ftp-data** | **http** | **https** | **msdp** | **ntp** | **oob-ws-http** | **pop3** | **radius** | **rip** | **smtp** | **snmp** | **telnet** | **tftp** } | **number** *source-port-number* | **range** *port-range* }

   * 按照协议类型，对报文进行分类
    
     ConnetOS# **set firewall term** *term-name* **protocol** { **name** { **ah** | **dstopts** | **egp** | **esp** | **fragment** | **gre** | **hop-by-hop** | **icmp** | **igmp** | **ipip** | **no-next-header** | **ospf** | **pim** | **routing** | **rsvp** | **sctp** | **tcp** | **udp** } | **number** *protocol-number* }

   * 按照源IP地址，对报文进行分类
    
     ConnetOS# **set firewall term** *term-name* **source-ipv4 network** *ipv4-network-address*

   * 按照源MAC地址，对报文行分类
      
     ConnetOS# **set firewall term** *term-name* **source-mac hwaddr** *source-mac-address*

   * 按照报文所属VLAN，对报文进行分类

     ConnetOS# **set firewall term** *term-name* **vlan number** *vlan-id*

     同一个过滤规则组，可以配置多种过滤规则。报文在进行规则匹配时，只要命中了一个过滤规则就不再进行匹配。

#. 配置对报文的过滤策略。关联过滤规则和动作，对报文进行丢弃或转发处理。

   一个过滤策略，可以同时绑定多个过滤规则组。

   ConnetOS# **set firewall filter** *filter-name* **term** *term-name* [ **action** { **discard** | **forward** } ]

#. 应用过滤策略，对接口或VLAN上的报文进行过滤。

   ConnetOS# **set firewall filter** *filter-name* { **input** | **output** } { **gigabit-ethernet** | **vlan-interface** } *interface-name*

#. 提交配置。

   ConnetOS# **commit**

配置转发策略
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 设置过滤规则组。

   ConnetOS# **set firewall term** *term-name*

#. 配置过滤规则组，对需要过滤的流量进行分类。请根据网络环境需要，选择执行以下命令，进行流量的分类

   * 按照报文携带的COS值，对报文进行分类

     ConnetOS# **set firewall term** *term-name* **cos value** *priority-value*

   * 按照目的IP地址，对报文进行分类
    
     ConnetOS# **set firewall term** *term-name* **dest-ipv4 network** *ipv4-network-address*

   * 按照目的MAC地址，对报文行分类
  
     ConnetOS# **set firewall term** *term-name* **dest-mac hwaddr** *dest-mac-address*

   * 按照报文的DSCP值，对报文进行分类
  
     ConnetOS# **set firewall term** *term-name* **dscp value** *dscp-value*

   * 按照以太网报文类型，对流量进行分类

     ConnetOS# **set firewall term** *term-name* **ether-type** { **name** { **arp** | **ipv4** | **rarp** } | **number** *ether-type-number* }

   * 按照目的端口号，对报文进行分类
    
     ConnetOS# **set firewall term** *term-name* **l4-dest-port** { **name** { **bgp** | **bootpc** | **bootps** | **dns** | **finger** | **ftp** | **ftp-data** | **http** | **https** | **msdp** | **ntp** | **oob-ws-http** | **pop3** | **radius** | **rip** | **smtp** | **snmp** | **telnet** | **tftp** } | **number** *dest-port-number* | **range** *port-range* }

   * 按照源端口号，对报文进行分类

     ConnetOS# **set firewall term** *term-name* **l4- source-port** { **name** { **bgp** | **bootpc** | **bootps** | **dns** | **finger** | **ftp** | **ftp-data** | **http** | **https** | **msdp** | **ntp** | **oob-ws-http** | **pop3** | **radius** | **rip** | **smtp** | **snmp** | **telnet** | **tftp** } | **number** *source-port-number* | **range** *port-range* }

   * 按照协议类型，对报文进行分类

     ConnetOS# **set firewall term** *term-name* **protocol** { **name** { **ah** | **dstopts** | **egp** | **esp** | **fragment** | **gre** | **hop-by-hop** | **icmp** | **igmp** | **ipip** | **no-next-header** | **ospf** | **pim** | **routing** | **rsvp** | **sctp** | **tcp** | **udp** } | **number** *protocol-number* }

   * 按照源IP地址，对报文进行分类

     ConnetOS# **set firewall term** *term-name* **source-ipv4 network** *ipv4-network-address*
   
   * 按照源MAC地址，对报文行分类

     ConnetOS# **set firewall term** *term-name* **source-mac hwaddr** *source-mac-address*

   * 按照报文所属VLAN，对报文进行分类
     
     ConnetOS# **set firewall term** *term-name* **vlan** number vlan-id

     同一个过滤规则组，可以配置多种过滤规则。报文在进行规则匹配时，只要命中了一个过滤规则就不再进行匹配。

#. 设置转发策略。

   ConnetOS# **set firewall forwarder** *forwarder-name*

#. 关联转发策略和过滤规则组，符合过滤规则的报文按照指定转发策略进行转发。

   ConnetOS# **set firewall forwarder** *forwarder-name* **matching term** *term-name*

#. 设置报文的匹配模式。

   **matched**：对符合过滤规则的报文按照转发行为进行转发。

   **unmatched**：对不符合过滤规则的报文按照转发行为进行转发。

   ConnetOS# **set firewall forwarder** *forwarder-name* **match-mode** { **matched** | **unmatched** }

#. 根据网络需要，选择执行以下命令，设置报文转发行为。

   * 设置报文分类动作，修改报文的设备优先级。

     ConnetOS# **set firewall forwarder** *forwarder-name* **action classifying** { **new-cos** *cos-modify-value* | **new-dscp** *dscp-modify-value* }

   * 设置对报文进行镜像。

     ConnetOS# **set firewall forwarder** *forwarder-name* **action mirroring interface** { **aggregate-ethernet** *ae-interface-name* | **gigabit-ethernet** *ge-interface-name* } 

   * 设置对报文进行三层转发。

     ConnetOS# **set firewall forwarder** *forwarder-name* **action routing** { **mode** { **load-balance** | **redundancy** } | **nexthopv4 address** *ipv4-address* | **vlan-interface** *vlan-interface* }

   * 设置对报文进行二层转发。
    
     ConnetOS# **set firewall forwarder** *forwarder-name* **action switching interface** { **aggregate-ethernet** *ae-interface-name* | **gigabit-ethernet** *ge-interface-name* }

#. 执行命令，将转发策略应用到入接口上。接口上接收的报文将按照转发策略进行转发。

   ConnetOS# **set firewall forwarder** *forwarder-name* **input** { **gigabit-ethernet** *ge-interface-name* | **vlan-interface** *vlan-interface-name* }

#. 提交配置。

   ConnetOS# **commit**

查看配置结果
---------------------------------------
查看过滤规则组的相关配置信息::

 ConnetOS# show firewall term term1
 Waiting for building configuration.
     protocol {
         name gre
 }

查看过滤策略的相关配置信息::

 ConnetOS# show firewall filter f1
 Waiting for building configuration.
     term t1 {
         action: "discard"
     }
     input {
         gigabit-ethernet "te-1/1/1"
         gigabit-ethernet "te-1/1/40"
     }

查看转发策略的相关配置信息::

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

