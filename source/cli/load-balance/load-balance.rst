负载分担命令
==============================

set forwarding-options load-balance ecmp algorithm
---------------------------------------------------------

命令功能
+++++++++++++++
**set forwarding-options load-balance ecmp algorithm** 命令用来配置等值负载均衡时的哈希（hash）算法。

**delete forwarding-options load-balance ecmp algorithm** 用来删除等值负载均衡的哈希算法。

缺省情况下，等值负载均衡采用的哈希算法为0，即可以进行二次哈希。

命令格式
+++++++++++++++
**set forwarding-options load-balance ecmp algorithm** *algorithm-num*

**delete forwarding-options load-balance ecmp algorithm**


参数说明
+++++++++++++++
algorithm-num：哈希算法，整数形式，取值范围是0～8。


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
本命令为覆盖式命令，最后一次配置生效。

配置hash算法为0表示可以进行二次哈希（进行二次哈希的设备必须为相同设备型号）。
1～8为设备内部算法，哈希算法设置为非0后，请根据具体的哈希后的效果进行调整哈希算法的值。

配置举例
+++++++++++++++
# 设置等值负载均衡哈希算法值为4::

 ConnetOS# set forwarding-options load-balance ecmp algorithm 4

set forwarding-options load-balance ecmp key
--------------------------------------------------

命令功能
+++++++++++++++
**set forwarding-options load-balance ecmp key** 命令用来配置用于等值负载均衡的哈希因子。

**delete forwarding-options load-balance ecmp key** 用来删除配置的哈希因子。

缺省情况下，哈希因子都是使能的，即全部用于进行哈希算法。

命令格式
+++++++++++++++
**set forwarding-options load-balance ecmp key** { **dest-ip** | **dest-mac** | **ether-type** | **ingress-interface** | **ip-protocol** | **l4-dest-port** | **4-source-port** | **source-ip** | **source-mac** | **vlan-id** } **enable** { **false** | **true** }

**delete forwarding-options load-balance ecmp key** { **dest-ip** | **dest-mac** | **ether-type** | **ingress-interface** | **ip-protocol** | **l4-dest-port** | **l4-source-port** | **source-ip** | **source-mac** | **vlan-id** } **enable**

参数说明
+++++++++++++++
**dest-ip**：目的IP地址。

**dest-mac**：目的MAC地址。

**ether-type**：以太类型。

**ingress-interface**：报文流入接口。

**ip-protocol**：IP协议。

**l4-dest-port**：目的端口号。

**l4-source-port**：源端口号。

**source-ip**：源IP地址。

**source-mac**：源MAC地址。

**vlan-id**：VLAN ID。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
负载均衡依靠哈希运算实现，哈希算法的输入是各报文的特征值，称之为哈希因子。如果哈希因子散列性较好，则哈希算法得出的负载分担将会更均匀。可作为哈希因子的特征值有报文的源目的MAC地址，源目的IP地址，源目的端口号和协议号。

配置举例
+++++++++++++++
# 设置ip-protocol不参与哈希运算::

 ConnetOS# set forwarding-options load-balance ecmp key ip-protocol enable false 

set forwarding-options load-balance ecmp max-path
------------------------------------------------------------

命令功能
+++++++++++++++
**set forwarding-options load-balance ecmp max-path** 命令用来配置等值负载均衡时的最大链路数，即参与负载均衡的链路数。

**delete forwarding-options load-balance ecmp max-path** 用来删除等值负载均衡时的最大链路数。

缺省情况下，等值负载均衡最大链路数是32。

命令格式
+++++++++++++++
**set forwarding-options load-balance ecmp max-path** *max-path*

**delete forwarding-options load-balance ecmp max-path**

参数说明
+++++++++++++++
max-path：整数形式，取值范围是1～32。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
本命令为覆盖式命令，最后一次配置生效。

配置举例
+++++++++++++++
# 设置等值负载均衡时最大链路为8::

 ConnetOS# set forwarding-options load-balance ecmp max-path 8

set forwarding-options load-balance ecmp tunnel
------------------------------------------------------

命令功能
+++++++++++++++
**set forwarding-options load-balance ecmp tunnel** 命令用来配置Tunnel报文用于等值负载均衡的哈希因子。

**delete forwarding-options load-balance ecmp tunnel** 用来删除配置的Tunnel报文的哈希因子。

缺省情况下，使用Tunnel报文外层报文头内容做哈希运算。

命令格式
+++++++++++++++
**set forwarding-options load-balance ecmp tunnel** { **inner** | **outer** }

**delete forwarding-options load-balance ecmp tunnel**

参数说明
+++++++++++++++
**inner**：使用Tunnel报文内层报文头内容做哈希运算。

**outer**：使用Tunnel报文外层报文头内容做哈希运算。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
本命令为覆盖式命令，最后一次的配置生效。

配置举例
+++++++++++++++
# 设置使用Tunnel报文内层报文头内容做哈希运算::

 ConnetOS# set forwarding-options load-balance ecmp tunnel inner

show forwarding-options load-balance ecmp
-------------------------------------------

命令功能
+++++++++++++++
**show forwarding-options load-balance ecmp** 命令用来查看等值负载均衡时哈希算法的配置信息。

命令格式
+++++++++++++++
**show forwarding-options load-balance ecmp** [ **key** [ **dest-ip** | **dest-mac** | **ether-type** | **ingress-interface** | **ip-protocol** | **l4-dest-port** | **l4-source-port** | **source-ip** | **source-mac** | **vlan-id** ] ]

参数说明
+++++++++++++++
**dest-ip**：目的IP地址。

**dest-mac**：目的MAC地址。

**ether-type**：以太类型。

**ingress-interface**：报文流入接口。

**ip-protocol**：IP协议。

**l4-dest-port**：目的端口号。

**l4-source-port**：源端口号。

**source-ip**：源IP地址。

**source-mac**：源MAC地址。

**vlan-id**：VLAN ID。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查看等值负载均衡时哈希算法的配置信息::

 ConnetOS# show forwarding-options load-balance ecmp
 Waiting for building configuration.
    algorithm: "0"
    max-path: 32
    key {
        ingress-interface {
            enable: true
        }
        source-mac {
            enable: true
        }
        dest-mac {
            enable: true
        }
        ether-type {
            enable: true
        }
        vlan-id {
            enable: true
        }
        ip-protocol {
            enable: false
        }
        source-ip {
            enable: true
        }
        dest-ip {
            enable: true
        }
        l4-source-port {
            enable: true
        }
        l4-dest-port {
            enable: true
        }
    }
    tunnel: "outer"

set forwarding-options load-balance lag algorithm
-------------------------------------------------------

命令功能
+++++++++++++++
**set forwarding-options load-balance lag algorithm** 命令用来配置汇聚组负载均衡的哈希算法。

**delete forwarding-options load-balance lag algorithm** 用来删除负载均衡的哈希算法。

缺省情况下，负载均衡采用的哈希算法为0，即可以进行二次哈希。

命令格式
+++++++++++++++
**set forwarding-options load-balance lag algorithm** *algorithm-num*

**delete forwarding-options load-balance lag algorithm**

参数说明
+++++++++++++++
*algorithm-num*：哈希算法，整数形式，取值范围是0～8。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
本命令为覆盖式命令，最后一次配置生效。

配置hash算法为0表示可以进行二次哈希（进行二次哈希的设备必须为相同设备型号）。
1～8为设备内部算法，哈希算法设置为非0后，请根据具体的哈希后的效果进行调整哈希算法的值。

配置举例
+++++++++++++++
# 设置汇聚组负载均衡的哈希算法值为4::

 ConnetOS# set forwarding-options load-balance lag algorithm 4

set forwarding-options load-balance lag key
-------------------------------------------------

命令功能
+++++++++++++++
**set forwarding-options load-balance lag key** 命令用来配置用于汇聚组负载均衡的哈希因子。

**delete forwarding-options load-balance lag key** 用来删除配置的哈希因子。

缺省情况下，哈希因子都是使能的，即全部用于进行哈希算法。

命令格式
+++++++++++++++
**set forwarding-options load-balance lag key** { **dest-ip** | **dest-mac** | **ether-type** | **ingress-interface** | **ip-protocol** | **l4-dest-port** | **l4-source-port** | **source-ip** | **source-mac** | **vlan-id** } **enable** { **false** | **true** }

**delete forwarding-options load-balance lag key** { **dest-ip** | **dest-mac** | **ether-type** | **ingress-interface** | **ip-protocol** | **l4-dest-port** | **l4-source-port** | **source-ip** | **source-mac** | **vlan-id** } **enable**


参数说明
+++++++++++++++
**dest-ip**：目的IP地址。

**dest-mac**：目的MAC地址。

**ether-type**：以太类型。

**ingress-interface**：报文流入接口。

**ip-protocol**：IP协议。

**l4-dest-port**：目的端口号。

**l4-source-port**：源端口号。

**source-ip**：源IP地址。

**source-mac**：源MAC地址。

**vlan-id**：VLAN ID。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
负载均衡依靠哈希运算实现，哈希算法的输入是各报文的特征值，称之为哈希因子。如果哈希因子散列性较好，则哈希算法得出的负载分担将会更均匀。可作为哈希因子的特征值有报文的源目的MAC地址，源目的IP地址，源目的端口号和协议号。

配置举例
+++++++++++++++
# 设置ether-type不参与哈希运算::

 ConnetOS# set forwarding-options load-balance lag key ether-type enable false

set forwarding-options load-balance lag symmetric
-------------------------------------------------------

命令功能
+++++++++++++++
**set forwarding-options load-balance lag symmetric** 命令用来配置对称哈希。

**delete forwarding-options load-balance lag symmetric** 用来删除配置的对称哈希。

缺省情况下，对称哈希没有使能。

命令格式
+++++++++++++++
**set forwarding-options load-balance lag symmetric enable** [ **false** | **true** ]

**delete forwarding-options load-balance lag symmetric**

参数说明
+++++++++++++++
**false**：不使能对称哈希。

**true**：使能对称哈希。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
本命令为覆盖式命令，最后一次配置生效。

配置举例
+++++++++++++++
# 设置使能对称哈希::

 ConnetOS# set forwarding-options load-balance lag symmetric enable true 

set forwarding-options load-balance lag tunnel
--------------------------------------------------------

命令功能
+++++++++++++++
**set forwarding-options load-balance lag tunnel** 命令用来配置Tunnel报文用于等值负载均衡的哈希因子。

**delete forwarding-options load-balance lag tunnel** 用来删除配置的Tunnel报文的哈希因子。

缺省情况下，使用Tunnel报文外层报文头内容做哈希运算。

命令格式
+++++++++++++++
**set forwarding-options load-balance lag tunnel** { **inner** | **outer** }

**delete forwarding-options load-balance lag tunnel**

参数说明
+++++++++++++++
**inner**：使用Tunnel报文内层报文头内容做哈希运算。

**outer**：使用Tunnel报文外层报文头内容做哈希运算。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
本命令为覆盖式命令，最后一次的配置生效。

配置举例
+++++++++++++++
# 设置使用Tunnel报文内层报文头内容做哈希运算::

 ConnetOS# set forwarding-options load-balance lag tunnel inner

show forwarding-options load-balance lag tunnel
-----------------------------------------------------

命令功能
+++++++++++++++
**show forwarding-options load-balance lag** 命令用来查看负载均衡时LAG链路哈希算法的配置信息。

命令格式
+++++++++++++++
**show forwarding-options load-balance lag** [ **key** [ **dest-ip** | **dest-mac** | **ether-type** | **ingress-interface** | **ip-protocol** | **l4-dest-port** | **l4-source-port** | **source-ip** | **source-mac** | **vlan-id** ] | **symmetric** ]

参数说明
+++++++++++++++
**dest-ip**：目的IP地址。

**dest-mac**：目的MAC地址。

**ether-type**：以太类型。

**ingress-interface**：报文流入接口。

**ip-protocol**：IP协议。

**l4-dest-port**：目的端口号。

**l4-source-port**：源端口号。

**source-ip**：源IP地址。

**source-mac**：源MAC地址。

**vlan-id**：VLAN ID。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查看负载均衡时LAG链路哈希算法的配置信息::

 ConnetOS# show forwarding-options load-balance lag
 Waiting for building configuration.
    algorithm: "0"
    key {
        ingress-interface {
            enable: true
        }
        source-mac {
            enable: true
        }
        dest-mac {
            enable: true
        }
        ether-type {
            enable: true
        }
        vlan-id {
            enable: true
        }
        ip-protocol {
            enable: true
        }
        source-ip {
            enable: true
        }
        dest-ip {
            enable: true
        }
        l4-source-port {
            enable: true
        }
        l4-dest-port {
            enable: true
        }
    }
    tunnel: "outer"
    symmetric {
        enable: false
    }

