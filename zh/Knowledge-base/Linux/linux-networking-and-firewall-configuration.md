---
title: Linux 网络和防火墙配置
description: 
published: true
date: 2023-02-11T23:32:29.598Z
tags: 
editor: markdown
dateCreated: 2023-02-11T23:32:27.473Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Linux Networking and Firewall Configuration***English** document is available*](/en/Knowledge-base/Linux/linux-networking-and-firewall-configuration)
{.links-list}


# Linux 网络和防火墙配置

由于绝大多数威胁来自互联网，良好的防火墙配置对于任何 Linux 服务器都至关重要。本指南将介绍使用流行的 iptables 工具配置防火墙的基础知识。

## 目录

- [什么是防火墙？](# what-is-a-firewall)
-[iptables](# iptables)
  - [安装 iptables](# installing-iptables)
  - [配置 iptables](# configuring-iptables)
- [结论](# conclusion)
- [资源](# resources)

## 什么是防火墙？

在计算中，防火墙是一种网络安全系统，它根据预先确定的安全规则监视和控制传入和传出的网络流量。防火墙通常在受信任的内部网络和不受信任的外部网络（例如 Internet）之间建立屏障。

## iptables

Iptables 是一种流行的防火墙工具，包含在大多数 Linux 发行版中。它使用一组规则来确定允许或阻止哪些流量。

### 安装 iptables

Iptables 包含在大多数 Linux 发行版中，并且可以与包管理器一起安装。例如，在基于 Debian 的系统上：

```
$ sudo apt-get install iptables
```

### 配置 iptables

Iptables 使用一组链来确定如何处理数据包。数据包可以被丢弃、拒绝或接受。默认链是“INPUT”、“FORWARD”和“OUTPUT”。

#### 规则

iptables 中的规则由多个匹配条件和一个目标组成。匹配标准可以是诸如协议（例如 TCP、UDP）、源和目标 IP 地址以及源和目标端口号之类的东西。目标可以是“DROP”、“REJECT”或“ACCEPT”。

##### 添加规则

可以使用 `iptables` 命令添加规则。例如，要丢弃所有传入流量：

```
$ iptables -A INPUT -j DROP
```

此规则将添加到“INPUT”链中，并将具有“DROP”目标，该目标将丢弃数据包。

##### 删除规则

可以使用 iptables 命令删除规则。例如，要删除以前的规则：

```
$ iptables -D INPUT 1
```

这将删除“INPUT”链中的第一条规则。

##### 保存规则

可以使用 iptables-save 命令保存规则。例如：

```
$ iptables-save > /etc/iptables.rules
```

这会将规则保存到“/etc/iptables.rules”文件中。

##### 加载规则

可以使用 iptables-restore 命令加载规则。例如：

```
$ iptables-restore < /etc/iptables.rules
```

这将从“/etc/iptables.rules”文件加载规则。

## 结论

本指南介绍了使用 iptables 配置防火墙的基础知识。有关详细信息，请参阅下面的资源。

## 资源

- [Iptables 教程](https://www.digitalocean.com/community/tutorials/a-deep-dive-into-iptables-and-netfilter-architecture)
- [如何在 Ubuntu 和 Debian 云服务器上使用 UFW 设置防火墙](https://www.digitalocean.com/community/tutorials/how-to-setup-a-firewall-with-ufw-on-an- ubuntu-and-debian-cloud-server)
- [如何在 CentOS 7 上使用 CSF 防火墙保护您的服务器](https://www.digitalocean.com/community/tutorials/how-to-secure-your-server-with-csf-firewall-on-centos-7 )