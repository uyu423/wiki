---
title: Linux 中断和信号
description: 
published: true
date: 2023-02-11T14:32:22.769Z
tags: 
editor: markdown
dateCreated: 2023-02-11T14:32:21.107Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Linux Interrupts and Signals***English** document is available*](/en/Knowledge-base/Linux/linux-interrupts-and-signals)
{.links-list}


# Linux 中断和信号

中断是需要操作系统内核注意的事件。当中断发生时，内核可能会挂起当前进程，并执行一个特殊的中断处理程序来处理该事件。

信号是由内核或另一个进程发送给进程的软件中断。信号可能由用户生成，例如使用 kill 命令，或由操作系统响应事件（例如分段错误）生成。

中断和信号很相似，但有一些重要的区别。

## 中断

中断由硬件产生，并导致内核挂起当前进程并执行特殊的中断处理程序。

中断可以由用户生成，例如使用 kill 命令，或由操作系统响应事件（例如分段错误）生成。

## 信号

信号是发送到进程的软件中断。信号可能由用户生成，例如使用 kill 命令，或由操作系统响应事件（例如分段错误）生成。

信号由内核或另一个进程生成。当信号产生时，内核可能会挂起当前进程，并执行一个特殊的信号处理程序来处理该事件。

## 差异

中断和信号很相似，但有一些重要的区别：

- 中断由硬件产生，而信号由内核或其他进程产生。
- 中断导致内核挂起当前进程并执行特殊的中断处理程序。信号可能会导致内核挂起当前进程并执行特殊的信号处理程序。
- 中断可以由用户产生，而信号只能由内核或其他进程产生。

## 外部资源

- [维基百科：中断](https://en.wikipedia.org/wiki/Interrupt)
- [维基百科：信号（计算）](https://en.wikipedia.org/wiki/Signal_(computing))
- [Linux 内核文档：中断](https://www.kernel.org/doc/Documentation/virtual/kvm/async_pf.txt)
- [Linux 内核文档：信号](https://www.kernel.org/doc/Documentation/signals.txt)