---
title: Java 应用程序中的线程转储分析和示例
description: 
published: true
date: 2023-02-09T02:49:44.510Z
tags: 
editor: markdown
dateCreated: 2023-02-09T02:49:42.819Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Thread Dump Analysis and Examples in Java Applications***English** document is available*](/en/Knowledge-base/Java/thread-dump-analysis-and-examples-in-java-applications)
{.links-list}


# Java 应用程序中的线程转储分析和示例

线程转储是诊断 Java 应用程序性能问题的重要工具。在本文中，我们将了解什么是线程转储、如何生成它们以及如何分析它们。我们还将提供一些示例，说明如何使用线程转储来解决常见的 Java 性能问题。

## 什么是线程转储？

线程转储是 Java 进程中所有线程状态的快照。线程转储可用于诊断性能问题、死锁和其他问题。

## 如何生成线程转储

有几种不同的方法可以生成线程转储。

### j堆栈

jstack 工具包含在 JDK 中，可用于为正在运行的 Java 进程生成线程转储。要使用 jstack，只需指定要为其生成线程转储的 Java 进程的进程 ID。例如：

```
jstack 12345
```

### jcmd

jcmd 工具也包含在 JDK 中，可用于为正在运行的 Java 进程生成线程转储。要使用 jcmd，只需指定要为其生成线程转储的 Java 进程的进程 ID。例如：

```
jcmd 12345 Thread.print
```

### 集成开发环境

一些 IDE，例如 Eclipse 和 IntelliJ IDEA，内置了对生成线程转储的支持。例如，在 Eclipse 中，您可以通过转到 **Window** > **Show View** > **Other** > **Debug** > **Threads** 来生成线程转储。然后，选择要为其生成线程转储的 Java 进程并单击 **Dump Threads** 按钮。

## 如何分析线程转储

一旦有了线程转储，就可以使用 jstackAnalyzer 或 VisualVM 等工具将其可视化。或者，您可以手动分析线程转储。

在分析线程转储时，您正在寻找两件事：

1. 处于“可运行”状态的线程。这些是当前正在工作的线程。
2. 处于“等待”状态的线程。这些是等待其他线程工作的线程。

如果您看到很多线程处于“等待”状态，这通常表明存在性能问题。例如，如果有很多线程在等待数据库连接，这可能表明数据库速度很慢。

如果您看到很多线程处于“可运行”状态，这通常表明存在 CPU 瓶颈。

## 例子

以下是有关如何使用线程转储解决常见 Java 性能问题的一些示例。

### 死锁

死锁是两个或多个线程被阻塞等待彼此工作的情况。例如，如果线程 A 正在等待线程 B 工作，而线程 B 正在等待线程 A 工作，则可能会发生这种情况。

下面是线程转储中的死锁示例：

```
"Thread-1" #11 prio=5 os_prio=0 tid=0x000000000019f800 nid=0xb34 waiting for monitor entry [0x00000000001b2000]
   java.lang.Thread.State: BLOCKED (on object monitor)
	at Deadlock.run(Deadlock.java:22)
	- waiting to lock <0x00000000d7216928> (a java.lang.String)
	- locked <0x00000000d7216940> (a java.lang.String)

"Thread-0" #10 prio=5 os_prio=0 tid=0x000000000019e800 nid=0x5bc waiting for monitor entry [0x00000000001a2000]
   java.lang.Thread.State: BLOCKED (on object monitor)
	at Deadlock.run(Deadlock.java:17)
	- waiting to lock <0x00000000d7216940> (a java.lang.String)
	- locked <0x00000000d7216928> (a java.lang.String)
```

在此线程转储中，我们可以看到 Thread-1 正在等待 Thread-0 工作，而 Thread-0 正在等待 Thread-1 工作。这是一个僵局。

要修复死锁，您需要识别死锁中涉及的线程并弄清楚它们在等待什么。在本例中，Thread-1 正在等待 Thread-0 工作，而 Thread-0 正在等待 Thread-1 工作。要解决此问题，您需要确保 Thread-0 在 Thread-1 之前完成其工作，反之亦然。

### CPU 瓶颈

CPU 瓶颈是指 CPU 过载而无法满足需求的情况。例如，如果同时运行的线程过多，就会发生这种情况。

以下是线程转储中的 CPU 瓶颈示例：

```
"Thread-0" #10 prio=5 os_prio=0 tid=0x000000000019e800 nid=0x5bc runnable [0x00000000001a2000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-1" #11 prio=5 os_prio=0 tid=0x000000000019f800 nid=0xb34 runnable [0x00000000001b2000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-2" #12 prio=5 os_prio=0 tid=0x00000000001a0800 nid=0x1424 runnable [0x00000000001c2000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-3" #13 prio=5 os_prio=0 tid=0x00000000001a1800 nid=0xd74 runnable [0x00000000001d2000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-4" #14 prio=5 os_prio=0 tid=0x00000000001a2800 nid=0x1238 runnable [0x00000000001e2000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-5" #15 prio=5 os_prio=0 tid=0x00000000001a3800 nid=0x1a8 runnable [0x00000000001f2000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-6" #16 prio=5 os_prio=0 tid=0x00000000001a4800 nid=0x1658 runnable [0x0000000000202000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-7" #17 prio=5 os_prio=0 tid=0x00000000001a5800 nid=0x6e4 runnable [0x0000000000212000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-8" #18 prio=5 os_prio=0 tid=0x00000000001a6800 nid=0x1740 runnable [0x0000000000222000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)

"Thread-9" #19 prio=5 os_prio=0 tid=0x00000000001a7800 nid=0x15fc runnable [0x0000000000232000]
   java.lang.Thread.State: RUNNABLE
	at BusyThread.run(BusyThread.java:44)
```

在这个线程转储中，我们可以看到有 10 个线程同时运行。这会导致 CPU 瓶颈。

要修复 CPU 瓶颈，您需要确定导致问题的线程并找出它们运行如此多的原因。在此示例中，线程正在运行一个繁忙的循环。要解决此问题，您需要确保线程在繁忙循环中运行的时间不会超过必要的时间。

### 数据库瓶颈

数据库瓶颈是数据库运行缓慢且跟不上需求的情况。例如，如果数据库查询过多，就会发生这种情况。

以下是线程转储中的数据库瓶颈示例：

```
"Thread-0" #10 prio=5 os_prio=0 tid=0x000000000019e800 nid=0x5bc waiting for monitor entry [0x00000000001a2000]
   java.lang.Thread.State: BLOCKED (on object monitor)
	at Deadlock.run(Deadlock.java:17)
	- waiting to lock <0x00000000d7216940> (a java.lang.String)
	- locked <0x00000000d7216928> (a java.lang.String)

"Thread-1" #11 prio=5 os_prio=0 tid=0x000000000019f800 nid=0xb34 runnable [0x00000000001b2000]
   java.lang.Thread.State: RUNNABLE
	at QueryThread.run(QueryThread.java:24)

"Thread-2" #12 prio=5 os_prio=0 tid=0x00000000001a0800 nid=0x1424 runnable [0x00000000001c2000]
   java.lang.Thread.State: RUNNABLE
	at QueryThread.run(QueryThread.java:24)

"Thread-3" #13 prio=5 os_prio=0 tid=0x00000000001a1800 nid=0xd74 runnable [0x00000000001d2000]
   java.lang.Thread.State: RUNNABLE
	at QueryThread.run(QueryThread.java:24)

"Thread-4" #14 prio=5 os_prio=0 tid=0x00000000001a2800 nid=0x1238 runnable [0x00000000001e2000]
   java.lang.Thread.State: RUNNABLE
	at QueryThread.run(QueryThread.java:24)

"Thread-5" #15 prio=5 os_prio=0 tid=0x00000000001a3800 nid=0x1a8 runnable [0x00000000001f2000]
   java.lang.Thread.State: RUNNABLE
	at QueryThread.run(QueryThread.java:24)

"Thread-6" #16 prio=5 os_prio=0 tid=0x00000000001a4800 nid=0x1658 waiting for monitor entry [0x0000000000202000]
   java.lang.Thread.State: BLOCKED (on object monitor)
	at QueryThread.run(QueryThread.java:24)
	- waiting to lock <0x00000000d7216940> (a java.lang.String)
	- locked <0x00000000d7216928> (a java.lang.String)

"Thread-7" #17 prio=5 os_prio=0 tid=0x00000000001a5800 nid=0x6e4 waiting for monitor entry [0x0000000000212000]
   java.lang.Thread.State: BLOCKED (on object monitor)
	at QueryThread.run(QueryThread.java:24)
	- waiting to lock <0x00000000d7216940> (a java.lang.String)
	- locked <0x00000000d7216928> (a java.lang.String)

"Thread-8" #18 prio=5 os_prio=0 tid=0x00000000001a6800 nid=0x1740 waiting for monitor entry [0x0000000000222000]
   java.lang.Thread.State: BLOCKED (on object monitor)
	at QueryThread.run(QueryThread.java:24)
	- waiting to lock <0x00000000d7216940> (a java.lang.String)
	- locked <0x00000000d7216928> (a java.lang.String)

"Thread-9" #19 prio=5 os_prio=0 tid=0x00000000001a7800 nid=0x15fc waiting for monitor entry [0x0000000000232000]
   java.lang.Thread.State: BLOCKED (on object monitor)
	at QueryThread.run(QueryThread.java:24)
	- waiting to lock <0x00000000d7216940> (a java.lang.String)
	- locked <0x00000000d7216928> (a java.lang.String)
```

在这个线程转储中，我们可以看到有 10 个线程同时运行，它们都在等待数据库做工作。这导致了数据库瓶颈。

要修复数据库瓶颈，您需要确定导致问题的线程并找出它们等待数据库的原因。在此示例中，线程正在运行一个需要很长时间才能执行的查询。要解决此问题，您需要优化查询。

## 结论

线程转储是诊断 Java 应用程序性能问题的重要工具。在本文中，我们了解了什么是线程转储、如何生成它们以及如何分析它们。我们还提供了一些示例，说明如何使用线程转储来解决常见的 Java 性能问题。