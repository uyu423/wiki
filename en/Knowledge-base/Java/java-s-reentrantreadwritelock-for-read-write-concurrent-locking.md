---
title: Java's ReentrantReadWriteLock for Read-Write Concurrent Locking
description: 
published: true
date: 2023-02-23T21:32:31.289Z
tags: 
editor: markdown
dateCreated: 2023-02-23T21:32:29.919Z
---

- [읽기-쓰기 동시 잠금을 위한 Java의 ReentrantReadWriteLock***Korean** document is available*](/ko/Knowledge-base/Java/java-s-reentrantreadwritelock-for-read-write-concurrent-locking)
{.links-list}


# Java's ReentrantReadWriteLock for Read-Write Concurrent Locking

ReentrantReadWriteLock is a Read-Write lock implementation provided as part of the Java concurrency utilities in JDK 5.0 and onwards. This implementation is designed to be fair, providing equal opportunity for access to both readers and writers.

ReentrantReadWriteLock maintains a pair of locks, one for read-only operations and one for writes. The read lock may be held concurrently by multiple reader threads, so long as there are no write threads waiting to acquire the lock. Similarly, the write lock is exclusive to a single writer thread, but may be acquired by a reader thread if there are no other waiting threads.

Readers are given priority over writers. That is, if a thread attempts to acquire the read lock while a write lock is already held, the thread will be granted the lock as soon as the write lock is released. However, if a thread attempts to acquire the write lock while other threads hold either the read or write lock, that thread will block until all other threads have released their locks.

## Implementation

ReentrantReadWriteLock is implemented as a wrapper around a ReentrantLock, providing the same basic functionality with a few additional features.

To acquire the read lock, a thread calls lockRead() which acquires the lock if it is available, or waits until it is released if it is not.

To acquire the write lock, a thread calls lockWrite() which acquires the lock if it is available, or waits until it is released if it is not.

Both lockRead() and lockWrite() are non-blocking methods, meaning that they will return immediately if the lock is available.

To release the read lock, a thread calls unlockRead(), and to release the write lock, unlockWrite().

## Code Example

Here is a simple example of how to use ReentrantReadWriteLock to protect a shared resource:

```java
import java.util.concurrent.locks.ReentrantReadWriteLock;

public class ReadWriteLockExample {

    private static final ReentrantReadWriteLock lock = new ReentrantReadWriteLock();

    public static void main(String[] args) {
        new Thread(ReadWriteLockExample::read).start();
        new Thread(ReadWriteLockExample::write).start();
    }

    private static void read() {
        lock.readLock().lock();
        try {
            // do something with the shared resource
        } finally {
            lock.readLock().unlock();
        }
    }

    private static void write() {
        lock.writeLock().lock();
        try {
            // do something with the shared resource
        } finally {
            lock.writeLock().unlock();
        }
    }
}
```

In this example, we have a shared resource that can be accessed by both reading and writing threads. To protect the resource, we use a ReentrantReadWriteLock.

The read thread acquires the read lock by calling lockRead(), then releases it by calling unlockRead(). The write thread does the same with the write lock.

## Benefits

ReentrantReadWriteLock provides a number of benefits over other locking mechanisms, such as synchronized keyword and ReentrantLock.

First, ReentrantReadWriteLock allows multiple reader threads to acquire the lock simultaneously, whereas synchronized keyword and ReentrantLock allow only a single thread to acquire the lock at a time. This can lead to significantly increased throughput in applications that perform a high number of read operations.

Second, ReentrantReadWriteLock provides a mechanism for granting priority to reader threads over writer threads. This is accomplished by giving reader threads priority when they attempt to acquire the lock while a write lock is already held.

Third, ReentrantReadWriteLock allows for lock downgrading, which is the process of acquiring a write lock and then releasing it in favor of a read lock. This can be useful in situations where a thread needs to perform a series of read operations followed by a single write operation.

Finally, ReentrantReadWriteLock provides a mechanism for lock upgrading, which is the process of acquiring a read lock and then releasing it in favor of a write lock. This can be useful in situations where a thread needs to perform a series of read operations followed by a single write operation.

## When to Use ReentrantReadWriteLock

ReentrantReadWriteLock is best used in applications that perform a high number of read operations and a relatively small number of write operations. In these applications, ReentrantReadWriteLock will provide increased throughput compared to other locking mechanisms.

ReentrantReadWriteLock is also a good choice in applications where it is important to give priority to reader threads over writer threads.

## When Not to Use ReentrantReadWriteLock

ReentrantReadWriteLock should not be used in applications where the number of write operations is high relative to the number of read operations. In these applications, the increased overhead associated with maintaining two locks will outweigh the benefits of having multiple reader threads.

ReentrantReadWriteLock is also not a good choice in applications where it is not important to give priority to reader threads over writer threads. In these applications, the increased overhead associated with maintaining two locks will outweigh the benefits of having multiple reader threads.

## Alternatives to ReentrantReadWriteLock

There are a number of alternatives to ReentrantReadWriteLock, each with its own benefits and drawbacks.

One alternative is the synchronized keyword. Synchronized keyword is a language construct that can be used to protect a block of code from concurrent access. Synchronized keyword is easier to use than ReentrantReadWriteLock, but it has a number of drawbacks.

First, synchronized keyword does not allow for lock downgrading or lock upgrading. This can lead to deadlock in situations where a thread needs to perform a series of read operations followed by a single write operation.

Second, synchronized keyword does not allow for multiple reader threads to acquire the lock simultaneously. This can lead to decreased throughput in applications that perform a high number of read operations.

Another alternative is ReentrantLock. ReentrantLock is a lock implementation that is part of the Java concurrency utilities. ReentrantLock is more flexible than synchronized keyword, but it has a number of drawbacks.

First, ReentrantLock does not allow for lock downgrading or lock upgrading. This can lead to deadlock in situations where a thread needs to perform a series of read operations followed by a single write operation.

Second, ReentrantLock does not allow for multiple reader threads to acquire the lock simultaneously. This can lead to decreased throughput in applications that perform a high number of read operations.

ReentrantReadWriteLock is a good choice for applications that perform a high number of read operations and a relatively small number of write operations. ReentrantReadWriteLock is also a good choice in applications where it is important to give priority to reader threads over writer threads.