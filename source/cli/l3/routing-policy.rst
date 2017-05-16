路由策略命令
=======================================

set policy policy-statement term from
---------------------------------------

命令功能
+++++++++++++++
**set policy policy-statement term from** 命令用来定义应用于源地址路由的路由策略。

**delete policy policy-statement term from** 命令用来删除配置的定义应用于源地址路由的路由策略。

命令格式
+++++++++++++++
**set policy policy-statement** *policy-name* **term** *term-name* **from** { **as-path** *as-path-name* | **as-path-list** *as-path-list-name* | **community** *community-name* | **community-list** *community-list-name* | **external-type** *type-number* | **localpref** *preference-number* | **med** *med* | **metric** *metric* | **neighbor** *neighbor-router* | **network4** *network4-address* | **network4-list** *network4-list-name* | **nexthop4** *nexthop4-address* | **origin** *origin-attribute* | **prefix-length4** *prefix-length4* | **protocol** { **connected** | **ospf4** | **static** } | **tag** *tag-value* }   

**delete policy policy-statement** *policy-name* **term** *term-name* **from** { **as-path** | **as-path-list**  *type-number* | **localpref** *preference-number* | **med** | **metric** | **neighbor** | **network4** | **network4-list**  | **nexthop4** | **origin** | **prefix-length4** | **protocol** | **tag** }    

参数说明
+++++++++++++++
*as-path-name*：BGP路由所经过的所有AS名称。

*as-path-list-name*：BGP路由所经过的所有AS列表名称。

*community-name*：BGP团体属性名称。

*community-list-name*：BGP团体属性列表名称。

*type-number*：引入OSPF外部路由的类型。取值为1、2。

*preference-number*：本地路由的优先级，整数形式，取值范围是0～4294967295。

*med*：BGP MED属性值，整数形式，取值范围是0～4294967295。

*metric*：路由信息开销，整数形式，取值范围是0～4294967295。

*neighbor-router*：邻居路由的IP地址，取值为点分十进制。

*network4-address*：区域所包含的网段。取值形式是网段地址／掩码。

*network4-list-name*：网段列表的名称。

*nexthop4-address*：下一跳的IP地址，取值为点分十进制。

*origin-attribute*：路由的原始属性。整数形式，取值范围是0～2。
 
 * 0：IGP
 * 1：EGP
 * 2：不完全路由

*prefix-length4*：地址前缀列表长度，整数形式，取值范围是0～4294967295。

**connected**：子网的直连路由。

**ospf4**：OSPFv4路由。

**static**：静态路由。

*tag-value*：OSPF路由信息的标记值。整数形式，取值范围是0～4294967295。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 定义应用于源地址路由的路由策略policy1::

 ConnetOS# set policy policy-statement policy1 term t1 from protocol ospf4

set policy policy-statement term then
---------------------------------------

命令功能
+++++++++++++++
**set policy policy-statement term then** 用来设置对符合路由策略中策略内容定义的路由的处理方式。

**delete policy policy-statement term then** 命令用来删除定义的路由的处理方式。

命令格式
+++++++++++++++
**set policy policy-statement** *policy-name* **term** *term-name* **then** { **accept** | **aggregate-brief-mode** { **false** | **true** } | **aggregate-prefix-len**  *aggregate-prefix-len* | **as-path-expand** *as-path-expand* | **as-path-prepend** *as-path-prepend* | **community** *community-name* | **community-add** *community-add-name* | **community-del** *community-del* | **external-type** *external-type-number* | **localpref** *localpref* | **med** *med* | **med-remove** { **false** | **true** } | **metric** *metric* | **nexthop4** *nexthop4-address* | **nexthop4-var** { **peer-address** | **self**} | **origin** *origin-attribute* | **reject** | **tag** *tag-value* }

**delete policy policy-statement** *policy-name* **term** *term-name* **then** { **accept** | **aggregate-brief-mode** | **aggregate-prefix-len** | **as-path-expand** | **as-path-prepend** | **community** | **community-add** | **community-del** | **external-type** | **localpref** | **med** | **med-remove** | **metric** | **nexthop4** | **nexthop4-var**  | **origin** | **reject** | **tag** }

参数说明
+++++++++++++++
**accept**：接受符合路由策略及过滤条件的路由。

**aggregate-brief-mode**：不生成聚合路由。

**aggregate-prefix-len** *aggregate-prefix-len*：生成指定前缀长度的聚合路由。*aggregate-prefix-len* 为前缀长度，整数形式，取值范围是0～4294967295。

**as-path-expand** *as-path-expand*：在增加本地AS域时的预留AS编号优先级。整数形式，取值范围是0～4294967295。

**as-path-prepend** *as-path-prepend*：AS路径的预留AS编号优先级。整数形式，取值范围是0～4294967295。

*community-name*：BGP团体的名称。

*community-add-name*：在路由中引入的BGP团体的名称。

*community-del*：在路由中删除的BGP团体的名称。

*external-type-number*：OSPF的外部路由类型。取值为1、2，分别代表type1和type2类型的外部OSPF路由。

*localpref*：本地优先级。整数形式，取值范围是0～4294967295。

*med*：BGP MED属性值，整数形式，取值范围是0～4294967295。

**med-remove**：是否移除MED属性。

*metric*：路由信息开销。整数形式，取值范围是0～4294967295。

*nexthop4-address*：下一跳的IP地址，取值为点分十进制。

**peer-address**：对端IP地址。

**self**：

*origin-attribute*：路由的原始属性。整数形式，取值范围是0～2。
 
 * 0：IGP
 * 1：EGP
 * 2：不完全路由

**reject**：拒绝接受符合路由策略及过滤条件的路由。

*tag-value*：OSPF路由信息的标记值。整数形式，取值范围是0～4294967295。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 接受符合policy1中term1定义的源路由::

 ConnetOS# set policy policy-statement policy1 term term1 then accept

set policy policy-statement term to
---------------------------------------

命令功能
+++++++++++++++
**set policy policy-statement term to** 命令用来定义应用于目的地址路由的路由策略。

**set policy policy-statement term to** 命令用来删除定义的应用于目的地址路由的路由策略。

命令格式
+++++++++++++++
**set policy policy-statement** *policy-name* **term** *term-name* **to** { **as-path** *as-path-name* | **as-path-list** *as-path-list-name* | **community** *community-name* | **community-list** *community-list-name* | **external-type** *type-number* | **localpref** *preference-number* | **med** *med* | **metric** *metric* | **neighbor** *neighbor-router* | **network4** *network4-address* | **network4-list** *network4-list-name* | **nexthop4** *nexthop4-address* | **origin** *origin-attribute* | **prefix-length4** *prefix-length4* | **protocol** { **connected** | **ospf4** | **static** } | **tag** *tag-value* | **was-aggregated** { **false** | **was-aggregated** } }  

**delete policy policy-statement** *policy-name* **term** *term-name* **to** { **as-path** | **as-path-list**  *type-number* | **localpref** *preference-number* | **med** | **metric** | **neighbor** | **network4** | **network4-list**  | **nexthop4** | **origin** | **prefix-length4** | **protocol** | **tag** | **was-aggregated** }    

参数说明
+++++++++++++++
*as-path-name*：BGP路由所经过的所有AS名称。

*as-path-list-name*：BGP路由所经过的所有AS列表名称。

*community-name*：BGP团体属性名称。

*community-list-name*：BGP团体属性列表名称。

*type-number*：引入OSPF外部路由的类型。取值为1、2。

*preference-number*：路由协议的优先级，整数形式，取值范围是0～4294967295。

*med*：BGP MED属性值，整数形式，取值范围是0～4294967295。

*metric*：路由信息的路由开销。整数形式，取值范围是0～4294967295。

*neighbor-router*：邻居路由的IP地址，取值为点分十进制。

*network4-address*：区域所包含的网段。取值形式是网段地址／掩码。

*network4-list-name*：网段列表的名称。

*nexthop4-address*：下一跳的IP地址，取值为点分十进制。

*origin-attribute*：路由的原始属性。整数形式，取值范围是0～2。
 
 * 0：IGP
 * 1：EGP
 * 2：不完全路由

*prefix-length4*：地址前缀列表长度，整数形式，取值范围是0～4294967295。

**connected**：子网的直连路由。

**ospf4**：OSPFv4路由。

**static**：静态路由。

*tag-value*：OSPF路由信息的标记值。整数形式，取值范围是0～4294967295。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 定义应用于目的地址路由的路由策略policy1::

 ConnetOS# set policy policy-statement policy1 term term2 to nexthop4 1.1.1.1
 

set policy policy-statement then
---------------------------------------

命令功能
+++++++++++++++
**set policy policy-statement then** 命令用来设置匹配路由策略后的执行动作。

**delete policy policy-statement then** 命令用来删除配置的执行动作。

命令格式
+++++++++++++++
**set policy policy-statement** *policy-name* **then** { **accept** | **reject**}

**delete policy policy-statement** *policy-name* **then** [ **accept** | **reject** ]

参数说明
+++++++++++++++
**accept**：接受符合 *policy-name* 定义的路由策略的路由。

**reject**：拒绝符合 *policy-name* 定义的路由策略的路由。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 接受policy1定义的路由::

 ConnetOS# set policy policy-statement policy1 then accept