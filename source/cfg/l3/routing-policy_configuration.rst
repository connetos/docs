路由策略配置
=======================================

简介
---------------------------------------

概述
+++++++++++++++++++++++++++++++++++++++
路由策略主要实现了路由过滤和路由属性设置等功能，它通过改变路由属性（包括可达性）来改变网络流量所经过的路径。

路由协议在发布、接收和引入路由信息时，如果根据实际组网需求实施一些策略，那么就可以对路由信息进行过滤和改变路由信息的属性，如：

 * 控制路由的接收和发布

   只发布和接收必要、合法的路由信息，以控制路由表的容量，提高网络的安全性。

 * 控制路由的引入

   在一种路由协议在引入其它路由协议发现的路由信息丰富自己的路由信息时，只引入一部分满足条件的路由信息。
 
 * 设置特定路由的属性

   修改通过路由策略过滤的路由的属性，满足自身需要。

路由策略具有以下：
 
 * 通过控制路由器的路由表规模，节约系统资源。
 * 通过控制路由的接收、发布和引入，提高网络安全性。
 * 通过修改路由属性，对网络数据流量进行合理规划，提高网络性能。

路由策略和策略路由
+++++++++++++++++++++++++++++++++++++++
策略路由（Policy-based Routing），本质上是路由。是一种根据用户指定的策略进行路由选择的机制，比基于目标网络进行路由更加灵活。

路由策略（Routing Policy），本质上是一种策略。是为了改变网络流量所经过的途径而修改路由信息的技术，主要通过改变路由属性（包括可达性）来实现。

=================  =================================   ===============================
差异                策略路由                             路由策略
=================  =================================   ===============================
作用对象            数据包                               路由信息
是否改变转发流程     改变                                 不改变
实现主体            转发平面，保证数据包按照策略转发         控制平面，实现路由过滤和属性修改     
过滤机制            匹配五元组：                          匹配路由：

                    * 源IP地址                           * 目标网段
                    * 目的IP地址                         * 下一跳
                    * 协议                               * 度量值
                    * 源端口                             * Tag
                    * 目的端口                           * Community
应用主体           * 本地数据包                        * 直连路由
                   * 转发数据包                        * 静态路由
                                                       * OSPF
                                                       * BGP
=================  =================================   ===============================

路由策略的配置逻辑
+++++++++++++++++++++++++++++++++++++++
配置路由策略，分为两步：

#. 定义路由策略。
    
   ConnetOS采用策略名＋策略内容名＋动作＋策略规则的方式，来实现路由策略：

   **set policy policy-statement** *policy-name* **term** *term-name* ｛ **from** ｜ **to** ｜ **then** ｝ ＋ 策略规则

   **set policy policy-statement** *policy-name* **term** *term-name* **then** ＋ 策略动作

   **set policy policy-statement** **then** ＋ 策略动作

   其中：

    * *policy-name*：代表策略名字。
    * *term-name*：代表策略内容。一个策略策略下可以配置多个 *term-name*。
    * **from**：应用于源地址路由
    * **to**：应用于目的地址路由。
    * **then**：匹配策略后的后的动作。

#. 应用路由策略。

  路由策略设置好后，直接在路由协议中应用即可生效。


配置路由策略
---------------------------------------
#. 进入配置模式。

   ConnetOS> **configure**

#. 定义路由策略的应用对象。
   
   * 定义应用于源地址路由的路由策略。
   
     ConnetOS# **set policy policy-statement** *policy-name* **term** *term-name* **from** { **as-path** *as-path-name* | **as-path-list** *as-path-list-name* | **community** *community-name* | **community-list** *community-list-name* | **external-type** *type-number* | **localpref** *preference-number* | **med** *med* | **metric** *metric* | **neighbor** *neighbor-router* | **network4** *network4-address* | **network4-list** *network4-list-name* | **nexthop4** *nexthop4-address* | **origin** *origin-attribute* | **prefix-length4** *prefix-length4* | **protocol** { **connected** | **ospf4** | **static** } | **tag** *tag-value* } 
   
   * 定义应用于目的地址路由的路由策略。
 
     ConnetOS# **set policy policy-statement** *policy-name* **term** *term-name* **to** { **as-path** *as-path-name* | **as-path-list** *as-path-list-name* | **community** *community-name* | **community-list** *community-list-name* | **external-type** *type-number* | **localpref** *preference-number* | **med** *med* | **metric** *metric* | **neighbor** *neighbor-router* | **network4** *network4-address* | **network4-list** *network4-list-name* | **nexthop4** *nexthop4-address* | **origin** *origin-attribute* | **prefix-length4** *prefix-length4* | **protocol** { **connected** | **ospf4** | **static** } | **tag** *tag-value* | **was-aggregated** { **false** | **was-aggregated** } } 

#. 设置路由策略的动作。
   
   * 设置路由策略的整体动作。

     **set policy policy-statement** *policy-name* **then** { **accept** | **reject** }

   * 设置指定策略内容的动作。

     ConnetOS# **set policy policy-statement** *policy-name* **term** *term-name* **then** { **accept** | **aggregate-brief-mode** { **false** | **true** } | **aggregate-prefix-len**  *aggregate-prefix-len* | **as-path-expand** *as-path-expand* | **as-path-prepend** *as-path-prepend* | **community** *community-name* | **community-add** *community-add-name* | **community-del** *community-del* | **external-type** *external-type-number* | **localpref** *localpref* | **med** *med* | **med-remove** { **false** | **true** } | **metric** *metric* | **nexthop4** *nexthop4-address* | **nexthop4-var** { **peer-address** | **self**} | **origin** *origin-attribute* | **reject** | **tag** *tag-value* }

#. 应用路由策略。
   
   ConnetOS# **set protocols** { **bgp** | **ospf4** } { **export** | **import** } *policy-name*

#. 提交配置。

   ConnetOS# **commit**