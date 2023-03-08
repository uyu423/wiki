---
title: Linux 网络堆栈和协议
description: 
published: true
date: 2023-02-11T22:32:17.022Z
tags: 
editor: markdown
dateCreated: 2023-02-11T22:32:15.419Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Linux Networking Stack and Protocols***English** document is available*](/en/Knowledge-base/Linux/linux-networking-stack-and-protocols)
{.links-list}


Linux 网络是一个庞大而复杂的话题。在本文中，我们将重点关注网络堆栈和协议。

## Linux 网络堆栈

Linux 网络堆栈由多个组件组成，每个组件都有自己的作用。

### 内核

Linux 网络堆栈的核心是内核。内核负责管理所有硬件资源，包括网络设备。它还实现了核心网络协议，例如 TCP/IP。

### 贝壳

内核之上是外壳。 shell 是一个用户界面，允许您与内核进行交互。它提供了一种执行命令和运行程序的方法。

### 配置文件

shell 使用配置文件来控制内核和运行在内核之上的程序的行为。最重要的网络配置文件是 /etc/hosts 文件，它将主机名映射到 IP 地址，以及 /etc/resolv.conf 文件，它定义了将用于解析主机名的 DNS 服务器。

### 实用程序

有许多实用程序可用于配置网络和排除网络故障。一些最重要的是用于配置网络接口的 ifconfig 和用于测试连通性的 ping。

## TCP/IP 协议栈

TCP/IP 协议栈是用于实现 Internet 核心功能的一组协议。它由四层组成：

- 应用层，即应用程序相互通信的层。
- 传输层，负责主机之间的端到端通信。
- 网络层，负责在主机之间路由流量。
- 链路层，负责在同一网络上的主机之间提供连接。

TCP/IP 堆栈在内核中实现，外壳提供用于配置和故障排除的实用程序。

## 参考

- https://www.tldp.org/LDP/GNU-Linux-Tools-Summary/html/c1022.htm
- https://www.thegeekstuff.com/2012/03/linux-networking-stack/
- https://www.redhat.com/en/blog/introduction-linux-networking-stack-part-1