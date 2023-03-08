---
title: Thread Dump Analysis and Examples in Java Applications
description: 
published: true
date: 2023-02-09T02:49:48.757Z
tags: 
editor: markdown
dateCreated: 2023-02-09T02:49:42.822Z
---

- [Análisis de volcado de subprocesos y ejemplos en aplicaciones Java***Spanish** document is available*](/es/Knowledge-base/Java/thread-dump-analysis-and-examples-in-java-applications)
{.links-list}
- [Java 应用程序中的线程转储分析和示例***Chinese Simplified** document is available*](/zh/Knowledge-base/Java/thread-dump-analysis-and-examples-in-java-applications)
{.links-list}
- [Java 애플리케이션의 스레드 덤프 분석 및 예제***Korean** document is available*](/ko/Knowledge-base/Java/thread-dump-analysis-and-examples-in-java-applications)
{.links-list}


# Thread Dump Analysis and Examples in Java Applications

Thread dumps are a valuable tool for diagnosing performance issues in Java applications. In this article, we'll take a look at what thread dumps are, how to generate them, and how to analyze them. We'll also provide some examples of how thread dumps can be used to troubleshoot common Java performance issues.

## What is a Thread Dump?

A thread dump is a snapshot of the state of all threads in a Java process. Thread dumps can be useful for diagnosing performance issues, deadlocks, and other problems.

## How to Generate a Thread Dump

There are a few different ways to generate a thread dump.

### jstack

The jstack tool is included in the JDK and can be used to generate a thread dump for a running Java process. To use jstack, simply specify the process ID of the Java process you want to generate a thread dump for. For example:

```
jstack 12345
```

### jcmd

The jcmd tool is also included in the JDK and can be used to generate a thread dump for a running Java process. To use jcmd, simply specify the process ID of the Java process you want to generate a thread dump for. For example:

```
jcmd 12345 Thread.print
```

### IDE

Some IDEs, such as Eclipse and IntelliJ IDEA, have built-in support for generating thread dumps. For example, in Eclipse, you can generate a thread dump by going to **Window** > **Show View** > **Other** > **Debug** > **Threads**. Then, select the Java process you want to generate a thread dump for and click the **Dump Threads** button.

## How to Analyze a Thread Dump

Once you have a thread dump, you can use a tool like jstackAnalyzer or VisualVM to visualize it. Alternatively, you can analyze the thread dump manually.

When analyzing a thread dump, you're looking for two things:

1. Threads that are in a "runnable" state. These are the threads that are currently doing work.
2. Threads that are in a "waiting" state. These are the threads that are waiting for other threads to do work.

If you see a lot of threads in a "waiting" state, that's usually an indication that there's a performance issue. For example, if there are a lot of threads waiting for a database connection, that could be an indication that the database is slow.

If you see a lot of threads in a "runnable" state, that's usually an indication that there's a CPU bottleneck.

## Examples

Here are some examples of how thread dumps can be used to troubleshoot common Java performance issues.

### Deadlock

A deadlock is a situation where two or more threads are blocked waiting for each other to do work. This can happen, for example, if Thread A is waiting for Thread B to do work, and Thread B is waiting for Thread A to do work.

Here's an example of a deadlock from a thread dump:

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

In this thread dump, we can see that Thread-1 is waiting for Thread-0 to do work, and Thread-0 is waiting for Thread-1 to do work. This is a deadlock.

To fix a deadlock, you need to identify the threads that are involved in the deadlock and figure out what they're waiting for. In this example, Thread-1 is waiting for Thread-0 to do work, and Thread-0 is waiting for Thread-1 to do work. To fix this, you need to make sure that Thread-0 does its work before Thread-1, or vice versa.

### CPU Bottleneck

A CPU bottleneck is a situation where the CPU is overloaded and can't keep up with the demand. This can happen, for example, if there are too many threads running at the same time.

Here's an example of a CPU bottleneck from a thread dump:

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

In this thread dump, we can see that there are 10 threads running at the same time. This is causing a CPU bottleneck.

To fix a CPU bottleneck, you need to identify the threads that are causing the problem and figure out why they're running so much. In this example, the threads are running a busy loop. To fix this, you need to make sure that the threads don't run the busy loop for longer than necessary.

### Database Bottleneck

A database bottleneck is a situation where the database is slow and can't keep up with the demand. This can happen, for example, if there are too many database queries.

Here's an example of a database bottleneck from a thread dump:

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

In this thread dump, we can see that there are 10 threads running at the same time, all of which are waiting for the database to do work. This is causing a database bottleneck.

To fix a database bottleneck, you need to identify the threads that are causing the problem and figure out why they're waiting for the database. In this example, the threads are running a query that is taking a long time to execute. To fix this, you need to optimize the query.

## Conclusion

Thread dumps are a valuable tool for diagnosing performance issues in Java applications. In this article, we've taken a look at what thread dumps are, how to generate them, and how to analyze them. We've also provided some examples of how thread dumps can be used to troubleshoot common Java performance issues.