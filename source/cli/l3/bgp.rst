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
# 设置联盟ID为9::

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
**set protocols bgp peer** ** **as**


命令格式
+++++++++++++++


参数说明
+++++++++++++++


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++


配置举例
+++++++++++++++
# ::

 ConnetOS# 


-------------------------------------------

命令功能
+++++++++++++++



命令格式
+++++++++++++++


参数说明
+++++++++++++++


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++


配置举例
+++++++++++++++
# ::

 ConnetOS# 



-------------------------------------------

命令功能
+++++++++++++++



命令格式
+++++++++++++++


参数说明
+++++++++++++++


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++


配置举例
+++++++++++++++
# ::

 ConnetOS# 



-------------------------------------------

命令功能
+++++++++++++++



命令格式
+++++++++++++++


参数说明
+++++++++++++++


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++


配置举例
+++++++++++++++
# ::

 ConnetOS# 



-------------------------------------------

命令功能
+++++++++++++++



命令格式
+++++++++++++++


参数说明
+++++++++++++++


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++


配置举例
+++++++++++++++
# ::

 ConnetOS# 



-------------------------------------------

命令功能
+++++++++++++++



命令格式
+++++++++++++++


参数说明
+++++++++++++++


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++


配置举例
+++++++++++++++
# ::

 ConnetOS# 




-------------------------------------------

命令功能
+++++++++++++++



命令格式
+++++++++++++++


参数说明
+++++++++++++++


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++


配置举例
+++++++++++++++
# ::

 ConnetOS# 



-------------------------------------------

命令功能
+++++++++++++++



命令格式
+++++++++++++++


参数说明
+++++++++++++++


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++


配置举例
+++++++++++++++
# ::

 ConnetOS# 




-------------------------------------------

命令功能
+++++++++++++++



命令格式
+++++++++++++++


参数说明
+++++++++++++++


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++


配置举例
+++++++++++++++
# ::

 ConnetOS# 



-------------------------------------------

命令功能
+++++++++++++++



命令格式
+++++++++++++++


参数说明
+++++++++++++++


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++


配置举例
+++++++++++++++
# ::

 ConnetOS# 



-------------------------------------------

命令功能
+++++++++++++++



命令格式
+++++++++++++++


参数说明
+++++++++++++++


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++


配置举例
+++++++++++++++
# ::

 ConnetOS# 



-------------------------------------------

命令功能
+++++++++++++++



命令格式
+++++++++++++++


参数说明
+++++++++++++++


命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++


配置举例
+++++++++++++++
# ::

 ConnetOS# 


