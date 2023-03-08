---
title: 使用 Java 的 java.util.concurrent.locks.LockSupport 进行线程阻塞
description: 
published: true
date: 2023-01-31T13:04:28.573Z
tags: 
editor: markdown
dateCreated: 2023-01-31T13:04:25.081Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Working with Java's java.util.concurrent.locks.LockSupport for Thread Blocking***English** version of this document is available*](/en/Knowledge-base/Java/working-with-java-s-java-util-concurrent-locks-locksupport-for-thread-blocking)
{.links-list}



线程阻塞
===============

在 Java 中，线程阻塞是指线程无法继续其工作，因为它正在等待另一个资源。发生这种情况的原因有很多，例如当一个线程正在等待另一个线程完成其工作时，或者当一个线程正在等待资源变得可用时。

在任何一种情况下，线程都被称为阻塞。当一个线程被阻塞时，它无法运行任何代码，并且在阻塞被移除之前有效地停止。

在 Java 中有很多方法可以处理线程阻塞。一种常见的方法是使用 java.util.concurrent.locks.LockSupport 类。

LockSupport 是一个实用程序类，它提供了许多用于处理锁和阻塞的静态方法。它是 Java Concurrency Utilities 的一部分，Java Concurrency Utilities 是一组旨在帮助开发并发应用程序的类。

LockSupport 最常见的用途是阻塞一个线程，直到另一个线程完成它的工作。这可以通过 park() 和 unpark() 方法来完成。

park() 方法阻塞当前线程，直到在同一线程上调用 unpark() 方法。可以从任何线程调用 unpark() 方法，但它仅在线程当前处于停放状态时才有效。

如果线程当前未停放，则 unpark() 不执行任何操作。

下面是一个简单示例，说明如何使用 park() 和 unpark() 阻塞一个线程，直到另一个线程完成其工作。

```java
public static void main(String[] args) {
    Thread worker = new Thread(() -> {
        // do some work
        System.out.println("Worker is done.");

        // call unpark to unblock the main thread
        LockSupport.unpark(Thread.currentThread());
    });

    worker.start();

    System.out.println("Main thread is waiting for worker to finish.");

    // call park to block the main thread until unpark is called
    LockSupport.park();

    System.out.println("Main thread is done.");
}
```

在这个例子中，主线程调用 park() 来阻塞自己。工作线程做一些工作，然后调用 unpark() 来解锁主线程。

一旦主线程被解除阻塞，它将继续运行并打印“Main thread is done”。

LockSupport 还提供了许多其他方法来处理锁和阻塞。这些包括 tryLock()、isParked() 和 parkNanos()。

tryLock() 类似于park()，但它不会阻塞当前线程。相反，它会尝试获取锁并立即返回。如果锁不可用，则 tryLock() 返回 false。

isParked() 可用于检查线程当前是否被阻塞。如果线程被阻塞，则返回 true，如果线程未被阻塞，则返回 false。

parkNanos() 类似于 park()，但它会在指定的时间内阻塞当前线程。时间以纳秒为单位指定。

 LockSupport 是处理线程阻塞的有用工具。它提供了许多静态方法，可用于阻塞和取消阻塞线程，以及尝试和获取锁。