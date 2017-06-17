BGP命令
=======================================

set protocols bgp 4byte-as-numbers enable
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp 4byte-as-numbers enable** 命令用来设置BGP使用4字节的AS编号。

**delete protocols bgp 4byte-as-numbers enable** 命令用来删除设置的AS编号，恢复为缺省值。

缺省情况下，不使用4字节的AS编号，使用2字节的AS编号。

命令格式
+++++++++++++++
**set protocols bgp 4byte-as-numbers enable** { **false** | **true** }

**delete protocols bgp 4byte-as-numbers enable**

参数说明
+++++++++++++++
**false**：不使用4字节的AS编号，即使用2字节的AS编号。

**true**：使用4字节的AS编号。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 使用4字节的AS编号::

 ConnetOS# set protocols bgp 4byte-as-numbers enable true

set protocols bgp bgp-id
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp bgp-id** 命令用来设置BGP设备的Router ID。

**delete protocols bgp bgp-id** 命令用来删除配置的BGP设备的Router ID，恢复为缺省值。

缺省情况下，BGP设备没有设置Router ID。

命令格式
+++++++++++++++
**set protocols bgp bgp-id** *bgp-id*

**delete protocols bgp bgp-id**

参数说明
+++++++++++++++
*bgp-id*：本BGP设备的Router ID，必须是IPv4地址的形式。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 设备本设备的Router ID为1.1.1.1::

 ConnetOS# set protocols bgp bgp-id 1.1.1.1

set protocols bgp confederation enable
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp confederation enable** 命令用来配置是否使能BGP联盟。

**delete protocols bgp confederation enable** 命令用来删除配置的BGP联盟，恢复为缺省值。

缺省情况下，BGP联盟是使能的。

命令格式
+++++++++++++++
**set protocols bgp confederation enable** { **false** | **true** }

**delete protocols bgp confederation enable** 

参数说明
+++++++++++++++
**false**：不使能BGP联盟。

**true**：使能BGP联盟。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 使能BGP联盟::

 ConnetOS# set protocols bgp confederation enable true

set protocols bgp confederation identifier
-------------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp confederation identifier** 命令用来设置联盟ID。

**delete protocols bgp confederation identifier** 命令用来删除设置的联盟ID。

缺省情况下，没有设置联盟ID。

命令格式
+++++++++++++++
**set protocols bgp confederation identifier** *confederation-id*

**delete protocols bgp confederation identifier** 

参数说明
+++++++++++++++
*confederation-id*：联盟ID。整数形式，取值范围1～4294967295。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
联盟ID相当于整个自治系统的编号，其他相关外部AS在指定对等体所在的AS号时，要指定这个联盟ID。属于同一个联盟的所有子自治系统都必须指定相同的联盟ID。

配置举例
+++++++++++++++
# 设置联盟ID为90::

 ConnetOS# set protocols bgp confederation identifier 90

set protocols bgp damping enable
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp damping enable** 命令用来配置是否使能路由衰减功能。

**delete protocols bgp damping enable** 命令用来删除配置的路由衰减功能，恢复为缺省值。

缺省情况下，路由衰减功能是使能的。

命令格式
+++++++++++++++
**set protocols bgp damping enable** { **false** | **true** }

**delete protocols bgp damping enable**

参数说明
+++++++++++++++
**false**：不使能路由衰减功能。

**true**：使能路由衰减功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能路由衰减功能::

 ConnetOS# set protocols bgp damping enable

set protocols bgp damping half-life
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp damping half-life** 命令用来配置可达路由的半衰期。

**delete protocols bgp damping half-life** 命令用来取消配置的可达路由的半衰期，恢复为缺省值。

缺省情况下，可达路由的半衰期为15分钟。

命令格式
+++++++++++++++
**set protocols bgp damping half-life** *half-life*

**delete protocols bgp damping half-life** 

参数说明
+++++++++++++++
*half-life*：可达路由的半衰期。整数形式，取值范围是1～4294967295。单位是分钟。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置路由衰减的半衰期为10分钟::

 ConnetOS# set protocols bgp damping half-life 10

set protocols bgp damping max-suppress
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp damping max-suppress** 命令用来配置路由衰减是的抑制时间。

**delete protocols bgp damping max-suppress** 命令用来删除配置的抑制时间，恢复为缺省值。

缺省情况下，抑制时间为60分钟。

命令格式
+++++++++++++++
**set protocols bgp damping max-suppress** *max-suppress-time*

**delete protocols bgp damping max-suppress** 

参数说明
+++++++++++++++
*max-suppress-time*：抑制时间，即路由从被抑制到恢复可用的时间。整数形式，取值范围是1～4294967295。单位是分钟。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 配置抑制时间为40分钟::

 ConnetOS# set protocols bgp damping max-suppress 40 

set protocols bgp damping reuse
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp damping reuse** 命令用来设置路由衰减时路由解除抑制状态时的再使用阈值。

**delete protocols bgp damping reuse** 命令用来删除配置的再使用阈值，恢复为缺省值。

缺省情况下，再使用阈值是750。

命令格式
+++++++++++++++
**set protocols bgp damping reuse** *reuse-value*

**delete protocols bgp damping reuse** 

参数说明
+++++++++++++++
*reuse-value*：指定路由解除抑制状态的阈值。当惩罚降低到该值以下，路由就被再使用。整数形式，取值范围是1～4294967295。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 配置路由解除抑制状态时的再使用阈值为1000::

 ConnetOS# set protocols bgp damping reuse 10000

set protocols bgp damping suppress
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp damping suppress** 命令用来配置路由进入抑制状态的抑制阈值。

**delete protocols bgp damping suppress** 命令用来删除配置的抑制阈值，恢复为缺省值。

缺省情况下，抑制阈值是3000。

命令格式
+++++++++++++++
**set protocols bgp damping suppress** *suppress-value*

**delete protocols bgp damping suppress**

参数说明
+++++++++++++++
*suppress-value*：指定路由进入抑制状态的阈值。整数形式，取值范围是1～4294967295。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
当惩罚值超过抑制阈值时，路由受到抑制，不再加入到路由表中，也不再向其他BGP对等体发布更新报文。

抑制阈值必须比再使用阈值大。

配置举例
+++++++++++++++
# 设置抑制阈值为5000::

 ConnetOS# set protocols bgp damping suppress 50000

set protocols bgp local-as
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp local-as** 命令过用来设置AS编号。

**delete protocols bgp local-as** 命令用来删除配置的AS编号。

缺省情况下，没有设置AS编号。

命令格式
+++++++++++++++
**set protocols bgp local-as** *as-id*

**delete protocols bgp local-as**

参数说明
+++++++++++++++
*as-id*：AS编号。整数形式，取值范围是1～4294967295。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 设置设备的AS编号为1::

 ConnetOS# set protocols bgp local-as 1

set protocols bgp route-reflector enable
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp route-reflector enable** 命令用来配置是否使能路由反射器。

**delete protocols bgp route-reflector enable** 命令用来删除配置的路由反射器功能，恢复为缺省值。

缺省情况下，路由反射器是使能的。

命令格式
+++++++++++++++
**set protocols bgp route-reflector enable** { **false** | **true** } 

**delete protocols bgp route-reflector enable**

参数说明
+++++++++++++++
**false**：不使能路由反射器。

**true**：使能路由反射器。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 使能路由反射器::

 ConnetOS# set protocols bgp route-reflector enable true

set protocols bgp route-reflector cluster-id
-------------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp route-reflector cluster-id** 命令用来配置路由反射器的集群ID。

**delete protocols bgp route-reflector cluster-id** 命令用来删除配置的集群ID，恢复为缺省值。

缺省情况下，每个路由反射器使用自己的Router ID作为集群ID。

命令格式
+++++++++++++++
**set protocols bgp route-reflector cluster-id** *cluster-id*

**delete protocols bgp route-reflector cluster-id**

参数说明
+++++++++++++++
*cluster-id*：集群ID。IPv4地址形式。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
同一集群内所有的路由反射器配置相同的集群ID，以便标识这个集群，避免路由环路。

配置举例
+++++++++++++++
# 设置集群ID为1.1.1.1::

 ConnetOS# set protocols bgp route-reflector cluster-id 1.1.1.1

set protocols bgp peer as
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp peer** **as** 命令用来配置指定BGP对等体的AS编号。

**delete protocols bgp peer as** 命令用来删除配置的BGP对等体的AS编号。

缺省情况下，没有配置BGP对等体的AS编号。

命令格式
+++++++++++++++
**set protocols bgp peer** *peer-id* **as** *as-id*

**delete protocols bgp peer** *peer-id* **as**

参数说明
+++++++++++++++
*peer-id*：BGP对等体的IP地址。点分十进制形式。

*as-id*：AS编号。整数形式，取值范围是1～4294967295。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
配置BGP对等体时，如果指定对等体所属的AS编号与本地AS编号相同，表示配置IBGP对等体。如果指定对等体所属的AS编号与本地AS编号不同，表示配置EBGP对等体。

配置举例
+++++++++++++++
# 设置BGP对等体的AS编号为1::

 ConnetOS# set protocols bgp peer 1.1.1.1 as 1

set protocols bgp peer client enable
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp peer client enable** 命令用来配置是否将BGP对等体设置为路由反射器的客户。

**delete protocols bgp peer client enable** 命令用来取消配置的路由反射器客户。

缺省情况下，BGP对等体并不是路由反射器的客户。

命令格式
+++++++++++++++
**set protocols bgp peer** *peer-id* **client enable** { **false** | **true** }

**delete protocols bgp peer** *peer-id* **client enable**

参数说明
+++++++++++++++
*peer-id*：BGP对等体的IP地址。点分十进制形式。

**false**：不使能BGP对等体是路由反射器的客户。

**true**：使能BGP对等体是路由反射器的客户。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
在一个AS内，其中一台交换机作为路由反射器RR（Route Reflector），其它交换机做为客户机（Client）。客户机与路由反射器之间建立IBGP连接。

RR的优点在于配置方便，因为只需要在反射器上配置，客户机不需要知道自己是客户机。

配置举例
+++++++++++++++
# 将BGP对等体1.1.1.1 设置为路由反射器的客户::

 ConnetOS# set protocols bgp peer 1.1.1.1 client enable true


set protocols bgp peer confederation-member enable
-------------------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp peer confederation-member enable** 命令用来配置是否将BGP对等体加入BGP联盟，即成为BGP联盟成员。

**delete protocols bgp peer confederation-member enable** 命令用来删除配置的加入BGP联盟。

缺省情况下，BGP对等体没有加入BGP联盟。

命令格式
+++++++++++++++
**set protocols bgp peer** *peer-id* confederation-member enable** { **false** | **true** }

**delete protocols bgp peer** *peer-id* confederation-member enable** 

参数说明
+++++++++++++++
*peer-id*：BGP对等体的IP地址。点分十进制形式。

**false**：不使能BGP对等体加入BGP联盟。

**true**：使能BGP对等体加入BGP联盟。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 将IP地址为1.1.1.1的BGP对等体加入BGP联盟::

 ConnetOS# set protocols bgp peer 1.1.1.1 confederation-member enable true


set protocols bgp peer delay-open-time
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp peer delay-open-time** 命令用来配置建立BGP对等体连接的延迟时间。

**delete protocols bgp peer delay-open-time** 命令用来删除配置的建立BGP对等体连接的延迟时间，恢复为缺省值。

缺省情况下，延迟时间是0秒，即马上建立BGP对等体连接。

命令格式
+++++++++++++++
**set protocols bgp peer** *peer-id* **delay-open-time** *delay-open-time*

**delete protocols bgp peer** *peer-id* **delay-open-time**

参数说明
+++++++++++++++
*peer-id*：BGP对等体的IP地址。点分十进制形式。

*delay-open-time*：建立BGP对等体连接的延迟时间。整数形式，取值范围是0～4294967295，单位是秒。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置建立BGP对等体连接的延迟时间为120秒::

 ConnetOS# set protocols bgp peer 1.1.1.1 delay-open-time 120


set protocols bgp peer enable
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp peer enable** 命令用来配置是否将指定的交换机使能为BGP对等体。

**delete protocols bgp peer enable** 命令用来删除使能的BGP对等体。

缺省情况下，交换机已经使能为BGP对等体。

命令格式
+++++++++++++++
**set protocols bgp peer** *peer-id* **enable** { **false** | **true** }

**delete protocols bgp peer** *peer-id* **enable**

参数说明
+++++++++++++++
*peer-id*：BGP对等体的IP地址。点分十进制形式。

**false**：不使能BGP对等体。

**true**：使能BGP对等体。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 使能BGP对等体::

 ConnetOS# set protocols bgp peer 1.1.1.1 enable true

set protocols bgp peer holdtime
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp peer holdtime** 命令用来配置建立BGP对等体时的空闲时间。

**delete protocols bgp peer holdtime** 命令用来删除配置的空闲时间，恢复为缺省值。

缺省情况下，建立BGP对等体时的空闲时间是90秒。

命令格式
+++++++++++++++
**set protocols bgp peer** *peer-id* **holdtime** *holdtime*

**delete protocols bgp peer** *peer-id* **holdtime** 

参数说明
+++++++++++++++
*peer-id*：BGP对等体的IP地址。点分十进制形式。

*holdtime*：建立BGP对等体时的空闲时间。整数形式，取值范围是：0，3～65535。0表示不再等待。单位是秒。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
Idle状态是BGP初始状态。在Idle状态下，BGP拒绝邻居发送的连接请求。只有在收到本设备的Start事件后，BGP才开始尝试和其它BGP对等体进行TCP连接，并转至Connect状态。

配置举例
+++++++++++++++
# 设置建立BGP对等体时的空闲时间::

 ConnetOS# set protocols bgp peer 1.1.1.1 holdtime 60


set protocols bgp peer ipv4-multicast enable
-----------------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp peer ipv4-multicast enable** 命令用来配置BGP对等体是否使能IPv4组播功能。

**delete protocols bgp peer ipv4-multicast enable** 命令用来删除配置的IPv4组播功能，恢复为缺省值。

缺省情况下，BGP对等体没有使能IPv4组播功能。

命令格式
+++++++++++++++
**set protocols bgp peer** *peer-id* **ipv4-multicast enable** { **false** | **true** }

**delete protocols bgp peer** *peer-id* **ipv4-multicast enable**

参数说明
+++++++++++++++
*peer-id*：BGP对等体的IP地址。点分十进制形式。

**false**：BGP对等体不使能IPv4组播功能。

**true**：BGP对等体使能IPv4组播功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# BGP对等体使能IPv4组播功能::

 ConnetOS# set protocols bgp peer 1.1.1.1 ipv4-multicast enable true

set protocols bgp peer ipv4-unicast enable
-----------------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp peer ipv4-unicast enable** 命令用来配置BGP对等体是否使能IPv4单播功能。

**delete protocols bgp peer ipv4-unicast enable** 命令用来删除配置的IPv4单播功能，恢复为缺省值。

缺省情况下，BGP对等体的IPv4单播功能是使能的。

命令格式
+++++++++++++++
**set protocols bgp peer** *peer-id* **ipv4-unicast enable** { **false** | **true** }

**delete protocols bgp peer** *peer-id* **ipv4-unicast enable**

参数说明
+++++++++++++++
*peer-id*：BGP对等体的IP地址。点分十进制形式。

**false**：BGP对等体不使能IPv4单播功能。

**true**：BGP对等体使能IPv4单播功能。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# BGP对等体使能IPv4单播功能::

 ConnetOS# set protocols bgp peer 1.1.1.1 ipv4-unicast enable true

set protocols bgp peer local-ip
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp peer local-ip** 命令用来配置BGP对等体在建立对等体连接时使用的IP地址。

**delete protocols bgp peer local-ip** 命令用来删除配置的BGP对等体IP地址。

缺省情况下，没有配置BGP对等体的IP地址。

命令格式
+++++++++++++++
**set protocols bgp peer** *peer-id* **local-ip** *ip-address*

**delete protocols bgp peer** *peer-id* **local-ip**

参数说明
+++++++++++++++
*peer-id*：BGP对等体的IP地址。点分十进制形式。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置BGP对等体的IP地址::

 ConnetOS# set protocols bgp peer 1.1.1.1 local-ip 2.2.2.2


set protocols bgp peer local-port
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp peer local-port** 命令用来配置本地BGP对等体进行TCP认证时端口号。

**delete protocols bgp peer local-port** 命令用来删除配置的本地TCP认证端口号。

缺省情况下，本地BGP对等体进行TCP认证时端口号是179。

命令格式
+++++++++++++++
**set protocols bgp peer** *peer-id* **local-port** *local-port*

**delete protocols bgp peer** *peer-id* **local-port**

参数说明
+++++++++++++++
*peer-id*：BGP对等体的IP地址。点分十进制形式。

*local-port*：本地BGP对等体进行TCP认证时端口号。整数形式，取值范围是1～4294967295。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置本地BGP对等体进行TCP认证时端口号::

 ConnetOS# set protocols bgp peer 1.1.1.1 local-port 1010

set protocols bgp peer md5-password
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp peer md5-password** 命令用来配置BGP对等体在建立TCP连接时对BGP消息进行MD5认证。

**delete protocols bgp peer md5-password** 命令用来删除配置的MD5认证，恢复为缺省值。

缺省情况下，对BGP消息不进行MD5认证。

命令格式
+++++++++++++++
**set protocols bgp peer** *peer-id* **md5-password** *md5-password*

**delete protocols bgp peer** *peer-id* **md5-password**

参数说明
+++++++++++++++
*peer-id*：BGP对等体的IP地址。点分十进制形式。

*md5-password*：进行MD5认证的密码。字符串形式。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
BGP使用TCP作为传输层协议，为提高BGP的安全性，可以在建立TCP连接时进行MD5认证。BGP的MD5认证只是为TCP连接设置MD5认证密码，由TCP完成认证。

如果MD5认证失败，则不建立TCP连接。

配置举例
+++++++++++++++
# 配置BGP对等体在建立TCP连接时采用MD5认证::

 ConnetOS# set protocols bgp peer 1.1.1.1 md5-password test

set protocols bgp peer next-hop
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp peer next-hop** 命令配置指定BGP对等体的下一跳IP地址。

**delete protocols bgp peer next-hop** 命令用来删除配置的下一跳IP地址。

缺省情况下，BGP对等体没有配置下一跳IP地址。

命令格式
+++++++++++++++
**set protocols bgp peer** *peer-id* **next-hop** *next-hop-address*

**delete protocols bgp peer** *peer-id* **next-hop**

参数说明
+++++++++++++++
*peer-id*：BGP对等体的IP地址。点分十进制形式。

*next-hop-address*：下一跳IP地址。点分十进制形式。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 设置对等体的下一跳地址为1.1.1.2::

 ConnetOS# set protocols bgp peer 1.1.1.1 next-hop 1.1.1.2

set protocols bgp peer peer-port
-------------------------------------------

命令功能
+++++++++++++++
**set protocols bgp peer peer-port** 命令用来配置远端设备进行TCP认证时端口号。

**delete protocols bgp peer peer-port** 命令用来删除配置的TCP认证端口号。

缺省情况下，进行TCP认证时端口号端口号是179。

命令格式
+++++++++++++++
**set protocols bgp peer** *peer-id* **peer-port** *peer-port-number*

**delete protocols bgp peer** *peer-id* **peer-port**

参数说明
+++++++++++++++
*peer-id*：BGP对等体的IP地址。点分十进制形式。

*peer-port-number*：端口号。整数形式，取值范围是1～4294967295。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 配置TCP认证端口号::

 ConnetOS# set protocols bgp peer 1.1.1.1 peer-port 1010
