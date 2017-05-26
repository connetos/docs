系统信息查询命令参考
=======================================

show system boot-messages
-------------------------------------------

命令功能
+++++++++++++++
**show system boot-messages** 命令用来查看启动信息。

命令格式
+++++++++++++++
**show system boot-messages**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查看系统的启动信息::

 ConnetOS 1> show system boot-messages
 [    0.000000] Initializing cgroup subsys cpuset
 [    0.000000] Initializing cgroup subsys cpu
 [    0.000000] Initializing cgroup subsys cpuacct
 [    0.000000] Linux version 3.16.7-ckt25+ (root@host-b) (gcc version 4.9.2 (Debian 4.9.2-10) ) #1 SMP Thu Mar 2 10:28:57 CST 2017
 [    0.000000] Command line: BOOT_IMAGE=/boot/vmlinuz-3.16.7-ckt25+ root=LABEL=/ ro console=tty0 console=ttyS1,115200n8 quiet
 [    0.000000] e820: BIOS-provided physical RAM map:
 [    0.000000] BIOS-e820: [mem 0x0000000000000000-0x000000000009abff] usable
 [    0.000000] BIOS-e820: [mem 0x000000000009ac00-0x000000000009ffff] reserved
 [    0.000000] BIOS-e820: [mem 0x00000000000e0000-0x00000000000fffff] reserved
 [    0.000000] BIOS-e820: [mem 0x0000000000100000-0x000000007f15bfff] usable
 [    0.000000] BIOS-e820: [mem 0x000000007f15c000-0x000000007f18bfff] reserved
 [    0.000000] BIOS-e820: [mem 0x000000007f18c000-0x000000007f234fff] usable
 [    0.000000] BIOS-e820: [mem 0x000000007f235000-0x000000007f4a2fff] ACPI NVS
 [    0.000000] BIOS-e820: [mem 0x000000007f4a3000-0x000000007f639fff] reserved
 [    0.000000] BIOS-e820: [mem 0x000000007f63a000-0x000000007f7fffff] usable
 [    0.000000] BIOS-e820: [mem 0x00000000e0000000-0x00000000e3ffffff] reserved
 [    0.000000] BIOS-e820: [mem 0x00000000fed01000-0x00000000fed03fff] reserved
 [    0.000000] BIOS-e820: [mem 0x00000000fed08000-0x00000000fed08fff] reserved
 [    0.000000] BIOS-e820: [mem 0x00000000fed0c000-0x00000000fed0ffff] reserved
 [    0.000000] BIOS-e820: [mem 0x00000000fed1c000-0x00000000fed1cfff] reserved
 [    0.000000] BIOS-e820: [mem 0x00000000fef00000-0x00000000feffffff] reserved
 [    0.000000] BIOS-e820: [mem 0x00000000ff800000-0x00000000ffffffff] reserved
 [    0.000000] NX (Execute Disable) protection: active
 [    0.000000] SMBIOS 0.8 present.
 [    0.000000] DMI: Accton AS5512-54X/AS5512-54X, BIOS 5.6.5 08/20/2015
 [    0.000000] e820: update [mem 0x00000000-0x00000fff] usable ==> reserved
 [    0.000000] e820: remove [mem 0x000a0000-0x000fffff] usable
 [    0.000000] AGP: No AGP bridge found
 [    0.000000] e820: last_pfn = 0x7f800 max_arch_pfn = 0x400000000
 [    0.000000] MTRR default type: write-back
 [    0.000000] MTRR fixed ranges enabled:
 [    0.000000]   00000-9FFFF write-back
 [    0.000000]   A0000-BFFFF uncachable
 [    0.000000]   C0000-E7FFF write-through
 [    0.000000]   E8000-FFFFF write-protect
 [    0.000000] MTRR variable ranges enabled:
 [    0.000000]   0 base 080000000 mask F80000000 uncachable
 [    0.000000]   1 base 100000000 mask F00000000 uncachable
 [    0.000000]   2 base 200000000 mask E00000000 uncachable
 [    0.000000]   3 base 400000000 mask C00000000 uncachable
 [    0.000000]   4 base 800000000 mask 800000000 uncachable
 [    0.000000]   5 base 07F800000 mask FFF800000 uncachable
 [    0.000000]   6 disabled
 [    0.000000]   7 disabled
 [    0.000000] x86 PAT enabled: cpu 0, old 0x7040600070406, new 0x7010600070106
 [    0.000000] found SMP MP-table at [mem 0x000fd6b0-0x000fd6bf] mapped at [ffff8800000fd6b0]
 [    0.000000] Base memory trampoline at [ffff880000094000] 94000 size 24576
 [    0.000000] init_memory_mapping: [mem 0x00000000-0x000fffff]
 [    0.000000]  [mem 0x00000000-0x000fffff] page 4k
 [    0.000000] BRK [0x01b09000, 0x01b09fff] PGTABLE
 [    0.000000] BRK [0x01b0a000, 0x01b0afff] PGTABLE
 [    0.000000] BRK [0x01b0b000, 0x01b0bfff] PGTABLE
 [    0.000000] init_memory_mapping: [mem 0x7ee00000-0x7effffff]
 [    0.000000]  [mem 0x7ee00000-0x7effffff] page 2M
 [    0.000000] BRK [0x01b0c000, 0x01b0cfff] PGTABLE
 [    0.000000] init_memory_mapping: [mem 0x7c000000-0x7edfffff]
 [    0.000000]  [mem 0x7c000000-0x7edfffff] page 2M
 [    0.000000] init_memory_mapping: [mem 0x00100000-0x7bffffff]
 [    0.000000]  [mem 0x00100000-0x001fffff] page 4k
 --More--

show system core-dumps
-------------------------------------------

命令功能
+++++++++++++++
**sshow system core-dumps** 命令用来查看CPU的利用率。

命令格式
+++++++++++++++
**show system core-dumps** 

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查看本设备的CPU的利用率::

 ConnetOS> show system cpu-usage
 Cpu usage: 2%


show system cpu-usage
-------------------------------------------

命令功能
+++++++++++++++
**show system cpu-usage** 命令用来查看CPU的利用率。

命令格式
+++++++++++++++
单机模式：**show system cpu-usage** 

堆叠模式：**show system cpu-usage** [ **all** | **member** *member-id* ]

参数说明
+++++++++++++++
**all**：查看堆叠系统内所有设备的CPU的利用率。

*member-id*：查看指定 *member-id* 设备的CPU的利用率。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查看本设备的CPU的利用率::

 ConnetOS> show system cpu-usage
 Cpu usage: 2%

show system ddm 
---------------------------------------

命令功能
+++++++++++++++
**show system ddm** 命令用来查看设备上光模块DDM信息。

命令格式
+++++++++++++++
单机模式：**show system ddm** [ *interface-name* ]

堆叠模式：**show system ddm** [ **all** | **member** *member-id* | *interface-name* ]

参数说明
+++++++++++++++
**all**：查看堆叠系统内所有设备的光模块DDM信息。

*member-id*：查看指定 *member-id* 设备的光模块DDM信息。

*interface-name*：接口名称。查看指定接口的光模块DDM信息。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查看设备上所有光模块DDM信息::

 ConnetOS> show system ddm
 Interface   Temp(C)  Voltage(V)  Bias(mA)  Tx Power(dBm)  Rx Power(dBm)  Module Type
 ----------  -------  ----------  --------  -------------  -------------  -----------
 te-1/1/6    36.24    3.39        8.10      -1.94          -2.80          SR/850nm
 te-1/1/7    28.45    3.35        5.14      -2.32          -2.75          SR/850nm
 te-1/1/34   32.33    3.37        8.09      -2.15          -2.24          SR/850nm
 qe-1/1/52   35.78    3.29        5.83      -3.61          -2.52          SR4/850nm
 qe-1/1/54   33.78    3.33        NA        NA             NA             SR4/850nm

show system fan
-------------------------------------------

命令功能
+++++++++++++++
**show system fan** 命令用来查询风扇的转速和PWM值。

命令格式
+++++++++++++++
单机模式：**show system fan** 

堆叠模式：**show system fan** [ **all** | **member** *member-id* ]

参数说明
+++++++++++++++
**all**：查看堆叠系统内所有设备的风扇信息。

*member-id*：查看指定 *member-id* 设备的风扇信息。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查询风扇的转速和PWM值::

 ConnetOS> show system fan
 Fan Status:
     Fan 1 : speed =  8925 RPM, PWM =  40%
     Fan 2 : speed =  8850 RPM, PWM =  40%
     Fan 3 : speed =  8850 RPM, PWM =  40%
     Fan 4 : speed =  8850 RPM, PWM =  40%
     Fan 5 : speed =  8850 RPM, PWM =  40%

show system memory-usage
-------------------------------------------

命令功能
+++++++++++++++
**show system memory-usage** 命令用来查询内存的使用率。

命令格式
+++++++++++++++
单机模式：**show system memory-usage** 

堆叠模式：**show system memory-usage** [ **all** | **member** *member-id* ]

参数说明
+++++++++++++++
**all**：查看堆叠系统内所有设备的内存使用率。

*member-id*：查看指定 *member-id* 设备的内存使用率。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查询内存使用率::

 ConnetOS> show system memory-usage
              total       used       free     shared    buffers     cached
 Mem:       2045380     550172    1495208      10640      16400     130444
 -/+ buffers/cache:     403328    1642052
 Swap:      7680300          0    7680300

show system processes
-------------------------------------------

命令功能
+++++++++++++++
**show system processes** 命令用来查看设备上对所有操作的系统处理过程。

命令格式
+++++++++++++++
单机模式：**show system processes**

堆叠模式：**show system processes** [ **all** | **member** *member-id* ]

参数说明
+++++++++++++++
**all**：查看堆叠系统内所有设备的系统处理过程

*member-id*：查看指定 *member-id* 设备的系统处理过程。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查看设备上对所有操作的系统处理过程::

 ConnetOS> show system processes
 USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
 root         1  0.0  0.2  28672  4648 ?        Ss   May12   0:13 /sbin/init
 root         2  0.0  0.0      0     0 ?        S    May12   0:00 [kthreadd]
 root         3  0.0  0.0      0     0 ?        S    May12   0:01 [ksoftirqd/0]
 root         5  0.0  0.0      0     0 ?        S<   May12   0:00 [kworker/0:0H]
 root         7  0.0  0.0      0     0 ?        S    May12   0:07 [rcu_sched]
 root         8  0.0  0.0      0     0 ?        S    May12   0:00 [rcu_bh]
 root         9  0.0  0.0      0     0 ?        S    May12   0:00 [migration/0]
 root        10  0.0  0.0      0     0 ?        S    May12   0:00 [watchdog/0]
 root        11  0.0  0.0      0     0 ?        S    May12   0:00 [watchdog/1]
 root        12  0.0  0.0      0     0 ?        S    May12   0:00 [migration/1]
 root        13  0.0  0.0      0     0 ?        S    May12   0:00 [ksoftirqd/1]
 root        15  0.0  0.0      0     0 ?        S<   May12   0:00 [kworker/1:0H]
 root        16  0.0  0.0      0     0 ?        S    May12   0:00 [watchdog/2]
 root        17  0.0  0.0      0     0 ?        S    May12   0:00 [migration/2]
 root        18  0.0  0.0      0     0 ?        S    May12   0:00 [ksoftirqd/2]
 root        20  0.0  0.0      0     0 ?        S<   May12   0:00 [kworker/2:0H]
 root        21  0.0  0.0      0     0 ?        S    May12   0:00 [watchdog/3]
 root        22  0.0  0.0      0     0 ?        S    May12   0:00 [migration/3]
 root        23  0.0  0.0      0     0 ?        S    May12   0:00 [ksoftirqd/3]
 root        25  0.0  0.0      0     0 ?        S<   May12   0:00 [kworker/3:0H]
 root        26  0.0  0.0      0     0 ?        S<   May12   0:00 [khelper]
 root        27  0.0  0.0      0     0 ?        S    May12   0:00 [kdevtmpfs]
 root        28  0.0  0.0      0     0 ?        S<   May12   0:00 [netns]
 root        29  0.0  0.0      0     0 ?        S    May12   0:00 [khungtaskd]
 root        30  0.0  0.0      0     0 ?        S<   May12   0:00 [writeback]
 root        31  0.0  0.0      0     0 ?        SN   May12   0:00 [ksmd]
 root        32  0.0  0.0      0     0 ?        SN   May12   0:00 [khugepaged]
 root        33  0.0  0.0      0     0 ?        S<   May12   0:00 [crypto]
 root        34  0.0  0.0      0     0 ?        S<   May12   0:00 [kintegrityd]
 root        35  0.0  0.0      0     0 ?        S<   May12   0:00 [bioset]
 root        36  0.0  0.0      0     0 ?        S<   May12   0:00 [kblockd]
 root        37  0.0  0.0      0     0 ?        S    May12   0:00 [khubd]
 root        38  0.0  0.0      0     0 ?        S<   May12   0:00 [devfreq_wq]
 root        39  0.0  0.0      0     0 ?        S    May12   0:04 [kworker/0:1]
 root        40  0.0  0.0      0     0 ?        S    May12   0:00 [kswapd0]
 root        41  0.0  0.0      0     0 ?        S<   May12   0:00 [vmstat]
 root        42  0.0  0.0      0     0 ?        S    May12   0:00 [fsnotify_mark]
 root        49  0.0  0.0      0     0 ?        S<   May12   0:00 [kthrotld]
 root        51  0.0  0.0      0     0 ?        S<   May12   0:00 [ipv6_addrconf]
 root        52  0.0  0.0      0     0 ?        S<   May12   0:00 [deferwq]
 root        58  0.0  0.0      0     0 ?        S    May12   0:00 [kworker/3:1]
 root        96  0.0  0.0      0     0 ?        S<   May12   0:00 [ata_sff]
 root        98  0.0  0.0      0     0 ?        S    May12   0:00 [scsi_eh_0]
 root        99  0.0  0.0      0     0 ?        S<   May12   0:00 [scsi_tmf_0]
 root       100  0.0  0.0      0     0 ?        S    May12   0:00 [scsi_eh_1]
 root       101  0.0  0.0      0     0 ?        S<   May12   0:00 [scsi_tmf_1]
 root       102  0.0  0.0      0     0 ?        S    May12   0:00 [scsi_eh_2]
 root       103  0.0  0.0      0     0 ?        S<   May12   0:00 [scsi_tmf_2]
 root       104  0.0  0.0      0     0 ?        S    May12   0:00 [scsi_eh_3]
 root       105  0.0  0.0      0     0 ?        S<   May12   0:00 [scsi_tmf_3]
 root       110  0.0  0.0      0     0 ?        S    May12   0:00 [scsi_eh_4]
 root       111  0.0  0.0      0     0 ?        S<   May12   0:00 [scsi_tmf_4]
 root       112  0.0  0.0      0     0 ?        S    May12   0:00 [scsi_eh_5]
 root       113  0.0  0.0      0     0 ?        S<   May12   0:00 [scsi_tmf_5]
 root       116  0.0  0.0      0     0 ?        S    May12   0:00 [scsi_eh_6]
 root       117  0.0  0.0      0     0 ?        S<   May12   0:00 [scsi_tmf_6]
 root       118  0.0  0.0      0     0 ?        S    May12   0:06 [usb-storage]
 root       119  0.0  0.0      0     0 ?        S    May12   0:06 [kworker/1:1]
 root       121  0.0  0.0      0     0 ?        S<   May12   0:00 [kworker/3:1H]
 root       122  0.0  0.0      0     0 ?        S<   May12   0:00 [kworker/2:1H]
 root       123  0.0  0.0      0     0 ?        S<   May12   0:00 [kworker/1:1H]
 root       130  0.0  0.0      0     0 ?        S<   May12   0:00 [kworker/0:1H]
 root       142  0.0  0.0      0     0 ?        S    May12   0:00 [jbd2/sda1-8]
 root       143  0.0  0.0      0     0 ?        S<   May12   0:00 [ext4-rsv-conver]
 root       174  0.0  0.0      0     0 ?        S    May12   0:00 [kworker/1:2]
 root       177  0.0  0.0      0     0 ?        S    May12   0:00 [kauditd]
 root       186  0.0  0.3  38456  6364 ?        Ss   May12   0:06 /lib/systemd/systemd-journald
 root       190  0.0  0.1  40668  3340 ?        Ss   May12   0:00 /lib/systemd/systemd-udevd
 root       257  0.0  0.0      0     0 ?        S<   May12   0:00 [kvm-irqfd-clean]
 root       405  0.0  0.1  19856  2540 ?        Ss   May12   0:00 /lib/systemd/systemd-logind
 message+   411  0.0  0.1  42124  3360 ?        Ss   May12   0:00 /usr/bin/dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation
 root       437  0.1  1.8 115756 37476 ?        S    May12   4:28 /switch/bin/rtrmgr -L local0.info
 root       490  0.0  0.1  62852  3360 ttyS1    Ss   May12   0:00 /bin/login --
 root       506  0.0  0.6  92760 14052 ?        S    May12   0:25 atp
 root       507  0.0  0.7  73828 15840 ?        S    May12   0:14 cardmgr
 root       508  0.0  2.5 134088 51636 ?        S    May12   2:16 sif
 root       585  0.0  0.4  14716  9044 ?        Ss   May12   0:00 dhclient eth0
 root       592  0.0  1.3  92636 26680 ?        S    May12   0:20 login
 root       605  0.0  0.1 258676  3208 ?        Ssl  May12   0:01 /usr/sbin/rsyslogd -n
 root       713  0.0  0.1  20216  2088 ?        Ss   May12   0:00 /usr/sbin/xinetd -pidfile /run/xinetd.pid -stayalive -inetd_compat -inetd_ipv6
 root       864  0.0  0.1  27504  2816 ?        Ss   May12   0:00 /usr/sbin/cron -f
 root       866  0.0  0.5  90336 11768 ?        S    May12   0:46 pcmgr
 root       867  0.0  0.9  98148 20220 ?        S    May12   4:00 stat
 root       870  0.0  0.7  87564 15684 ?        S    May12   0:20 lacp
 root       871  5.5  6.1 552332 125840 ?       Sl   May12 236:23 lcmgr
 root       875  0.0  0.8  95592 17600 ?        S    May12   1:25 lldp
 ntp        887  0.0  0.2  29168  4232 ?        Ss   May12   0:07 /usr/sbin/ntpd -p /var/run/ntpd.pid -g -u 106:111
 root       891  0.0  0.6  69032 13992 ?        S    May12   0:13 policy
 root       892  0.0  0.7  67408 15332 ?        S    May12   0:23 static_routes
 root       893  0.0  0.8  93424 18284 ?        S    May12   0:26 ospfv2
 root       986  0.0  0.1  21940  3736 ttyS1    S    May12   0:00 -bash
 root      1005  0.0  1.4 2538224 30524 ttyS1   Sl+  May12   0:13 ./rest
 root      1960  0.0  0.0      0     0 ?        S    May12   0:05 [kworker/3:0]
 root      7663  0.0  0.1  18976  2120 ?        Ss   16:00   0:00 in.telnetd: 192.168.1.128
 root      7664  0.0  0.1  61252  2912 pts/0    Ss   16:00   0:00 login -h 192.168.1.128 -p
 admin     7737  0.0  0.1  21876  3780 pts/0    S    16:01   0:00 -bash
 root      7758  0.0  0.0      0     0 ?        S    May13   0:13 [kworker/2:0]
 root      8430  0.0  0.0      0     0 ?        S    16:10   0:00 [kworker/2:2]
 root      9001  0.0  0.0      0     0 ?        S    08:46   0:00 [kworker/u8:1]
 root      9635  0.0  0.0      0     0 ?        S    16:26   0:00 [kworker/u8:0]
 root     12794  0.0  0.0      0     0 ?        S    17:10   0:00 [kworker/u8:2]
 admin    13082  0.0  0.1  13244  2808 pts/0    S+   17:15   0:00 /bin/sh /usr/bin/cli
 admin    13088  1.5  0.8 176648 16972 pts/0    S+   17:15   0:00 /switch/bin/cli_sh
 root     13582  0.0  0.0      0     0 ?        S    May14   0:02 [kworker/0:2]

show system rpsu
-------------------------------------------

命令功能
+++++++++++++++
**show system rpsu** 命令用来查询电源信息。

命令格式
+++++++++++++++
**show system rpsu**

**show system rpsu** [ **all** | **member** *member-id* ]

参数说明
+++++++++++++++
**all**：查看堆叠模式下所有设备的电源信息。

*member-id*：查看指定 *member-id* 设备的电源信息。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
本命令可以查询电源模块的SN号、温度、风扇转速、电压、电流和功率，并能对电源模块的状态进行监控展示。

配置举例
+++++++++++++++
# 查询电源信息::

 ConnetOS> show system rpsu
 RPSU 1:
     Module Status   : OK
     Serial Number   : SA020T051623000218
     Temperature     : 29     Centigrade
     IIN             : 0.43   A
     VIN             : 215.00 V
     PIN             : 89.00  W
     IOUT            : 6.16   A
     VOUT            : 12.02  V
     POUT            : 74.00  W
 RPSU 2:
     Module Status   : Unpresent

show system running-mode
-------------------------------------------

命令功能
+++++++++++++++
**show system running-mode** 查看系统的运行状态，单机还是堆叠。

命令格式
+++++++++++++++
**show system running-mode**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查看设备的运行状态::

 ConnetOS> show system running-mode
 Current mode      :  Standalone

show system serial-number
-------------------------------------------

命令功能
+++++++++++++++
**show system serial-number** 命令用来查询系统的SN信息，包括主板SN、电源模块SN以及光模块信息。

命令格式
+++++++++++++++
单机模式：**show system serial-number**

堆叠模式：**show system serial-number** [ **all** | **member** *member-id* ]

参数说明
+++++++++++++++
**all**：查看堆叠模式下所有设备的SN信息。

*member-id*：查看指定 *member-id* 设备的SN信息。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无。

配置举例
+++++++++++++++
# 查询产品序列号信息::

 ConnetOS> show system serial-number
 MotherBoard Serial Number : SW047110G826000010
 RPSU 1 Serial Number      : SA020T051623000218
 RPSU 2 is not ready.
 SFP+ te-1/1/6
     Vendor Name           : FINISAR CORP.
     Serial Number         : MUG0ZRH
     Product Number        : FTLX8571D3BCL
     Module Type           : SR/850nm
     Cable Length          : 300.0m
 SFP+ te-1/1/7
     Vendor Name           : CISCO-SUMITOMO
     Serial Number         : SPC150704J2
     Product Number        : SPP5100SR-C5
     Module Type           : SR/850nm
     Cable Length          : 300.0m
 SFP+ te-1/1/34
     Vendor Name           : FINISAR CORP.
     Serial Number         : MUG1702
     Product Number        : FTLX8571D3BCL
     Module Type           : SR/850nm
     Cable Length          : 300.0m
 QSFP+ qe-1/1/52
     Vendor Name           : Yunqi
     Serial Number         : RD160900420010
     Product Number        : RTXM320-571
     Module Type           : SR4/850nm
     Cable Length          : 300.0m
 QSFP+ qe-1/1/54
     Vendor Name           : FINISAR CORP
     Serial Number         : XUC06GP
     Product Number        : FTL410QE2C
     Module Type           : SR4/850nm
     Cable Length          : 100.0m

show system temperature
-------------------------------------------

命令功能
+++++++++++++++
**show system temperature** 命令用来查看设备的温度信息。

命令格式
+++++++++++++++
**show system temperature**

参数说明
+++++++++++++++
无

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查询设备温度信息::

 ConnetOS> show system temperature
 Temperature: 31 Centigrade
     Sensor 1 Temperature :  32 Centigrade
     Sensor 2 Temperature :  33 Centigrade
     Sensor 3 Temperature :  30 Centigrade

show system uptime
-------------------------------------------

命令功能
+++++++++++++++
**show system uptime** 命令用来查看系统启动时间。

命令格式
+++++++++++++++
单机模式：**show system uptime**

堆叠模式：**show system uptime** [ **all** | **member** *member-id* ]

参数说明
+++++++++++++++
**all**：查看堆叠模式下所有系统的启动时间。

*member-id*：查看指定 *member-id* 设备的系统启动时间。

命令模式
+++++++++++++++
运维模式

使用指南
+++++++++++++++
无

配置举例
+++++++++++++++
# 查看系统启动时间::

 ConnetOS> show system uptime
  15:57:49 up 3 days, 18:39,  1 user,  load average: 0.29, 0.11, 0.07




