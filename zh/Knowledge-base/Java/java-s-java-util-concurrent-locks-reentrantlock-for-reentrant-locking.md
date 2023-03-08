---
title: Java 的 java.util.concurrent.locks.ReentrantLock 用于可重入锁定
description: 
published: true
date: 2023-02-12T02:55:26.609Z
tags: 
editor: markdown
dateCreated: 2023-02-12T02:55:25.083Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Java's java.util.concurrent.locks.ReentrantLock for Reentrant Locking***English** document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-locks-reentrantlock-for-reentrant-locking)
{.links-list}


# Java 的 java.util.concurrent.locks.ReentrantLock 用于可重入锁定

可重入锁定是一种流行的机制，用于确保 Java 应用程序中的线程安全。在本文中，我们将仔细研究 ReentrantLock 在 Java 中的工作原理。

ReentrantLock 是 Java 并发实用程序的一部分，并实现 Lock 接口。它提供了比 Java 中可用的内部锁更复杂的锁定机制。

ReentrantLock 公平策略

ReentrantLock 有两种公平策略：

* 公平的
* 不公平

公平策略防止线程在等待锁时饿死。在一个公平的ReentrantLock中，当多个线程都在等待锁时，等待时间最长的线程最先获得锁。

非公平策略是默认策略，不保证线程获取锁的顺序。该策略比公平策略更有效。

ReentrantLock 的工作原理

ReentrantLock 使用内部锁对象来表示锁定状态。当线程调用 lock() 方法时，如果锁可用，它就会获取锁。如果锁不可用，则线程进入等待状态。

当线程获取锁时，它会获得一个保持计数。线程可以通过调用 unlock() 方法来释放锁。只有当线程的保持计数变为零时，锁才会被释放。

如果一个线程试图获取它已经持有的锁，则该线程的持有计数会增加。

线程可以通过调用 unlock() 方法释放它不持有的锁。这会导致 IllegalMonitorStateException。

tryLock() 方法

tryLock() 方法用于获取锁。如果锁可用，则线程获取锁并且该方法返回 true。如果锁不可用，则线程不会阻塞并且该方法返回 false。

tryLock(long time, TimeUnit unit) 方法用于在指定时间内获取锁。如果锁可用，则线程获取锁并且该方法返回 true。如果锁不可用，线程将被阻塞，直到指定的时间到期。如果时间在锁可用之前到期，则线程不会获取锁并且该方法返回 false。

lockInterruptibly() 方法

lockInterruptibly() 方法用于获取锁。如果锁可用，则线程获取锁。如果锁不可用，线程将被阻塞，直到锁可用或线程被中断。

新条件（）方法

newCondition() 方法创建一个绑定到此 Lock 实例的新 Condition 对象。

isHeldByCurrentThread() 方法

如果当前线程持有此锁，则 isHeldByCurrentThread() 方法返回 true，否则返回 false。

isLocked() 方法

如果此锁被任何线程持有，则 isLocked() 方法返回 true，否则返回 false。

getQueueLength() 方法

getQueueLength() 方法返回等待获取此锁的线程数。

hasQueuedThreads() 方法

如果有线程在等待获取此锁，则 hasQueuedThreads() 方法返回 true，否则返回 false。

isFair() 方法

如果此锁是公平的，则 isFair() 方法返回 true，否则返回 false。

getHoldCount() 方法

getHoldCount() 方法返回当前线程持有的锁的数量。

toString() 方法

toString() 方法返回此锁的字符串表示形式。