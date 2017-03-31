QoS命令
====================================

set class-of-service
------------------------
命令功能
+++++++++++++++
**set class-of-service** 命令用来QoS服务等级节点。

缺省情况下，没有设置QoS服务等级节点。

命令格式
+++++++++++++++
**set class-of-service**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 设置QoS服务等级节点::

ConnetOS# set class-of-service

set class-of-service classifier
-------------------------------------------

命令功能
+++++++++++++++
**set class-of-service classifier** 命令用来定义流分类。

**delete class-of-service classifier** 命令用来删除指定的流分类及流分类的相关配置。
缺省情况下，ConnetOS上没有定义流分类。

命令格式
+++++++++++++++
**set class-of-service classifier** *classifier-name*

**delete class-of-service classifier** *classifier-name*

参数说明
+++++++++++++++
*classifier-name*：流分类的名字。字符串形式，支持区分大小写及特殊字符，如果首字母是空格，能配置但是空格在名称中不体现。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
ConnetOS上可以定义任意个数的流分类，但是不提交流分类就不生效，并不消耗多少系统资源。

.. note:: 
   * 流分类必须配置优先级信任模式（trust-mode）后才能提交。
   * 如果流分类已经被绑定，必须先去除绑定后才能删除。

配置举例
+++++++++++++++
# 创建一个名字为c1的类::

 ConnetOS# set class-of-service classifier c1

set class-of-service classifier forwarding-class
------------------------------------------------------

命令功能
+++++++++++++++
**set class-of-service classifier forwarding-class** 命令用来设置指定流分类在出端口进行报文转发时的转发队列。

**delete class-of-service classifier forwarding-class** 命令用来删除流分类和转发队列的绑定。

缺省情况下，如果不指定转发队列，那报文进0队列进行转发。

命令格式
+++++++++++++++
**set class-of-service classifier** *classifier-name* **forwarding-class** *forwarding-class* [ **code-point** *code-poin* ]

**delete class-of-service classifier** *classifier-name* **forwarding-class** *forwarding-class* [ **code-point** *code-point* ]

参数说明
+++++++++++++++
*classifier-name*：流分类的名字。字符串形式，支持区分大小写及特殊字符，如果首字母是空格，能配置但是空格在名字中不体现。

*forwarding-class*：转发队列的名称。字符串形式，支持区分大小写及特殊字符，如果首字母是空格，能配置但是空格在名字中不体现。

*code-point*：ieee-802.1和inet-precedence的取值范围是0～7，dscp的取值范围是0～63。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
在入端口上为流分类绑定转发队列时，决定了报文发送时走哪个队列。
配置此命令后，流分类将进入不同的转发队列。

配置举例
+++++++++++++++
# 设置流分类c1中的DSCP流量，在转发时按照转发队列fd1的队列编号进行转发::

 ConnetOS# set class-of-service classifier c1 forwarding-class fd1 code-point 14

set class-of-service classifier trust-mode
-------------------------------------------------

命令功能
+++++++++++++++
**set class-of-service classifier trust-mode** 命令用来配置优先级信任模式，即设备根据哪种优先级进行映射。

**delete class-of-service classifier trust-mode** 用来删除配置的优先级信任模式。

命令格式
+++++++++++++++
**set class-of-service classifier** *classifier-name* **trust-mode** { **dscp** | **ieee-802.1** | **trust-port** }

**delete class-of-service classifier** *classifier-name* **trust-mode** { **dscp** | **ieee-802.1** | **trust-port** }

参数说明
+++++++++++++++
**dscp**：指定对报文按照DSCP优先级进行映射。

**ieee-802.1**：指定对报文按照802.1p优先级进行映射。

**trust-port**：指定对报文按照端口信任模式进行映射。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 设置流分类c1中的IP报文按照DSCP优先级优先级进行映射::

 ConnetOS# set class-of-service classifier c1 trust-mode dscp

set class-of-service forwarding-class
-------------------------------------------

命令功能
+++++++++++++++
**set class-of-service forwarding-class** 命令用来设置出端口的转发队列。

**delete class-of-service forwarding-class** 命令用来删除创建的转发队列。

缺省情况下，ConnetOS上没有创建转发队列。

命令格式
+++++++++++++++
**set class-of-service forwarding-class** *forwarding-class* **queue-num** *queue-numer* 

**delete class-of-service** **forwarding-class** *forwarding-class* [ **queue-num** ]

参数说明
+++++++++++++++
*forwarding-class*：转发队列的名称。字符串形式，支持区分大小写及特殊字符，如果首字母是空格，能配置但是空格在名字中不体现。

*queue-numer*：队列编号。整数形式，取值范围是0～7。数字越大，优先级越高。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
ConnetOS按照配置的队列优先级在出端口对报文进行转发，不同的转发队列，将获得不同的服务等级。

配置举例
+++++++++++++++
# 设置转发队列fd1的队列编号为1::

 ConnetOS# set class-of-service forwarding-class fd1 queue-num 1

set class-of-service interface
-------------------------------------------

命令功能
+++++++++++++++
**set class-of-service interface** 命令用来设置将指定的流分类绑定到指定接口。

**delete class-of-service interface** 命令用来删除接口上绑定的流分类。

缺省情况下，接口上没有绑定任何流分类。

命令格式
+++++++++++++++
**set class-of-service interface** *interface-name* [ **classifier** *classifier-name* ]

**delete class-of-service interface** *interface-name* [ **classifier** ]

参数说明
+++++++++++++++
*interface-name*：接口名称。

*classifier-name*：流分类名称。此流分类必须是ConnetOS上已经存在的流分类。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
将流分类绑定到流量的入口后，流量在出口会按照优先级到队列映射表映射到相应的出口队列。

配置举例
+++++++++++++++
# 将流分类c1绑定到接口te－1/1/15::

 ConnetOS# set class-of-service interface te-1/1/15 classifier c1 

set interface gigabit-ethernet cos
-------------------------------------------

命令功能
+++++++++++++++

**set interface gigabit-ethernet cos** 命令用来在报文映射模式为信任端口时，配置端口优先级。

**delete interface gigabit-ethernet cos** 命令用来删除端口优先级。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-number* **cos priority** *priority-value*

**delete interface gigabit-ethernet** *interface-number* **cos priority**

参数说明
+++++++++++++++
*interface-number*：接口编号。

*priority-value*：优先级。整数形式，取值范围是0～7。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
配置端口优先级后，此端口流入的流量将以端口优先级查找优先级映射表得到出口队列。

配置举例
+++++++++++++++
# 设置接口te－1/1/15的端口优先级为3::

 ConnetOS# set class-of-service interface gigabit-ethernet te-1/1/15 cos priority 3

set interface gigabit-ethernet cos schedule mode
------------------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet cos schedule mode** 命令用来设置指定接口在拥塞管理时的调度算法。

**delete interface gigabit-ethernet cos schedule mode** 命令用来删除指定接口的拥塞管理调度算法。

缺省情况下，接口采用WDRR调度算法。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-number* **cos schedule mode** { **sp** | **sp+wdrr** | **sp+wrr** | **wdrr** | **wrr** } 

**delete interface gigabit-ethernet** *interface-number* **cos schedule mode**

参数说明
+++++++++++++++
*interface-number*：接口编号。

**sp**：严格优先级调度。

**sp+wrr**：SP和WRR结合的调度算法

**wdrr**：带赤字的加权轮询调度。

**wrr**：加权轮询调度。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
WRR和WDRR模式需要配置全部8个队列的权重。

WRR+SP和WDRR+SP模式下没有配置权重的队列按照SP调度，SP模式无需配置队列权重。

配置举例
+++++++++++++++
# 设置接口gigabit-ethernet te-1/1/16采用sp+wdrr的调度算法::

 ConnetOS# set interface gigabit-ethernet te-1/1/16 cos schedule mode sp+wdrr

set interface gigabit-ethernet cos schedule queue
-------------------------------------------------------

命令功能
+++++++++++++++
**set interface gigabit-ethernet cos schedule queue** 命令用来设置在拥塞管理时指定接口进入的调度队列编号和加权值。

**delete interface gigabit-ethernet cos schedule** 命令用来删除指定端口的队列编号和加权值。

缺省情况下，端口上不同报文入指定编号的队列。

命令格式
+++++++++++++++
**set interface gigabit-ethernet** *interface-number* **cos schedule queue** *queue-number* [ **weight** *weight-value* ]

**delete interface gigabit-ethernet** *interface-number* **cos schedule queue** *queue-number* [ **weight** ]

参数说明
+++++++++++++++
*interface-number*：接口编号。

*queue-number*：队列编号。整数形式，取值范围是0～7。 

*weight-value*：WRR和WDRR的权重值。整数形式，取值范围是0～127。0属于SP队列。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
缺省的队列映射如下：

 ====================  ======================  =================
 入口报文携带dscp        入口报文携带8021.p        出口队列
 ====================  ======================  =================
 0～7                   0                       0
 8～15                  1                       1
 16～23                 2                       2
 24～31                 3                       3
 32～39                 4                       4
 40～47                 5                       5
 48～55                 6                       6
 58～63                 7                       7
 ====================  ======================  =================

配置举例
+++++++++++++++
# 设置接口gigabit-ethernet te-1/1/16在发生拥塞时进入2号队列::

 ConnetOS# set interface gigabit-ethernet te-1/1/17 cos schedule queue 2 weight 34

show class-of-service
-------------------------------------------

命令功能
+++++++++++++++
**show class-of-service** 命令用来查看QoS的所有配置信息。

命令格式
+++++++++++++++
**show class-of-service**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
如果用户执行了 **delete class-of-servic** 命令，show的时候会看不到 **class-of-service** 关键字，必须先设置cos服务器节点才能看到相关命令。

配置举例
+++++++++++++++
# 查看设备上QoS的配置信息::

 ConnetOS# show class-of-service
 Waiting for building configuration.
    forwarding-class fd1 {
        queue-num: 1
    }
    classifier c1 {
        trust-mode: "trust-port"
        forwarding-class fd1 {
            code-point 7
        }
    }
    interface "te-1/1/13" {
        classifier: "c1"
    }

show class-of-service classifier
-------------------------------------------

命令功能
+++++++++++++++
**show class-of-service classifier** 命令用来查看指定流分类的配置信息。

命令格式
+++++++++++++++
**show class-of-service classifier** *classifier-name*\［ **forwarding-class**\  *forwarding-class* [ **code-point** *code-point* ] ］

参数说明
+++++++++++++++
*classifier-name*：流分类的名字。字符串形式，支持区分大小写及特殊字符，如果首字母是空格，能配置但是空格在名字中不体现。

*forwarding-class*：转发队列的名称。字符串形式，支持区分大小写及特殊字符，如果首字母是空格，能配置但是空格在名字中不体现。

*code-point*：ieee-802.1和inet-precedence的取值范围是0～7；dscp的取值范围是0～63。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
在入端口上为流分类绑定转发队列时，决定了报文发送时走哪个队列。

配置此命令后，流分类将进入不同的转发队列。

配置举例
+++++++++++++++
# 查看指定流分类的配置信息::

   ConnetOS 1# show class-of-service classifier c1
      trust-mode: "dscp"
      forwarding-class f1


show class-of-service forwarding-class
-------------------------------------------

命令功能
+++++++++++++++
**show class-of-service forwarding-class** 命令用来查看指定转发队列的配置信息。

命令格式
+++++++++++++++
**show class-of-service forwarding-class** *forwarding-class*

参数说明
+++++++++++++++
*forwarding-class*：已经定义的转发队列的名称。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
当ConnetOS上没有定义转发队列时，无法执行此命令。

配置举例
+++++++++++++++
# 查看转发队列fd1的配置信息::

 ConnetOS# show class-of-service forwarding-class fd1
 Waiting for building configuration.
    queue-num: 1

show class-of-service interface
-------------------------------------------

命令功能
+++++++++++++++
**show class-of-service interface** 命令用来查看指定接口的QoS配置信息。

命令格式
+++++++++++++++
**show class-of-service interface** *interface-name*

参数说明
+++++++++++++++
*interface-name*：接口名称。此接口是指已经配置了QoS功能的接口。

命令模式
+++++++++++++++
配置模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查看接口te－1/1/7的QoS配置信息::

 ConnetOS# show class-of-service interface te-1/1/7
 Waiting for building configuration.
    classifier: "c1"

