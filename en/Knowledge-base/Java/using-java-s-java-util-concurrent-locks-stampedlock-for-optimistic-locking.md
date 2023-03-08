---
title: Using Java's java.util.concurrent.locks.StampedLock for Optimistic Locking
description: 
published: true
date: 2023-02-01T07:17:44.366Z
tags: 
editor: markdown
dateCreated: 2023-02-01T07:17:40.595Z
---

- [낙관적 잠금을 위해 Java의 java.util.concurrent.locks.StampedLock 사용***Korean** version of this document is available*](/ko/Knowledge-base/Java/using-java-s-java-util-concurrent-locks-stampedlock-for-optimistic-locking)
{.links-list}
- [Java の java.util.concurrent.locks.StampedLock を楽観的ロックに使用する***Japanese** version of this document is available*](/ja/Knowledge-base/Java/using-java-s-java-util-concurrent-locks-stampedlock-for-optimistic-locking)
{.links-list}
- [使用 Java 的 java.util.concurrent.locks.StampedLock 进行乐观锁定***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Java/using-java-s-java-util-concurrent-locks-stampedlock-for-optimistic-locking)
{.links-list}



# Using Java's java.util.concurrent.locks.StampedLock for Optimistic Locking

Optimistic locking is a strategy to ensure that data is not concurrently modified by more than one thread. It is a widely used technique in concurrent programming to avoid the overhead of locking, while still providing some protection against data corruption.

Java's java.util.concurrent.locks.StampedLock provides a mechanism for optimistic locking. In this article we will explore how to use the StampedLock class to achieve optimistic locking in Java.

## What is Optimistic Locking?

Optimistic locking is a strategy to ensure that data is not concurrently modified by more than one thread. It is a widely used technique in concurrent programming to avoid the overhead of locking, while still providing some protection against data corruption.

When using optimistic locking, each thread first reads the data. If the data has not been modified by another thread, the thread can safely update the data. If the data has been modified by another thread, the update is aborted and the data is reloaded.

## How Does StampedLock Work?

StampedLock is a reentrant lock with three modes for locking: optimistic, read, and write.

Optimistic mode is the default mode. In optimistic mode, a thread can lock the lock without blocking. If the lock is already locked by another thread, the attempt to lock will fail.

Read mode allows multiple threads to lock the lock for reading. If the lock is already locked for writing, the attempt to lock will fail.

Write mode allows only one thread to lock the lock for writing. If the lock is already locked for reading or writing, the attempt to lock will fail.

## Using StampedLock

Here is a simple example of using StampedLock to protect data from concurrent modification:

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

In the example above, thread 1 tries to read the data. If the data has not been modified by another thread, the read will succeed and thread 1 can safely use the data. If the data has been modified by another thread, the read will fail and thread 1 will need to acquire a read lock to read the data.

Thread 2 tries to update the data. If the data has not been modified by another thread, the update will succeed. If the data has been modified by another thread, the update will fail and thread 2 will need to acquire a write lock to update the data.

## When to Use StampedLock

StampedLock is a useful tool for achieving optimistic locking in Java. When using optimistic locking, it is important to consider the trade-offs between performance and correctness.

Optimistic locking can improve performance by avoiding the overhead of locking. However, it comes at the cost of increased risk of data corruption. If data is frequently modified by concurrent threads, optimistic locking may not be the best strategy.

## Conclusion

In this article, we have explored how to use Java's java.util.concurrent.locks.StampedLock to achieve optimistic locking. We have also seen the trade-offs that need to be considered when using optimistic locking.