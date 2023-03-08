---
title: Java 的 java.util.concurrent.locks.Condition 线程信号指南
description: 
published: true
date: 2023-02-04T02:55:25.532Z
tags: 
editor: markdown
dateCreated: 2023-02-04T02:55:20.086Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [A Guide to Java's java.util.concurrent.locks.Condition for Thread Signaling***English** document is available*](/en/Knowledge-base/Java/a-guide-to-java-s-java-util-concurrent-locks-condition-for-thread-signaling)
{.links-list}



# Java 的 java.util.concurrent.locks.Condition 线程信号指南

线程经常需要相互通信。例如，一个线程可能需要告诉其他线程一项任务已完成，或者共享资源可用。

Java 有一个内置的线程通信机制，称为 java.util.concurrent.locks.Condition 类。在本文中，我们将了解如何使用“条件”在线程之间进行通信。

## 什么是条件？

Condition 是一个 Java 类，它允许线程等待或向其他线程发出信号。它是 java.util.concurrent.locks 包的一部分，该包还包含 Lock 类。

Condition 与 Lock 一起使用以提供更灵活的方式来控制线程何时可以运行。使用Lock，线程只有在持有锁时才能运行。使用 Condition，一个线程只有在另一个线程发出信号时才能运行。

## 使用条件

Condition 与 Lock 一起使用以提供更灵活的方式来控制线程何时可以运行。使用Lock，线程只有在持有锁时才能运行。使用 Condition，一个线程只有在另一个线程发出信号时才能运行。

这是一个如何使用条件的简单示例。假设我们有一个可以处于两种状态之一的共享资源：空或满。我们有两个线程：一个产生资源，一个消耗它。

我们要确保消费者线程仅在资源处于“满”状态时才尝试使用资源，而生产者线程仅在其处于“空”状态时才尝试生产资源。为此，我们可以使用锁和条件：


```java
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class Resource {
    private final Lock lock = new ReentrantLock();
    private final Condition isEmpty = lock.newCondition();
    private final Condition isFull = lock.newCondition();

    private boolean empty = true;

    public void produce() throws InterruptedException {
        lock.lock();
        try {
            while (!empty) {
                isEmpty.await();
            }
            // produce resource
            empty = false;
            isFull.signalAll();
        } finally {
            lock.unlock();
        }
    }

    public void consume() throws InterruptedException {
        lock.lock();
        try {
            while (empty) {
                isFull.await();
            }
            // consume resource
            empty = true;
            isEmpty.signalAll();
        } finally {
            lock.unlock();
        }
    }
}
```

在此示例中，`produce()` 方法首先检查资源是否为空。如果不是，它会一直等到它为空（通过调用 isEmpty.await() ）。一旦资源为空，它就会生成资源并向所有等待的线程发出信号（通过调用 isFull.signalAll() ）。

同样，`consume()` 方法首先检查资源是否已满。如果不是，它会一直等到它已满（通过调用 isFull.await() ）。一旦资源已满，它就会消耗资源并向任何等待的线程发出信号（通过调用 isEmpty.signalAll() ）。

## 其他方法

Condition 还提供了一个 signal() 方法，它可以唤醒正在等待该条件的单个线程。如果有多个线程在等待，则随机选择其中一个唤醒。

还有一个 `awaitUninterruptibly()` 方法，它与 `await()` 类似，只是它不会在线程中断时抛出 InterruptedException。

## 使用条件的提示

以下是使用条件的一些提示：

- 始终在循环中调用 `await()` 或 `signal()`。这是因为 `await()` 可以被中断（通过调用 `interrupt()`），并且 `signal()` 可以丢失（如果多个线程正在等待，只有其中一个会被唤醒）。

- 注意不要在锁外调用 `await()` 或 `signal()`。如果这样做，另一个线程可能会在您检查条件和调用 `await()` 或 `signal()` 之间获取锁。这可能会导致您的程序冻结。

- 当使用多个条件时，注意不要对所有条件使用同一个锁。这可能会导致死锁。

## 结论

在本文中，我们了解了如何使用 Java 的 java.util.concurrent.locks.Condition 类进行线程通信。我们还看到了一些使用条件的技巧。