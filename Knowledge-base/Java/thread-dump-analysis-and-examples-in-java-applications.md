---
title: Java 애플리케이션의 스레드 덤프 분석 및 예제
description: 
published: true
date: 2023-02-09T02:49:44.509Z
tags: 
editor: markdown
dateCreated: 2023-02-09T02:49:42.819Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Thread Dump Analysis and Examples in Java Applications***English** document is available*](/en/Knowledge-base/Java/thread-dump-analysis-and-examples-in-java-applications)
{.links-list}


# Java 애플리케이션의 스레드 덤프 분석 및 예제

스레드 덤프는 Java 애플리케이션의 성능 문제를 진단하는 데 유용한 도구입니다. 이 기사에서는 스레드 덤프가 무엇인지, 어떻게 생성하고 분석하는지 살펴보겠습니다. 또한 스레드 덤프를 사용하여 일반적인 Java 성능 문제를 해결하는 방법에 대한 몇 가지 예를 제공합니다.

## 스레드 덤프란?

스레드 덤프는 Java 프로세스의 모든 스레드 상태에 대한 스냅샷입니다. 스레드 덤프는 성능 문제, 교착 상태 및 기타 문제를 진단하는 데 유용할 수 있습니다.

## 스레드 덤프 생성 방법

스레드 덤프를 생성하는 몇 가지 방법이 있습니다.

### 제이스택

jstack 도구는 JDK에 포함되어 있으며 실행 중인 Java 프로세스에 대한 스레드 덤프를 생성하는 데 사용할 수 있습니다. jstack을 사용하려면 스레드 덤프를 생성하려는 Java 프로세스의 프로세스 ID를 지정하기만 하면 됩니다. 예를 들어:

```
jstack 12345
```

### jcmd

jcmd 도구는 JDK에도 포함되어 있으며 실행 중인 Java 프로세스에 대한 스레드 덤프를 생성하는 데 사용할 수 있습니다. jcmd를 사용하려면 스레드 덤프를 생성하려는 Java 프로세스의 프로세스 ID를 지정하기만 하면 됩니다. 예를 들어:

```
jcmd 12345 Thread.print
```

### IDE

Eclipse 및 IntelliJ IDEA와 같은 일부 IDE는 스레드 덤프 생성을 기본적으로 지원합니다. 예를 들어 Eclipse에서 **Window** > **Show View** > **Other** > **Debug** > **Threads**로 이동하여 스레드 덤프를 생성할 수 있습니다. 그런 다음 스레드 덤프를 생성하려는 Java 프로세스를 선택하고 **Dump Threads** 버튼을 클릭합니다.

## 스레드 덤프 분석 방법

스레드 덤프가 있으면 jstackAnalyzer 또는 VisualVM과 같은 도구를 사용하여 시각화할 수 있습니다. 또는 스레드 덤프를 수동으로 분석할 수 있습니다.

스레드 덤프를 분석할 때 다음 두 가지를 확인합니다.

1. "실행 가능" 상태에 있는 스레드. 현재 작업 중인 스레드입니다.
2. "대기" 상태에 있는 스레드. 이들은 다른 스레드가 작업을 수행하기를 기다리는 스레드입니다.

"대기" 상태의 스레드가 많이 표시되는 경우 일반적으로 성능 문제가 있음을 나타냅니다. 예를 들어 데이터베이스 연결을 기다리는 스레드가 많은 경우 데이터베이스가 느리다는 표시일 수 있습니다.

"실행 가능" 상태의 많은 스레드가 표시되면 일반적으로 CPU 병목 현상이 있음을 나타냅니다.

## 예

다음은 스레드 덤프를 사용하여 일반적인 Java 성능 문제를 해결하는 방법에 대한 몇 가지 예입니다.

### 교착상태

교착 상태는 두 개 이상의 스레드가 서로 작업을 대기하면서 차단되는 상황입니다. 예를 들어 스레드 A가 스레드 B가 작업을 수행하기를 기다리고 있고 스레드 B가 스레드 A가 작업을 수행하기를 기다리는 경우에 이러한 상황이 발생할 수 있습니다.

다음은 스레드 덤프의 교착 상태 예입니다.

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

이 스레드 덤프에서 Thread-1은 Thread-0이 작업을 수행하기를 기다리고 있고 Thread-0은 Thread-1이 작업을 수행하기를 기다리고 있음을 알 수 있습니다. 이것은 교착 상태입니다.

교착 상태를 해결하려면 교착 상태에 관련된 스레드를 식별하고 대기 중인 스레드를 파악해야 합니다. 이 예에서 Thread-1은 Thread-0이 작업을 수행하기를 기다리고 있고 Thread-0은 Thread-1이 작업을 수행하기를 기다리고 있습니다. 이 문제를 해결하려면 Thread-0이 Thread-1보다 먼저 작업을 수행하는지 또는 그 반대인지 확인해야 합니다.

### CPU 병목 현상

CPU 병목 현상은 CPU가 과부하되어 수요를 따라갈 수 없는 상황입니다. 예를 들어 동시에 실행 중인 스레드가 너무 많은 경우 이런 일이 발생할 수 있습니다.

다음은 스레드 덤프로 인한 CPU 병목 현상의 예입니다.

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

이 스레드 덤프에서 동시에 실행 중인 10개의 스레드가 있음을 알 수 있습니다. 이로 인해 CPU 병목 현상이 발생합니다.

CPU 병목 현상을 해결하려면 문제를 일으키는 스레드를 식별하고 스레드가 너무 많이 실행되는 이유를 파악해야 합니다. 이 예에서 스레드는 사용 중 루프를 실행하고 있습니다. 이 문제를 해결하려면 스레드가 필요 이상으로 사용 중인 루프를 실행하지 않도록 해야 합니다.

### 데이터베이스 병목 현상

데이터베이스 병목 현상은 데이터베이스가 느리고 수요를 따라갈 수 없는 상황입니다. 예를 들어 데이터베이스 쿼리가 너무 많은 경우 이런 일이 발생할 수 있습니다.

다음은 스레드 덤프로 인한 데이터베이스 병목 현상의 예입니다.

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

이 스레드 덤프에서 동시에 실행 중인 10개의 스레드가 있으며 모두 데이터베이스가 작동하기를 기다리고 있음을 알 수 있습니다. 이로 인해 데이터베이스 병목 현상이 발생합니다.

데이터베이스 병목 현상을 해결하려면 문제를 일으키는 스레드를 식별하고 스레드가 데이터베이스를 기다리는 이유를 파악해야 합니다. 이 예에서 스레드는 실행하는 데 오랜 시간이 걸리는 쿼리를 실행하고 있습니다. 이 문제를 해결하려면 쿼리를 최적화해야 합니다.

## 결론

스레드 덤프는 Java 애플리케이션의 성능 문제를 진단하는 데 유용한 도구입니다. 이 기사에서는 스레드 덤프가 무엇인지, 생성하는 방법 및 분석하는 방법에 대해 살펴보았습니다. 또한 스레드 덤프를 사용하여 일반적인 Java 성능 문제를 해결하는 방법에 대한 몇 가지 예를 제공했습니다.