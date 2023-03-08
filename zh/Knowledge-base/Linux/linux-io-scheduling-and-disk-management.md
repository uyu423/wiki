---
title: Linux I/O 调度和磁盘管理
description: 
published: true
date: 2023-02-11T17:32:34.237Z
tags: 
editor: markdown
dateCreated: 2023-02-11T17:32:32.645Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Linux I/O Scheduling and Disk Management***English** document is available*](/en/Knowledge-base/Linux/linux-io-scheduling-and-disk-management)
{.links-list}


# Linux I/O 调度和磁盘管理

Linux 内核的 I/O 调度器负责优化来自内核块层的块 I/O 请求提交给存储设备的顺序。此过程称为 I/O 调度，会对系统性能产生重大影响。

I/O 调度的三个主要目标：

- 通过重新排序请求以最小化查找来提高性能
- 通过合并请求提高性能
- 通过优先处理 I/O 优先级较低的进程的请求来减少延迟

Linux 内核中的 I/O 调度器旨在平衡这三个目标。

## I/O 调度算法

Linux 内核中提供了三种 I/O 调度算法：

- 截止时间 I/O 调度器
- Noop I/O 调度器
- CFQ I/O 调度器

Deadline I/O 调度器是 Linux 内核中默认的 I/O 调度器。它旨在通过优先处理来自 I/O 优先级较低的进程的请求来最大限度地减少延迟。

Noop I/O 调度器是一个非常简单的 I/O 调度器，它不会对请求重新排序。它通常用于 I/O 延迟非常低的设备，例如固态驱动器。

CFQ I/O 调度器是大多数 Linux 发行版上的默认 I/O 调度器。它旨在平衡 I/O 调度的三个目标：最小化寻道时间、合并请求和减少延迟。

## 更改 I/O 调度程序

可以使用 `blockdev` 命令的 `-s` 选项在每个设备的基础上更改 I/O 调度程序。例如，要将 `/dev/sda` 的 I/O 调度器更改为 Deadline I/O 调度器，您可以使用以下命令：

```
blockdev -s /dev/sda deadline
```

I/O 调度程序也可以在每个文件系统的基础上进行更改。要将 `/` 文件系统的 I/O 调度程序更改为 CFQ I/O 调度程序，您可以使用以下命令：

```
mount -o remount,ioscheduler=cfq /
```

## I/O 调度和磁盘管理

I/O 调度程序会对磁盘性能产生重大影响。例如，Deadline I/O 调度程序旨在通过优先处理来自 I/O 优先级较低的进程的请求来最大限度地减少延迟。这可以提高具有高 I/O 优先级的进程的性能，例如数据库服务器。

CFQ I/O 调度器旨在平衡 I/O 调度的三个目标：最小化寻道时间、合并请求和减少延迟。这可以提高大多数工作负载的性能。

## 结论

Linux内核中的I/O调度器负责优化内核块层的块I/O请求提交给存储设备的顺序。 I/O 调度有三个主要目标：通过重新排序请求以最小化查找来提高性能，通过合并请求来提高性能，以及通过优先处理来自 I/O 优先级较低的进程的请求来减少延迟。

I/O 调度程序会对磁盘性能产生重大影响。 Deadline I/O 调度程序旨在通过优先处理来自 I/O 优先级较低的进程的请求来最大限度地减少延迟。 CFQ I/O 调度器旨在平衡 I/O 调度的三个目标：最小化寻道时间、合并请求和减少延迟。

## 资源

- [Linux I/O 调度](https://www.kernel.org/doc/Documentation/block/ioprio.txt)
- [I/O 调度器](https://en.wikipedia.org/wiki/I/O_scheduler)
- [Noop I/O 调度程序](https://www.kernel.org/doc/Documentation/block/noop-iosched.txt)
- [CFQ I/O 调度程序](https://www.kernel.org/doc/Documentation/block/cfq-iosched.txt)
- [截止日期 I/O 调度器](https://www.kernel.org/doc/Documentation/block/deadline-iosched.txt)