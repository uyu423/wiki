---
title: Java 的 java.util.concurrent.locks.AbstractQueuedSynchronizer 用于自定义锁定
description: 
published: true
date: 2023-01-31T16:43:58.575Z
tags: 
editor: markdown
dateCreated: 2023-01-31T16:43:56.956Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Java's java.util.concurrent.locks.AbstractQueuedSynchronizer for Custom Locking***English** version of this document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-locks-abstractqueuedsynchronizer-for-custom-locking)
{.links-list}


# Java 的 java.util.concurrent.locks.AbstractQueuedSynchronizer 用于自定义锁定

Java 的“java.util.concurrent.locks.AbstractQueuedSynchronizer”(AQS) 是用于构建自定义锁的强大工具。在本文中，我们将探索如何使用 AQS 创建一个简单的锁。我们还将了解如何使用 AQS 创建一个更复杂的锁，该锁可用于实现公平、可重入的锁。

## 使用 AQS 创建一个简单的锁

让我们先看看如何使用 AQS 创建一个简单的锁。我们需要做的第一件事是创建一个扩展 `AbstractQueuedSynchronizer` 的类。这个类将负责实现我们锁的功能。

```java
public class MyLock extends AbstractQueuedSynchronizer {

}
```

接下来，我们需要添加将用于获取和释放锁的方法。 `acquire` 方法将用于获取锁，`release` 方法将用于释放锁。我们可以通过覆盖 MyLock 类中的 acquire 和 release 方法来添加这些方法。

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

`tryAcquire` 方法将负责获取锁。 `tryRelease` 方法将负责释放锁。

## 实现 tryAcquire 方法

`tryAcquire` 方法负责获取锁。在我们的 MyLock 类中，我们可以通过调用 acquireQueued 方法来实现 tryAcquire 方法。 `acquireQueued` 方法将尝试获取锁并在获取锁时返回 `true`。否则，它将返回“false”。

```java
@Override
protected boolean tryAcquire(int arg) {
    return acquireQueued(new Node(), arg);
}
```

## 实现 tryRelease 方法

`tryRelease` 方法负责释放锁。在我们的 MyLock 类中，我们可以通过调用 release 方法来实现 tryRelease 方法。 `release` 方法将释放锁，如果锁被释放则返回 `true`。否则，它将返回“false”。

```java
@Override
protected boolean tryRelease(int arg) {
    return release(arg);
}
```

## 使用锁

现在我们已经实现了 MyLock 类，让我们来看看如何使用它。首先，我们需要创建 MyLock 类的实例。

```java
MyLock lock = new MyLock();
```

接下来，我们可以通过调用 lock 方法来获取锁。

```java
lock.lock();
```

一旦我们获得了锁，我们就可以在持有锁的同时执行我们需要执行的操作。完成后，我们可以通过调用 unlock 方法来释放锁。

```java
lock.unlock();
```

## 使用 AQS 创建一个公平的可重入锁

现在我们已经了解了如何使用 AQS 创建一个简单的锁，让我们来看看如何创建一个更复杂的锁。在本节中，我们将使用 AQS 实现一个公平的可重入锁。

公平可重入锁是一种公平的锁，可以由同一个线程多次获取。如果锁按照线程获取锁的顺序授予对其保护的资源的访问权限，则该锁是公平的。如果线程可以多次获取锁，则锁是可重入的。

让我们首先看看如何使用 AQS 创建一个公平的可重入锁。我们需要做的第一件事是创建一个扩展 `AbstractQueuedSynchronizer` 的类。这个类将负责实现我们锁的功能。

```java
public class MyLock extends AbstractQueuedSynchronizer {

}
```

接下来，我们需要添加将用于获取和释放锁的方法。 `acquire` 方法将用于获取锁，`release` 方法将用于释放锁。我们可以通过覆盖 MyLock 类中的 acquire 和 release 方法来添加这些方法。

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

`tryAcquire` 方法将负责获取锁。 `tryRelease` 方法将负责释放锁。

## 实现 tryAcquire 方法

`tryAcquire` 方法负责获取锁。在我们的 MyLock 类中，我们可以通过调用 acquireQueued 方法来实现 tryAcquire 方法。 `acquireQueued` 方法将尝试获取锁并在获取锁时返回 `true`。否则，它将返回“false”。

```java
@Override
protected boolean tryAcquire(int arg) {
    return acquireQueued(new Node(), arg);
}
```

## 实现 tryRelease 方法

`tryRelease` 方法负责释放锁。在我们的 MyLock 类中，我们可以通过调用 release 方法来实现 tryRelease 方法。 `release` 方法将释放锁，如果锁被释放则返回 `true`。否则，它将返回“false”。

```java
@Override
protected boolean tryRelease(int arg) {
    return release(arg);
}
```

## 使用锁

现在我们已经实现了 MyLock 类，让我们来看看如何使用它。首先，我们需要创建 MyLock 类的实例。

```java
MyLock lock = new MyLock();
```

接下来，我们可以通过调用 lock 方法来获取锁。

```java
lock.lock();
```

一旦我们获得了锁，我们就可以在持有锁的同时执行我们需要执行的操作。完成后，我们可以通过调用 unlock 方法来释放锁。

```java
lock.unlock();
```

## 结论

在本文中，我们探讨了如何使用 Java 的“java.util.concurrent.locks.AbstractQueuedSynchronizer”来创建一个简单的锁和一个公平的可重入锁。我们已经了解了如何使用 `acquire` 和 `release` 方法来获取和释放锁。我们还了解了如何使用 `lock` 和 `unlock` 方法来获取和释放锁。