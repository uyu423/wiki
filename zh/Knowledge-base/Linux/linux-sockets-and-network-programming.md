---
title: Linux套接字和网络编程
description: 
published: true
date: 2023-02-12T00:32:25.603Z
tags: 
editor: markdown
dateCreated: 2023-02-12T00:32:18.943Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Linux Sockets and Network Programming***English** document is available*](/en/Knowledge-base/Linux/linux-sockets-and-network-programming)
{.links-list}


# Linux 套接字和网络编程

在本文中，我们将讨论 Linux 套接字和网络编程。我们将介绍它们是什么、它们如何工作以及一些常见的用例。我们还将提供一些 C 代码示例来说明如何使用它们。

## 什么是套接字？

在计算机网络中，套接字是双向或单向数据通信通道的端点。套接字可用于在两台计算机之间建立连接，然后可用于交换数据。

套接字可以是面向流的，也可以是面向数据报的。面向流的套接字在两台计算机之间提供可靠、有序和错误检查的连接。另一方面，面向数据报的套接字是无连接的，并且不保证数据将按照与发送时相同的顺序传送。

## 它们是如何工作的？

套接字通过在一台计算机上创建一个绑定到端口号的套接字对象来工作。然后可以使用此套接字对象连接到另一台计算机上的套接字，该套接字也绑定到端口号。一旦建立连接，就可以在两台计算机之间交换数据。

## 常见用例

您可能希望在应用程序中使用套接字的原因有很多。一些常见的用例包括：

- 创建聊天应用程序
- 创建多人游戏
- 将数据从一台计算机发送到另一台
- 创建一个网络服务器

## 代码示例

这里有一些 C 代码示例来说明如何使用套接字。

### 创建套接字

要创建套接字，您需要使用 socket() 函数。该函数接受三个参数：

- 套接字的地址族（例如 IPv4 的 AF_INET 或 IPv6 的 AF_INET6）
- 套接字的类型（例如，面向流的套接字的“SOCK_STREAM”或面向数据报的套接字的“SOCK_DGRAM”）
- 套接字的协议（例如 `IPPROTO_TCP` 用于 TCP 或 `IPPROTO_UDP` 用于 UDP）

```c
int sockfd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
```

### 连接到套接字

要连接到套接字，您需要使用 `connect()` 函数。该函数接受三个参数：

- 套接字文件描述符
- 要连接的套接字地址（转换为 `struct sockaddr *`）
- 地址的大小

```c
struct sockaddr_in addr;
addr.sin_family = AF_INET;
addr.sin_port = htons(80);
addr.sin_addr.s_addr = inet_addr("127.0.0.1");

connect(sockfd, (struct sockaddr *)&addr, sizeof(addr));
```

### 发送数据

要发送数据，您需要使用 send() 函数。该函数接受三个参数：

- 套接字文件描述符
- 要发送的数据（转换为 `void *`）
- 数据的大小

```c
char buf[1024];

send(sockfd, buf, sizeof(buf), 0);
```

### 接收数据

要接收数据，您需要使用 `recv()` 函数。这个函数有四个参数：

- 套接字文件描述符
- 用于存储数据的缓冲区（转换为 `void *`）
- 缓冲区的大小
- 标志（例如 `MSG_WAITALL` 等待所有数据到达）

```c
char buf[1024];

recv(sockfd, buf, sizeof(buf), MSG_WAITALL);
```

## 关闭套接字

要关闭套接字，您需要使用 close() 函数。此函数采用单个参数：

- 套接字文件描述符

```c
close(sockfd);
```

## 外部资源

- [Beej 的网络编程指南](https://beej.us/guide/bgnet/)
- [Linux 套接字编程示例](https://www.amazon.com/Linux-Socket-Programming-Example-Addison-Wesley/dp/0321524713)
- [Linux Socket 编程书](https://www.amazon.com/Linux-Socket-Programming-Mark-Twain/dp/188477749X)