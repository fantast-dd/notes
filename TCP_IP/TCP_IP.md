## TCP/IP详解（卷一：协议）
### 学习笔记

### 目录
#### [第1章  概述](#chapter 01)
#### 第2章  链路层
#### 第3章  IP：网际协议
#### 第6章  ICMP：Internet控制报文协议
#### 第11章 UDP：用户数据报协议
#### 第17章 TCP：传输控制协议
--

#### chapter 01
##### 分层
	协议栈 | 操作系统
	------| ------
	应用层 | 用户层
	传输层 | 内核层
	网络层 | 内核层
	链路层 | 内核层
##### 数据封装
当应用程序用TCP传送数据时，数据被送入协议栈中，然后逐个通过每一层直到被当做一串比特流送入网络。其中每一层对收到的数据都要增加一些首部信息（有时还要增加尾部信息），该过程如图1-7所示。

协议栈 | 数据格式
------|--------
应用层 | 应用数据
传输层 | TCP段（TCP segment）/ UDP数据报（UDP datagram）
网络层 | IP数据报（IP datagram）
链路层 | 帧（Frame）
![图1-7](https://raw.githubusercontent.com/fantast-dd/notes/master/TCP_IP/chapter-01/1-7.png)
<center>图1-7 数据进入协议栈时的封装过程</center>
##### 分用
当目的主机收到一个以太网数据帧时，数据就开始从协议栈中由底向上升，同时去掉各层协议加上的报文首部。每层协议盒都要去检查报文首部中的协议标识，以确定接受数据的上层协议。这个过程称作分用（Demultiplexing），图1-8显示了该过程是如何发生的。
![图1-8](https://raw.githubusercontent.com/fantast-dd/notes/master/TCP_IP/chapter-01/1-8.png)
<center>图1-8 以太网数据帧的分用过程</center>

--

#### 第2章 链路层
##### 以太网封装和IEEE 802封装（如图2-1所示）
![图2-1](https://raw.githubusercontent.com/fantast-dd/notes/master/TCP_IP/chapter-02/2-1.jpeg)
CRC（Cyclic Redundancy Check）：用户帧内后续字节差错的循环冗余码检验（检验和）
最小长度：802.3标准定义的帧和以太网的帧都有最小长度的要求。802.3规定数据部分必须至少为38字节，而对于以太网，则要求至少46字节。为了保证这一点，必须在不足的空间插入填充（pad）字节。
##### 最大传输单元MTU
以太网：1500字节，802.3：1492字节
##### 路径MTU
两台通信主机路径中的最小MTU

--

#### 第三章 IP：网际协议
##### 引言
IP是TCP/IP协议族中最为核心的协议。所有的TCP，UDP，ICMP及IGMP数据都以IP数据报的格式传输

不可靠（unreliable）：不能保证IP数据报能成功地到达目的地

无连接（connectionless）：不维护任何关于后续数据报的状态信息。每个数据报的处理是相互独立的

##### IP首部
IP数据报的格式如图3-1所示。普通的IP首部长为20个字节，除非含有特殊字段。
![图3-1](https://raw.githubusercontent.com/fantast-dd/notes/master/TCP_IP/chapter-03/3-1.png)
<center>图3-1 IP数据报格式及首部中的各字段</center>

4位版本：协议版本号，IPv4 or IPv6

4位首部长度

8位服务类型（TOS）

16位总长度（字节数）：整个IP数据报的长度，以字节为单位

16位标识：唯一地标识主机发送的每一份数据报。通常每发送一份报文它的值就会加1

3位标志：

13位片偏移：

8位生存时间（TTL）：设置数据报可以经过的最多路由器数，指定了数据报的生存时间。

8位协议：对数据报进行分用，根据它识别是哪个协议向IP传送数据

16位首部检验和：根据IP首部计算的检验和码。它不对首部后面的数据进行计算。

32位源IP地址

32位目地IP地址

选项（如果有）

数据

--

#### 第6章 ICMP：Internet控制报文协议
##### 引言
ICMP报文是在IP数据报内部被传输的，如图6-1所示。
![图6-2](https://raw.githubusercontent.com/fantast-dd/notes/master/TCP_IP/chapter-06/6-1.png)
<center>图6-1 ICMP封装在IP数据报内部</center>

ICMP报文的格式如图6-2所示。所有报文的前四个字节都是一样的，但是剩下的其他字节则互不相同。
![图6-2](https://raw.githubusercontent.com/fantast-dd/notes/master/TCP_IP/chapter-06/6-2.png)
<center>图6-2 ICMP报文</center>

--

#### 第11章 UDP：用户数据报协议
##### 引言
UDP是一个简单的面向数据报的传输层协议：进程的每个输出操作都正好产生一个UDP数据报，并组装成一份待发送的IP数据报。

UDP数据报封装成一份数据报的格式如图11-1所示。
![图11-1](https://raw.githubusercontent.com/fantast-dd/notes/master/TCP_IP/chapter-11/11-1.png)
<center>图11-1 UDP封装</center>

UDP不提供可靠性：它把应用程序传给IP层的数据发送出去，但是并不保证它们能到达目的地。

应用程序必须关心IP数据报的长度。如果它超过网络的MTU，那么就要对IP数据报进行分片。

##### UDP首部
UDP首部的各字段如图11-2所示。
![图11-2](https://raw.githubusercontent.com/fantast-dd/notes/master/TCP_IP/chapter-11/11-2.png)
<center>图11-2 UDP首部</center>

16位UDP长度：UDP首部和UDP数据的字节长度。该字段的最小值为8字节。

##### UDP检验和
