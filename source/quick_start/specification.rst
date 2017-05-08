业务特性
=======================================
ConnetOS支持的功能特性如下表所示。

===========     ===========================================================
分类             特性
===========     ===========================================================
自动部署        Auto provision：ATP
                
                Zero Touching Provision：ZTP

管理            Telnet、SSH、TFTP
                
                聚合网段管理
                
                带内管理（loopback、vlan-interface）
                
                带外管理
                
                SNMP、DHCP、DHCP relay
                
                基于TACACS+的认证、授权、计费
                
                基于事务机制的命令行
                
                多达49级的配置回滚

交换与路由      VLAN、LAG、LLDP、LACP
                
                静态路由、OSPF、BGP、ECMP
                
                LAG、ECMP
                
                哈希：一致性哈希、对称哈希、二次哈希
                
                路由策略

虚拟化           VXLAN bridging

QoS             基于优先级的映射：DSCP、IEEE 802.1p、Trust-port
                
                队列调度模式：SP、WDRR、SP+WDRR

策略            访问控制列表：L2、L3、L4 fields

                转发策略：分类、镜像、策略、交换、路由

可靠性           高智能堆叠系统：ISS

流式遥测        sFlow：监控接口转发数据包级别
                
                sDrop：分析丢弃的数据包
                
                sMetric：监控管理面和控制面状态、配置和事件

分析和诊断      Tcpdump：Linux系统直接抓包

                Mirror：业务端口数据包镜像

                Navmesh：网络转发路径计算

DEVOPS          Remote CLI Call（RCC）
                
                Python SDK
                
                RESTful API
                
                agt-get/dpkg软件包：Puppet、Ansible、Zabbix
===========     ===========================================================