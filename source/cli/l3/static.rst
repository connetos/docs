静态路由命令
========================

set protocols static route
-------------------------------------------

命令功能
+++++++++++++++
**set protocols static route** 命令用来配置静态路由。

命令格式
+++++++++++++++
**set protocols static route** *ip-address*

参数说明
+++++++++++++++
*ip-address*：目的IP地址/掩码长度，点分十进制格式。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置到目的地址10.10.1.0/24的静态路由::

 ConnetOS# set protocols static route 10.10.1.0/24

set protocols static route metric
-------------------------------------------

命令功能
+++++++++++++++
**set protocols static route metric** 命令用来配置静态路由的度量值metric。

命令格式
+++++++++++++++
**set protocols static route** *ip-address* **metric** *metric-value*

参数说明
+++++++++++++++
*ip-address*：目的IP地址/掩码长度，点分十进制格式。

*metric-value*：整数形式，取值范围是1～65535。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置到目的地址10.10.1.0/24的静态路由的metric是5::

 ConnetOS# set protocols static route 10.10.1.0/24 metric 5

set protocols static route
-------------------------------------------

命令功能
+++++++++++++++
**set protocols static route** 命令用来配置静态路由的等价。

命令格式
+++++++++++++++
**set protocols static route** *ip-address* **qualified-next-hop** *ip-address* [ **metric** *metric-value* ]

参数说明
+++++++++++++++
*ip-address*：目的IP地址/掩码长度。点分十进制格式。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置到目的地址10.10.1.0/24的静态路由::

 ConnetOS# set protocols static route 10.10.1.0/24

show protocols static
-------------------------------------------

命令功能
+++++++++++++++
**show protocols static** 命令用来查看静态路由的配置信息。

命令格式
+++++++++++++++
**show protocols static** [ **route** *ip-address* ]

参数说明
+++++++++++++++
*ip-address*：目的IP地址/掩码长度。点分十进制格式。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查看ConnetOS上的静态路由的配置信息::

 ConnetOS# show protocols static
 Waiting for building configuration.
    route 10.10.1.0/24 {
        next-hop: 192.168.2.5
        metric: 1
    }

