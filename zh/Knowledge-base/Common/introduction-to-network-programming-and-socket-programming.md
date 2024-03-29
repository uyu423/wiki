---
title: 网络编程和套接字编程简介
description: 
published: true
date: 2023-02-12T14:55:30.355Z
tags: 
editor: markdown
dateCreated: 2023-02-12T14:55:28.715Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Introduction to Network Programming and Socket Programming***English** document is available*](/en/Knowledge-base/Common/introduction-to-network-programming-and-socket-programming)
{.links-list}


# 网络编程和Socket编程简介

计算机使用各种协议相互通信，其中最常见的是传输控制协议 (TCP) 和用户数据报协议 (UDP)。

#### 传输控制协议 (TCP)

TCP是面向连接的协议，也就是说两台计算机必须建立连接才能进行通信。一旦建立连接，数据就可以双向传输。 TCP 是一种可靠的协议，这意味着数据按发送顺序传送，丢失或损坏的数据将重新传输。

#### 用户数据报协议（UDP）

UDP 是一种无连接协议，这意味着两台计算机无需先建立连接即可进行通信。不保证数据按发送顺序交付，并且不会重新传输丢失或损坏的数据。

#### 插座

套接字是两台计算机之间通信的端点。套接字可以与特定的端口号相关联，用于标识套接字。

#### 套接字编程

套接字编程是一种编写软件的方式，可以利用 TCP 和 UDP 协议的特性。套接字编程可用于创建各种应用程序，包括网络服务器、文件传输应用程序和聊天应用程序。

##### 创建套接字

为了创建套接字，必须首先创建一个套接字地址结构。此结构包含标识套接字所需的信息，包括地址族、端口号和 IP 地址。

一旦创建了套接字地址结构，就可以调用 socket() 函数来创建套接字。 socket() 函数将地址族、套接字类型和协议作为参数。

##### 连接到套接字

创建套接字后，您可以通过调用 connect() 函数连接到远程套接字。 connect() 函数将套接字和套接字地址结构作为参数。

##### 绑定套接字

为了从远程套接字接收数据，您必须首先将套接字绑定到本地端口。这是通过调用 bind() 函数来完成的。 bind() 函数将套接字和套接字地址结构作为参数。

##### 侦听传入连接

一旦将套接字绑定到本地端口，就可以通过调用 listen() 函数来侦听传入连接。 listen() 函数将套接字和积压工作作为参数。积压是在任何给定时间可以排队的最大挂起连接数。

##### 接受传入连接

调用 listen() 函数后，您可以通过调用 accept() 函数接受传入连接。 accept() 函数将套接字和正在连接的客户端地址作为参数。

##### 发送和接收数据

建立连接后，您可以使用 send() 和 recv() 函数发送和接收数据。 send() 函数将套接字、指向要发送的数据的指针、数据的长度和标志作为参数。 recv() 函数将套接字、指向用于存储数据的缓冲区的指针、缓冲区的长度和标志作为参数。

##### 关闭连接

完成发送和接收数据后，可以通过调用 close() 函数关闭连接。 close() 函数将套接字作为参数。