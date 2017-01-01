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

####chapter 01
##### 分层
	协议栈 | 操作系统
	------| ------
	应用层 | 用户层
	传输层 | 内核层
	网络层 | 内核层
	链路层 | 内核层
##### 数据封装
##### 当应用程序用TCP传送数据时，数据被送入协议栈中，然后逐个通过每一层直到被当做一串比特流送入网络。其中每一层对收到的数据都要增加一些首部信息（有时还要增加尾部信息），该过程如图1-7所示。
	协议栈 | 数据格式
	------|--------
	应用层 | 应用数据
	传输层 | TCP段（TCP segment）/ UDP数据报（UDP datagram）
	网络层 | IP数据报（IP datagram）
	链路层 | 帧（Frame）
![图1-7](https://raw.githubusercontent.com/fantast-dd/notes/master/TCP_IP/chapter-01/1-7.png)
<center>图1-7 数据进入协议栈时的封装过程</center>
##### 分用
##### 当目的主机收到一个以太网数据帧时，数据就开始从协议栈中由底向上升，同时去掉各层协议加上的报文首部。每层协议盒都要去检查报文首部中的协议标识，以确定接受数据的上层协议。这个过程称作分用（Demultiplexing），图1-8显示了该过程是如何发生的。
![图1-8](https://raw.githubusercontent.com/fantast-dd/notes/master/TCP_IP/chapter-01/1-8.png)
<center>图1-8 以太网数据帧的分用过程</center>

--
####第2章 链路层
#####以太网封装和IEEE 802封装
