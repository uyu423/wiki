---
title: Linux 系统监控和日志记录
description: 
published: true
date: 2023-02-12T10:32:20.537Z
tags: 
editor: markdown
dateCreated: 2023-02-12T10:32:13.958Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Linux System Monitoring and Logging***English** document is available*](/en/Knowledge-base/Linux/linux-system-monitoring-and-logging)
{.links-list}


# Linux 系统监控和日志记录

Linux 操作系统有许多用于监控系统性能和活动的工具。这些工具可用于检查系统的健康状况以及诊断和排除问题。

可以使用测量 CPU 和内存使用情况、网络流量、磁盘活动和进程信息的工具来监控系统性能。可以使用跟踪系统日志文件、用户活动和进程信息的工具来监视系统活动。

## CPU 和内存使用情况

top 命令是一个通用的系统活动监视器。它可以用来查看当前正在运行的进程的信息，包括进程ID、用户ID、CPU使用率和内存使用率。 htop 命令是 top 的一种更用户友好的替代方法。

vmstat 命令可用于查看虚拟内存的信息，包括内存使用情况、磁盘活动和进程信息。 iostat 命令可用于查看有关磁盘活动的信息。

free 命令可用于查看有关系统上可用和已用内存量的信息。 -m 选项以兆字节为单位显示输出。

## 网络流量

iftop 命令可用于查看有关网络流量的信息。 tcpdump 命令可用于捕获和查看网络流量。

## 磁盘活动

iotop 命令可用于查看有关磁盘活动的信息。 -d 选项以兆字节/秒为单位显示输出。

## 处理信息

ps 命令可用于查看有关进程的信息。 -e 选项显示所有进程。 -f 选项显示每个进程的完整命令行。

pstree 命令可用于查看进程树。 -p 选项显示每个进程的进程 ID。

lsof 命令可用于查看有关打开文件的信息。 -n 选项显示网络文件。

kill 命令可用于终止进程。 -9 选项向进程发送 SIGKILL 信号。

## 系统日志文件

/var/log/messages 文件包含系统消息。 /var/log/secure 文件包含安全消息。 /var/log/apache2/access.log 文件包含 Apache 访问日志。

## 用户活动

w 命令可用于查看有关用户活动的信息。 -u 选项显示特定用户的信息。

last 命令可用于查看有关上次登录用户的信息。 -x 选项显示有关系统重新引导的信息。

who 命令可用于查看有关当前登录用户的信息。

## 结论

Linux 提供了许多用于监视系统性能和活动的工具。这些工具可用于检查系统的健康状况以及诊断和排除问题。