---
layout: post
title: 'JavaLearning'
date: 2023-07-23
author: survivor
tags: Java Mysql Spring
---
「Java学习+面试材料」整理我学习&面试涵盖的方方面面
- [Java基础篇](#java基础篇)
    - [网络基础](#网络基础)
    - [HTTP协议](#http协议)

# Java基础篇

## 网络基础

### TCP协议

![]({{site.url}}/assets/img/tcpThreeFour.png)

**三次握手**：目的是为了建立可靠的通信信道，即全双工的通信，需要确定通信双方都具备完好的接收和发送能力

1. client   发送带有syn标志的数据包， **一次握手**进入syn_sent状态——server端确认：client发送正常，server端接收正常
2. server 发送带有syn、ack标志的数据包， **二次握手**进入syn_rcvd状态——client端确认：client发送接收都正常，server端发送接收都正常
3. client  发送带有ack标志的数据包，**三次握手**连接成功进入established状态——server端确认：client发送接收都正常，server端发送接收都正常

**为什么两次不行？**

1. 首先要理解三次握手都做了什么，从上面的图解及描述可以看出，如果只有两次，最终client端能够确认双方的接发都没问题，但是server无法确认client的接收和自身的发送是否正常，无法达到全双工通信的要求
2. 在网络拥塞的情况下，如果只有二次握手，只要服务端发出确认就可以建立链接，那客户端一直不发数据，服务端就会一直等待造成资源浪费

**四次挥手**

1. client 发送带有FIN标志的数据包，关闭与server的连接——client进入FIN-WAIT-1状态
2. server 收到FIN，发回一个ACK，确认序号为收到的序号+1——server 进入了CLOSE-WAIT的状态
3. server 发送一个FIN数据包，关闭与client的连接——client进入FIN-WAIT-2的状态
4. client 收到FIN，发回ACK确认，并将确认序号设置为收到序号+1——client进入TIME-WAIT的状态，server进入CLOSE状态，此时client等待2MSL（**Maximum Segment Lifetime**一个发送和一个回复所需的最大时间）的时间后依然没有收到信息，确认server已关闭，client也关闭了连接

### OSI与TCP/IP模型

![]({{site.url}}/assets/img/OSITCP.png)