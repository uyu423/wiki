---
title: 用于并行编程的 Java java.util.concurrent 包
description: 
published: true
date: 2023-02-01T21:57:42.284Z
tags: 
editor: markdown
dateCreated: 2023-02-01T21:57:40.660Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Java's java.util.concurrent Package for Parallel Programming***English** document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-package-for-parallel-programming)
{.links-list}


# Java 用于并行编程的 java.util.concurrent 包

`java.util.concurrent` 包提供了一组支持多线程编程的类和接口。该软件包使开发人员能够轻松编写利用多处理器的程序。

`java.util.concurrent` 包包含以下项目：

* 执行者
* 期货
*线程池
* 锁
* 原子变量
*并发收藏
*同步器

在本文中，我们将重点介绍如何使用 java.util.concurrent 包来编写并行程序。

## 执行者

`Executor` 是执行提交的 `Runnable` 任务的对象。 `Executor` 接口提供了一种将任务提交与每个任务将如何运行的机制分离的方法，包括排队、调度和执行。

`java.util.concurrent` 包中有许多内置的 `Executor` 实现，例如 `ThreadPoolExecutor` 和 `ScheduledThreadPoolExecutor`。我们还可以创建自己的 Executor 实现。

在下面的示例中，我们创建一个 Runnable 任务并将其提交给 Executor 执行：

```java
Runnable task = () -> {
    // Do something
};

Executor executor = Executors.newSingleThreadExecutor();
executor.execute(task);
```

## 期货

`Future` 表示异步计算的结果。我们可以使用 Future 来检查计算是否完成，并检索计算结果。

在以下示例中，我们使用 Future 来检查任务是否已完成并检索结果：

```java
Future<Integer> future = executor.submit(task);

if (future.isDone()) {
    int result = future.get();
}
```

## 线程池

`ThreadPool` 是可用于执行任务的`Threads` 的集合。 `ThreadPool` 管理池中的 `Threads`，并提供在可用时重用 `Threads` 的机制。

在以下示例中，我们创建了一个包含四个“Threads”的“ThreadPool”：

```java
ExecutorService threadPool = Executors.newFixedThreadPool(4);
```

我们可以将 Runnable 任务提交到 ThreadPool 中执行：

```java
threadPool.submit(task);
```

当我们使用完 `ThreadPool` 后，我们可以关闭它：

```java
threadPool.shutdown();
```

## 锁

`Lock` 是一种用于控制对共享资源的访问的机制。锁可用于实现临界区，临界区是必须以原子方式执行的代码段。

在以下示例中，我们使用 `Lock` 来控制对共享资源的访问：

```java
Lock lock = new ReentrantLock();

lock.lock();
try {
    // Access the shared resource
} finally {
    lock.unlock();
}
```

## 原子变量

`AtomicVariable` 是可以自动更新的变量。 `AtomicVariable` 用于实现临界区。

在下面的示例中，我们使用 `AtomicVariable` 来控制对共享资源的访问：

```java
AtomicInteger counter = new AtomicInteger();

int value = counter.incrementAndGet();
```

## 并发集合

`java.util.concurrent` 包中包含一些并发集合，这些集合是可以被多个线程安全使用的集合。

在下面的示例中，我们使用一个 `ConcurrentHashMap` 以线程安全的方式存储数据：

```java
ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();

map.put("foo", 42);
map.get("foo");
```

## 同步器

`Synchronizer` 是一个协调多个线程动作的对象。 `java.util.concurrent` 包包含许多同步器，例如 `Semaphore` 和 `CountDownLatch`。

在下面的示例中，我们使用 `CountDownLatch` 来等待任务完成：

```java
CountDownLatch latch = new CountDownLatch(1);

executor.submit(() -> {
    try {
        // Do something
        latch.countDown();
    } catch (InterruptedException e) {
        // Handle the exception
    }
});

latch.await();
```

## 结论

在本文中，我们了解了如何使用 java.util.concurrent 包编写并行程序。我们已经了解了如何使用 `Executors`、`Futures`、`ThreadPools`、`Locks`、`AtomicVariables`、`ConcurrentCollections` 和 `Synchronizers`。