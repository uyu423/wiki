---
title: Working with Java's java.util.concurrent.locks.LockSupport for Thread Blocking
description: 
published: true
date: 2023-01-31T13:04:26.679Z
tags: 
editor: markdown
dateCreated: 2023-01-31T13:04:25.076Z
---

- [스레드 차단을 위한 Java의 java.util.concurrent.locks.LockSupport 작업***Korean** version of this document is available*](/ko/Knowledge-base/Java/working-with-java-s-java-util-concurrent-locks-locksupport-for-thread-blocking)
{.links-list}
- [Java の java.util.concurrent.locks.LockSupport を使用してスレッドをブロックする***Japanese** version of this document is available*](/ja/Knowledge-base/Java/working-with-java-s-java-util-concurrent-locks-locksupport-for-thread-blocking)
{.links-list}
- [使用 Java 的 java.util.concurrent.locks.LockSupport 进行线程阻塞***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Java/working-with-java-s-java-util-concurrent-locks-locksupport-for-thread-blocking)
{.links-list}



Thread Blocking
===============

In Java, thread blocking is when a thread is unable to proceed with its work because it is waiting for another resource. This can happen for a number of reasons, such as when a thread is waiting for another thread to finish its work, or when a thread is waiting for a resource to become available.

In either case, the thread is said to be blocked. When a thread is blocked, it is unable to run any code and is effectively stalled until the block is removed.

There are a number of ways to deal with thread blocking in Java. One common approach is to use the java.util.concurrent.locks.LockSupport class.

LockSupport is a utility class that provides a number of static methods for dealing with locks and blocking. It is part of the Java Concurrency Utilities, which is a set of classes designed to help with developing concurrent applications.

The most common use of LockSupport is to block a thread until another thread has finished its work. This can be done with the park() and unpark() methods.

The park() method blocks the current thread until the unpark() method is called on the same thread. The unpark() method can be called from any thread, but it only has an effect if the thread is currently parked.

If the thread is not currently parked, then unpark() does nothing.

Here is a simple example of how to use park() and unpark() to block a thread until another thread has finished its work.

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

In this example, the main thread calls park() to block itself. The worker thread does some work and then calls unpark() to unblock the main thread.

Once the main thread is unblocked, it will continue to run and print "Main thread is done."

LockSupport also provides a number of other methods for dealing with locks and blocking. These include tryLock(), isParked(), and parkNanos().

tryLock() is similar to park(), but it does not block the current thread. Instead, it tries to acquire a lock and returns immediately. If the lock is not available, then tryLock() returns false.

isParked() can be used to check if a thread is currently blocked. It returns true if the thread is blocked, or false if the thread is not blocked.

parkNanos() is similar to park(), but it blocks the current thread for a specified amount of time. The time is specified in nanoseconds.

 LockSupport is a useful tool for dealing with thread blocking. It provides a number of static methods that can be used to block and unblock threads, as well as to try and acquire locks.