---
title: Java's java.util.concurrent.locks.ReentrantLock for Reentrant Locking
description: 
published: true
date: 2023-02-12T02:55:31.909Z
tags: 
editor: markdown
dateCreated: 2023-02-12T02:55:25.087Z
---

- [java.util.concurrent.locks.ReentrantLock de Java para bloqueo reentrante***Spanish** document is available*](/es/Knowledge-base/Java/java-s-java-util-concurrent-locks-reentrantlock-for-reentrant-locking)
{.links-list}
- [Java 的 java.util.concurrent.locks.ReentrantLock 用于可重入锁定***Chinese Simplified** document is available*](/zh/Knowledge-base/Java/java-s-java-util-concurrent-locks-reentrantlock-for-reentrant-locking)
{.links-list}
- [재진입 잠금을 위한 Java의 java.util.concurrent.locks.ReentrantLock***Korean** document is available*](/ko/Knowledge-base/Java/java-s-java-util-concurrent-locks-reentrantlock-for-reentrant-locking)
{.links-list}


# Java's java.util.concurrent.locks.ReentrantLock for Reentrant Locking

Reentrant locking is a popular mechanism for ensuring thread safety in Java applications. In this article, we'll take a close look at how ReentrantLock works in Java.

ReentrantLock is a part of the Java concurrency utilities and implements the Lock interface. It provides a more sophisticated locking mechanism than the intrinsic locks available in Java.

ReentrantLock fairness policy

There are two types of fairness policy for ReentrantLock:

* Fair
* Non-fair

The fair policy prevents threads from starving while waiting for the lock. In a fair ReentrantLock, when multiple threads are waiting for the lock, the thread that has been waiting the longest is given the lock first.

The non-fair policy is the default policy and gives no guarantee about the order in which threads acquire the lock. This policy is more efficient than the fair policy.

How ReentrantLock works

ReentrantLock uses an internal lock object to represent the locked state. When a thread invokes the lock() method, it acquires the lock if it's available. If the lock is not available, the thread goes into a waiting state.

When a thread acquires a lock, it gets a hold count. The thread can release the lock by invoking the unlock() method. The lock is released only when the thread's hold count becomes zero.

If a thread tries to acquire a lock that it already holds, the thread's hold count is incremented.

A thread can release a lock that it doesn't hold by invoking the unlock() method. This results in an IllegalMonitorStateException.

The tryLock() method

The tryLock() method is used to acquire a lock. If the lock is available, the thread acquires the lock and the method returns true. If the lock is not available, the thread doesn't block and the method returns false.

The tryLock(long time, TimeUnit unit) method is used to acquire a lock within a specified time. If the lock is available, the thread acquires the lock and the method returns true. If the lock is not available, the thread is blocked until the specified time expires. If the time expires before the lock is available, the thread doesn't acquire the lock and the method returns false.

The lockInterruptibly() method

The lockInterruptibly() method is used to acquire a lock. If the lock is available, the thread acquires the lock. If the lock is not available, the thread is blocked until the lock becomes available or the thread is interrupted.

The newCondition() method

The newCondition() method creates a new Condition object that is bound to this Lock instance.

The isHeldByCurrentThread() method

The isHeldByCurrentThread() method returns true if the current thread holds this lock and false otherwise.

The isLocked() method

The isLocked() method returns true if this lock is held by any thread and false otherwise.

The getQueueLength() method

The getQueueLength() method returns the number of threads waiting to acquire this lock.

The hasQueuedThreads() method

The hasQueuedThreads() method returns true if there are threads waiting to acquire this lock and false otherwise.

The isFair() method

The isFair() method returns true if this lock is fair and false otherwise.

The getHoldCount() method

The getHoldCount() method returns the number of locks held by the current thread.

The toString() method

The toString() method returns a string representation of this lock.