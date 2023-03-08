---
title: Java's java.util.concurrent.locks.AbstractQueuedSynchronizer for Custom Locking
description: 
published: true
date: 2023-01-31T16:44:00.574Z
tags: 
editor: markdown
dateCreated: 2023-01-31T16:43:56.922Z
---

- [사용자 지정 잠금을 위한 Java의 java.util.concurrent.locks.AbstractQueuedSynchronizer***Korean** version of this document is available*](/ko/Knowledge-base/Java/java-s-java-util-concurrent-locks-abstractqueuedsynchronizer-for-custom-locking)
{.links-list}
- [カスタム ロック用の Java の java.util.concurrent.locks.AbstractQueuedSynchronizer***Japanese** version of this document is available*](/ja/Knowledge-base/Java/java-s-java-util-concurrent-locks-abstractqueuedsynchronizer-for-custom-locking)
{.links-list}
- [Java 的 java.util.concurrent.locks.AbstractQueuedSynchronizer 用于自定义锁定***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Java/java-s-java-util-concurrent-locks-abstractqueuedsynchronizer-for-custom-locking)
{.links-list}


# Java's java.util.concurrent.locks.AbstractQueuedSynchronizer for Custom Locking

Java's `java.util.concurrent.locks.AbstractQueuedSynchronizer` (AQS) is a powerful tool for building custom locks. In this article, we'll explore how to use AQS to create a simple lock. We'll also look at how to use AQS to create a more complex lock that can be used to implement a fair, reentrant lock.

## Creating a Simple Lock with AQS

Let's start by looking at how to create a simple lock using AQS. The first thing we need to do is create a class that extends `AbstractQueuedSynchronizer`. This class will be responsible for implementing the functionality of our lock.

```java
public class MyLock extends AbstractQueuedSynchronizer {

}
```

Next, we need to add the methods that will be used to acquire and release the lock. The `acquire` method will be used to acquire the lock, and the `release` method will be used to release the lock. We can add these methods by overriding the `acquire` and `release` methods in our `MyLock` class.

```java
@Override
protected boolean tryAcquire(int arg) {
    // TODO: implement tryAcquire
}

@Override
protected boolean tryRelease(int arg) {
    // TODO: implement tryRelease
}
```

The `tryAcquire` method will be responsible for acquiring the lock. The `tryRelease` method will be responsible for releasing the lock.

## Implementing the tryAcquire Method

The `tryAcquire` method is responsible for acquiring the lock. In our `MyLock` class, we can implement the `tryAcquire` method by calling the `acquireQueued` method. The `acquireQueued` method will attempt to acquire the lock and will return `true` if the lock is acquired. Otherwise, it will return `false`.

```java
@Override
protected boolean tryAcquire(int arg) {
    return acquireQueued(new Node(), arg);
}
```

## Implementing the tryRelease Method

The `tryRelease` method is responsible for releasing the lock. In our `MyLock` class, we can implement the `tryRelease` method by calling the `release` method. The `release` method will release the lock and will return `true` if the lock is released. Otherwise, it will return `false`.

```java
@Override
protected boolean tryRelease(int arg) {
    return release(arg);
}
```

## Using the Lock

Now that we've implemented the `MyLock` class, let's take a look at how to use it. First, we need to create an instance of the `MyLock` class.

```java
MyLock lock = new MyLock();
```

Next, we can acquire the lock by calling the `lock` method.

```java
lock.lock();
```

Once we have acquired the lock, we can perform the actions that we need to perform while holding the lock. When we are finished, we can release the lock by calling the `unlock` method.

```java
lock.unlock();
```

## Creating a Fair, Reentrant Lock with AQS

Now that we've seen how to create a simple lock with AQS, let's take a look at how to create a more complex lock. In this section, we'll implement a fair, reentrant lock using AQS.

A fair, reentrant lock is a lock that is fair and that can be acquired multiple times by the same thread. A lock is fair if it grants access to the resources that it protects in the order in which the threads acquire the lock. A lock is reentrant if a thread can acquire the lock multiple times.

Let's start by looking at how to create a fair, reentrant lock using AQS. The first thing we need to do is create a class that extends `AbstractQueuedSynchronizer`. This class will be responsible for implementing the functionality of our lock.

```java
public class MyLock extends AbstractQueuedSynchronizer {

}
```

Next, we need to add the methods that will be used to acquire and release the lock. The `acquire` method will be used to acquire the lock, and the `release` method will be used to release the lock. We can add these methods by overriding the `acquire` and `release` methods in our `MyLock` class.

```java
@Override
protected boolean tryAcquire(int arg) {
    // TODO: implement tryAcquire
}

@Override
protected boolean tryRelease(int arg) {
    // TODO: implement tryRelease
}
```

The `tryAcquire` method will be responsible for acquiring the lock. The `tryRelease` method will be responsible for releasing the lock.

## Implementing the tryAcquire Method

The `tryAcquire` method is responsible for acquiring the lock. In our `MyLock` class, we can implement the `tryAcquire` method by calling the `acquireQueued` method. The `acquireQueued` method will attempt to acquire the lock and will return `true` if the lock is acquired. Otherwise, it will return `false`.

```java
@Override
protected boolean tryAcquire(int arg) {
    return acquireQueued(new Node(), arg);
}
```

## Implementing the tryRelease Method

The `tryRelease` method is responsible for releasing the lock. In our `MyLock` class, we can implement the `tryRelease` method by calling the `release` method. The `release` method will release the lock and will return `true` if the lock is released. Otherwise, it will return `false`.

```java
@Override
protected boolean tryRelease(int arg) {
    return release(arg);
}
```

## Using the Lock

Now that we've implemented the `MyLock` class, let's take a look at how to use it. First, we need to create an instance of the `MyLock` class.

```java
MyLock lock = new MyLock();
```

Next, we can acquire the lock by calling the `lock` method.

```java
lock.lock();
```

Once we have acquired the lock, we can perform the actions that we need to perform while holding the lock. When we are finished, we can release the lock by calling the `unlock` method.

```java
lock.unlock();
```

## Conclusion

In this article, we've explored how to use Java's `java.util.concurrent.locks.AbstractQueuedSynchronizer` to create a simple lock and a fair, reentrant lock. We've seen how to use the `acquire` and `release` methods to acquire and release the lock. We've also seen how to use the `lock` and `unlock` methods to acquire and release the lock.