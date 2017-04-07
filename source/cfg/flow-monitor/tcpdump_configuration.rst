TcpDump
=======================================

简介
---------------------------------------
TcpDump，即Dump the traffic on a network，是根据使用者的定义对网络上的数据包进行截获的包分析工具，也是Linux中强大的网络数据采集分析工具之一。

ConnetOS基于Debian Linux，天然支持TcpDump。

TcpDump可以将网络中传送的数据包的“头”完全截获下来提供分析。它支持针对网络层、协议、主机、网络或端口的过滤，并提供and、or、not等逻辑语句来帮助你去掉无用的信息。

TcpDump的总的输出格式为：系统时间 来源主机.端口 > 目标主机.端口 数据包参数
如下图所示::

 admin@ConnetOS:~ 1$ tcpdump
 tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
 listening on eth0, link-type EN10MB (Ethernet), capture size 262144 bytes
 16:00:54.674781 IP 192.168.1.31.telnet > 192.168.1.127.57388: Flags [P.], seq 1750927828:1750927979, ack 93009793, win 57, options [nop,nop,TS val 248778 ecr 1026263780], length 151
 16:00:54.675973 IP 192.168.1.127.57388 > 192.168.1.31.telnet: Flags [.], ack 151, win 4091, options [nop,nop,TS val 1026264589 ecr 248778], length 0
 ……

TcpDump使用
---------------------------------------
直接启动 **tcpdump**，将监视第一个网络接口上所有流过的数据包。虽然简单，但是数据信息太多，不利于数据包的截取和后续分析。可以使用各种参数进行数据包过滤。

TcpDump使用参数指定要监视数据包的类型、地址、端口等，根据具体的网络问题，充分利用这些过滤规则就能达到迅速定位故障的目的。

如果忘记了这个软件的用法，可以使用 **tcpdump --help** 查看使用方法::

 admin@ConnetOS:~ 1$ tcpdump --help
 tcpdump version 4.6.2
 libpcap version 1.6.2
 OpenSSL 1.0.1t  3 May 2016
 Usage: tcpdump [-aAbdDefhHIJKlLnNOpqRStuUvxX#] [ -B size ] [ -c count ]
		 [ -C file_size ] [ -E algo:secret ] [ -F file ] [ -G seconds ]
		 [ -i interface ] [ -j tstamptype ] [ -M secret ] [ --number ]
		 [ -Q in|out|inout ]
		 [ -r file ] [ -s snaplen ] [ --time-stamp-precision precision ]
		 [ -T type ] [ --version ] [ -V file ]
		 [ -w file ] [ -W filecount ] [ -y datalinktype ] [ -z command ]
		 [ -Z user ] [ expression ]

.. note::
 使用 **man tcpdump**，可以查看这些过滤参数的具体用法。

由于TcpDump对截获的数据没有进行彻底解码，为了网络故障分析方便，通常的解决办法是先使用带“-w”参数的tcpdump截获数据并保存到文件中，然后再使用其他程序进行解码分析。

TcpDump常见命令介绍
---------------------------------------

启动
+++++++++++++++++++++++++++++++++++++++
**tcpdump**

直接启动tcpdump将监视第一个网络接口上所有流过的数据包。

监视指定网络接口的数据包
+++++++++++++++++++++++++++++++++++++++
**tcpdump -i eth1**

如果不指定网卡，默认tcpdump只会监视第一个网络接口，一般是eth0，下面的例子都没有指定网络接口。

监听指定协议的数据
+++++++++++++++++++++++++++++++++++++++
监听ICMP协议的数据::

 tcpdump -i eth0 -nn 'icmp'

如果要监听TCP或UDP协议，只需要修改上例的icmp就可以了。

监听指定的主机
+++++++++++++++++++++++++++++++++++++++
抓取192.168.1.231接收到的包和发送的包::

 tcpdump -i eth0 -nn 'host 192.168.1.231'

抓取192.168.1.231发送的包::

 tcpdump -i eth0 -nn 'src host 192.168.1.231'

抓取192.168.1.231接收到的包::

 tcpdump -i eth0 -nn 'dst host 192.168.1.231'

监听指定端口
+++++++++++++++++++++++++++++++++++++++
监听主机的80端口收到和发送的所有数据包::

 tcpdump -i eth0 -nnA 'port 80'

监听指定主机和端口
+++++++++++++++++++++++++++++++++++++++
监听192.168.1.231主机通过80端口发送的数据包。多个条件可以用and，or连接::

 tcpdump -i eth0 -nnA 'port 80 and src host 192.168.1.231'


监听除某个端口外的其它端口
+++++++++++++++++++++++++++++++++++++++
监听非22端口的数据包::
 
 tcpdump -i eth0 -nnA '!port 22'



