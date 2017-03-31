LLDP命令
==================================

set protocols lldp advertisement-interval
-------------------------------------------

命令功能
+++++++++++++++
**set protocols lldp advertisement-interval** 命令用来配置发送LLDP报文的时间间隔。

**set protocols lldp advertisement-interval** 命令用来删除配置的发送LLDP报文的时间间隔，恢复到缺省值。

缺省情况下，发送LLDP报文的时间间隔是30秒。

命令格式
+++++++++++++++
**set protocols lldp advertisement-interval** *advertisement-interval*

**delete set protocols lldp advertisement-interval**

参数说明
+++++++++++++++
*advertisement-interval*：发送LLDP报文的时间间隔。整数形式，取值范围为5～32768，单位是秒。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
发送LLDP报文的时间间隔是指设备LLDP状态一直没有发生变化或没有发现新的邻居的情况下，接口周期性的向邻居设备发送LLDP报文的时间间隔。配置该时间间隔后，每一个使能LLDP功能的接口都以该间隔为周期向邻居设备发送LLDP报文，但是各个接口发送报文的时间点可以不一致。

当调整网络拓扑的发现频率时，需要使用该命令修改发送LLDP报文的时间间隔。

配置举例
+++++++++++++++
# 配置发送LLDP报文的时间间隔为40秒::

 ConnetOS# set protocols lldp advertisement-interval 40

set protocols lldp enable
-------------------------------------------

命令功能
+++++++++++++++
**set protocols lldp enable** 命令用来配置是否使能全局的LLDP功能。

**delete protocols lldp enable** 命令用来删除LLDP功能。

缺省情况下，全局LLDP功能已经使能。

命令格式
+++++++++++++++
**set protocols lldp enable** { **false** | **true** }

**delete protocols lldp enable**

参数说明
+++++++++++++++
**false**：去使能全局LLDP功能。

**true**：使能全局LLDP功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
使能全局的LLDP功能后，缺省情况下所有接口的LLDP功能都处于使能状态。

配置举例
+++++++++++++++
# 去使能全局的LLDP功能::

 ConnetOS# set protocols lldp enable false

set protocols lldp hold-time-multiplier
-------------------------------------------

命令功能
+++++++++++++++
**set protocols lldp hold-time-multiplier** 命令用来配置邻居信息在本设备上的老化时间的时间倍数。

**delete protocols lldp hold-time-multiplier** 命令用来恢复邻居设备信息在本设备中保持的时间倍数的缺省值。

缺省情况下，邻居设备信息在本设备中保持的时间倍数是4。

命令格式
+++++++++++++++
**set protocols lldp hold-time-multiplier** *hold-time-multiplier*
**delete protocols lldp hold-time-multiplier**

参数说明
+++++++++++++++
*hold-time-multiplier*：邻居信息在本设备保存的时间倍数。整数形式，取值范围为1～300。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
邻居信息在本地设备上的老化时间由Time to Live TLV中TTL的值来确定， 老化时间的计算公式是：TTL = Min (65535, (interval × hold))

TTL代表Time to Live，表示设备信息在邻居设备中保持的时间，取65535和interval × hold中的最小值。interval代表设备向邻居设备发送LLDP报文的时间周期，hold代表设备信息在邻居设备中保持的时间倍数。

当原来使能LLDP功能的设备去使能LLDP功能后，它的邻居设备不会马上老化掉该设备的信息，而是在等待TTL时间后再进行老化，以防止网络拓扑频繁变更。

配置举例
+++++++++++++++
# 配置邻居设备信息在本设备中中保持的时间倍数为10::

 ConnetOS# set protocols lldp hold-time-multiplier 10

set protocols lldp interface status
-------------------------------------------

命令功能
+++++++++++++++
**set protocols lldp interface status** 命令用来配置接口的LLDP工作模式。

**delete protocols lldp interface status** 命令用来将LLDP工作模式恢复到缺省值。 

缺省情况下，接口下LLDP的工作模式为Tx/Rx模式。

命令格式
+++++++++++++++
**set protocols lldp interface** *interface-name* **status** { **disabled** | **rx-only** | **tx-only** | **tx-rx** }

**delete protocols lldp interface** *interface-name* **status**

参数说明
+++++++++++++++
**interface-name**：接口名称。此接口既可以是单接口，也可以是汇聚接口组。

**disabled**：既不发送也不接收LLDP报文。

**rx-only**：Rx模式，即只接收LLDP报文。

**tx-only**：Tx模式，即只发送LLDP报文。

**tx-rx**：Tx/Rx模式，即既可以接收又可以发送LLDP报文。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
通过配置LLDP的工作模式，使得指定接口只能工作在指定的工作模式，可以有效减少网络中LLDP报文的数量，降低系统负担，保证用户其他业务的正常运行。

配置举例
+++++++++++++++
# 配置接口te-1/1/1上的LLDP功能工作在Rx模式::

 ConnetOS# set protocols lldp interface te-1/1/1 status rx-only

set protocols lldp reinit-delay
-------------------------------------------

命令功能
+++++++++++++++
**set protocols lldp reinit-delay** 命令用来配置当LLDP工作模式变化时，接口初始化延迟时间。

**delete protocols lldp reinit-delay** 命令用来删除配置的接口初始化延迟时间，恢复到缺省值。

缺省情况下，LLDP工作模式变化，接口初始化的延迟时间为2秒。

命令格式
+++++++++++++++
**set protocols lldp reinit-delay** *reinit-delay*

**delete protocols lldp reinit-delay**

参数说明
+++++++++++++++
*reinit-delay*：接口初始化的延迟时间。整数形式，取值范围为2～5，单位是秒。


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
当端口的LLDP工作模式发生变化时，端口将对协议状态机进行初始化操作。为了避免端口模式频繁改变导致端口不断初始化，可以配置端口的初始化延迟时间，即当端口工作模式改变时延迟一段时间再执行初始化操作。

配置举例
+++++++++++++++
# 设置LLDP重新使能的延迟时间为3秒::

 ConnetOS# set protocols lldp reinit-delay 3

set protocols lldp tlv-select enable
-------------------------------------------

命令功能
+++++++++++++++
**set protocols lldp tlv-select enable** 命令用来配置是否使能发布指定类型的TLV。

**delete protocols lldp tlv-select enable** 命令用来删除发布指定类型的TLV。

缺省情况下，发布所有类型的TLV。

命令格式
+++++++++++++++
**set protocols lldp tlv-select** { **mac-phy-cfg** | **management-address** | **port-description** | **port-vlan** | **system-capabilities** | **system-description** | **system-name** } **enable** { **false** | t**rue** }

**delete protocols lldp tlv-select** { **mac-phy-cfg** | **management-address** | **port-description** | **port-vlan** | **system-capabilities** | **system-description** | **system-name** } **enable**

参数说明
+++++++++++++++
**mac-phy-cfg**：MAC/PHY Configuration/Status TLV，用于标识端口的速率和双工状态、是否支持端口速率自动协商、是否已使能自动协商功能以及当前的速率和双工状态。

**management-address**：Management Address TLV，管理地址的TLV。管理地址是供网络管理系统标识网络设备并进行管理的地址。管理地址可以明确地标识一台设备，有利于网络拓扑的绘制，便于网络管理。

**port-description**：Port Description TLV，用于描述端口。

**port-vlan**：Port VLAN TLV，一个LLDPDU中只允许携带一个此类型的TLV。

**system-capabilities**：System Capabilities TLV，用于描述系统的主要功能及已经使能的功能。

**system-description**：System Description TLV，用于对系统进行描述。

**system-name**：System Name TLV，用户描述系统名称。

**false**：不使能发布TLV。

**true**：使能发布TLV。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 不使能发布MAC/PHY Configuration/Status TLV::

 ConnetOS# set protocols lldp tlv-select mac-phy-cfg enable false


set protocols lldp transmit-delay
-------------------------------------------

命令功能
+++++++++++++++
**set protocols lldp transmit-delay** 命令用来配置本设备向邻居设备发送LLDP报文的延迟时间。

**delete protocols lldp transmit-delay** 命令用来删除用户配置的发送LLDP报文的延迟时间，恢复到缺省值。

缺省情况下，发送LLDP报文的延迟时间为2秒。

命令格式
+++++++++++++++
**set protocols lldp transmit-delay** *transmit-delay*
**delete protocols lldp transmit-delay**

参数说明
+++++++++++++++
*transmit-delay*：发送LLDP报文的延迟时间。整数形式，取值范围是1～8192，单位是秒。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
发送LLDP报文的延迟时间是指设备状态频繁发生变化的时候，接口模块向邻居设备发送LLDP报文的最小延迟时间。设备配置该延迟时间之后，每一个使能LLDP功能的接口都以该值为最小延迟时间向邻居节点发送LLDP报文，但是各个接口发送报文的时间点可以不一致。

当设备的状态信息频繁发生变化的时候可以通过增大该延迟时间来减少设备频繁向邻居设备发送信息，以达到抑制拓扑振荡目的。

配置举例
+++++++++++++++
# 设置设备LLDP报文的延迟时间为10秒::

 ConnetOS# set protocols lldp transmit-delay 10

show protocols lldp
-------------------------------------------

命令功能
+++++++++++++++
**show protocols lldp** 命令用来LLDP的配置信息。

命令格式
+++++++++++++++
**show protocols lldp** \ [ [ **tlv-select** \ { **mac-phy-cfg** | **management-address** | **port-description** | **port-vlan** | **system-capabilities** | **system-description** | **system-name** }] ]

参数说明
+++++++++++++++
**tlv-select**：查看指定类型的TLV是否发布。

**mac-phy-cfg**：MAC/PHY Configuration/Status TLV，用于标识端口的速率和双工状态、是否支持端口速率自动协商、是否已使能自动协商功能以及当前的速率和双工状态。

**management-address**：Management Address TLV，管理地址的TLV。管理地址是供网络管理系统标识网络设备并进行管理的地址。管理地址可以明确地标识一台设备，有利于网络拓扑的绘制，便于网络管理。

**port-description**：Port Description TLV，用于描述端口。

**port-vlan**：Port VLAN TLV，一个LLDPDU中只允许携带一个此类型的TLV。

**system-capabilities**：System Capabilities TLV，用于描述系统的主要功能及已经使能的功能。

**system-description**：System Description TLV，用于对系统进行描述。

**system-name**：System Name TLV，用户描述系统名称。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查看LLDP功能的配置信息::

 ConnetOS 1# show protocols lldp
 Waiting for building configuration.
    enable: true
    advertisement-interval: 30
    reinit-delay: 2
    transmit-delay: 2
    hold-time-multiplier: 4
    tlv-select {
        mac-phy-cfg {
            enable: true
        }
        management-address {
            enable: true
        }
        port-description {
            enable: true
        }
        port-vlan {
            enable: true
        }
        system-capabilities {
            enable: true
        }
        system-description {
            enable: true
        }
        system-name {
            enable: true
        }
    }
