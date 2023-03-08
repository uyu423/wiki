---
title: 使用 Java 的 java.util.concurrent.locks.StampedLock 进行乐观锁定
description: 
published: true
date: 2023-02-01T07:17:42.132Z
tags: 
editor: markdown
dateCreated: 2023-02-01T07:17:40.600Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Using Java's java.util.concurrent.locks.StampedLock for Optimistic Locking***English** version of this document is available*](/en/Knowledge-base/Java/using-java-s-java-util-concurrent-locks-stampedlock-for-optimistic-locking)
{.links-list}



# 使用 Java 的 java.util.concurrent.locks.StampedLock 进行乐观锁

乐观锁是一种确保数据不被多个线程同时修改的策略。它是并发编程中广泛使用的一种技术，可以避免锁定的开销，同时仍然提供一些防止数据损坏的保护。

Java 的 java.util.concurrent.locks.StampedLock 提供了一种乐观锁定机制。在本文中，我们将探讨如何使用 StampedLock 类在 Java 中实现乐观锁定。

## 什么是乐观锁？

乐观锁是一种确保数据不被多个线程同时修改的策略。它是并发编程中广泛使用的一种技术，可以避免锁定的开销，同时仍然提供一些防止数据损坏的保护。

使用乐观锁时，每个线程首先读取数据。如果数据没有被另一个线程修改过，线程可以安全地更新数据。如果数据已被另一个线程修改，更新将中止并重新加载数据。

## StampedLock 如何工作？

StampedLock 是一种可重入锁，具有三种锁定模式：乐观、读取和写入。

乐观模式是默认模式。在乐观模式下，一个线程可以在不阻塞的情况下锁定锁。如果锁已经被另一个线程锁定，则锁定尝试将失败。

读取模式允许多个线程锁定锁以进行读取。如果锁已经被锁定用于写入，则锁定尝试将失败。

写模式只允许一个线程为写加锁。如果锁已经被锁定用于读取或写入，则锁定尝试将失败。

## 使用 StampedLock

下面是一个使用 StampedLock 保护数据免受并发修改的简单示例：

```java
import java.util.concurrent.locks.StampedLock;

public class OptimisticLocking {

    private static final StampedLock lock = new StampedLock();
    private static int data = 0;

    public static void main(String[] args) {
        // thread 1 tries to read data
        long stamp = lock.tryOptimisticRead();
        int localData = data;
        if (!lock.validate(stamp)) {
            // data has been modified, need to acquire read lock
            stamp = lock.readLock();
            try {
                localData = data;
            } finally {
                lock.unlockRead(stamp);
            }
        }
        // data has not been modified, can use localData safely

        // thread 2 tries to update data
        long stamp = lock.writeLock();
        try {
            data = localData + 1;
        } finally {
            lock.unlockWrite(stamp);
        }
    }
}
```

在上面的示例中，线程 1 尝试读取数据。如果数据没有被另一个线程修改，读取将成功，线程 1 可以安全地使用数据。如果数据已经被另一个线程修改，读取将失败，线程 1 将需要获取读取锁来读取数据。

线程 2 尝试更新数据。如果数据没有被另一个线程修改过，更新就会成功。如果数据已被另一个线程修改，更新将失败，线程 2 将需要获取写锁来更新数据。

## 何时使用 StampedLock

StampedLock 是在 Java 中实现乐观锁定的有用工具。使用乐观锁定时，重要的是要考虑性能和正确性之间的权衡。

乐观锁定可以通过避免锁定的开销来提高性能。但是，这是以增加数据损坏的风险为代价的。如果数据被并发线程频繁修改，乐观锁定可能不是最好的策略。

## 结论

在本文中，我们探索了如何使用Java的java.util.concurrent.locks.StampedLock来实现乐观锁。我们还看到了使用乐观锁定时需要考虑的权衡。