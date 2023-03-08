---
title: 利用 Java 的 java.util.concurrent.CountDownLatch 进行并发编程
description: 
published: true
date: 2023-02-17T18:16:41.941Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:23:27.406Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Leveraging Java's java.util.concurrent.CountDownLatch for Concurrent Programming***English** version of this document is available*](/en/Knowledge-base/Java/leveraging-java-s-java-util-concurrent-countdownlatch-for-concurrent-programming)
{.links-list}


# 利用 Java 的 java.util.concurrent.CountDownLatch 进行并发编程

随着 Java 5 的发布，平台中添加了一组新的并发实用程序。其中之一，“java.util.concurrent.CountDownLatch”，是一种同步辅助工具，它允许一个或多个线程等待，直到其他线程中执行的一组操作完成。本文将展示如何使用 CountDownLatch 解决并发编程中的常见问题。

## 什么是 CountDownLatch？

`CountDownLatch` 使用正整数 `count` 进行初始化。 `await` 方法会阻塞，直到当前的 `count` 由于调用 `countDown` 方法而达到零，之后所有等待的线程都将解除阻塞并能够继续。

`CountDownLatch` 只能使用一次。如果您需要可重置版本，请参阅 java.util.concurrent.CyclicBarrier。

## 创建一个 CountDownLatch

创建一个 CountDownLatch 很简单，只需将要倒计时的线程数传递给构造函数即可：

```java
int numThreads = 5;
CountDownLatch latch = new CountDownLatch(numThreads);
```

##倒计时

一旦有了 CountDownLatch，就可以通过调用 countDown 方法进行倒计时：

```java
latch.countDown();
```

通常在 finally 块中执行此操作以确保始终调用 countDown 方法，即使抛出异常也是如此：

```java
try {
    // do some work
} finally {
    latch.countDown();
}
```

## 等待 CountDownLatch

倒数到零后，您可以调用 `await` 方法等待其他人：

```java
latch.await();
```

如果你想等待指定的时间量，你可以使用带有 `long` 和 `TimeUnit` 的 `await` 方法：

```java
latch.await(1, TimeUnit.SECONDS);
```

这将等待最多一秒钟，以便“计数”达到零。如果没有，则 `await` 将返回 `false`。

## 用例

现在我们已经了解了 CountDownLatch 的工作原理，让我们来看看一些常见的用例。

### 初始化组件

假设您有一个组件需要先初始化才能使用。这可以通过 `CountDownLatch` 来完成：

```java
public class MyComponent {
    private final CountDownLatch latch = new CountDownLatch(1);

    public void init() {
        // do some work
        latch.countDown();
    }

    public void use() {
        try {
            latch.await();
            // do some work
        } catch (InterruptedException e) {
            // handle exception
        }
    }
}
```

在此示例中，“use”方法将阻塞，直到调用“init”。

### 坐过山车

假设你有一辆有两辆车的过山车。汽车是相同的，因此它们可以并行运行。每节车厢最多可搭载 10 名乘客。您希望乘客能够同时登上两节车厢，但两节车厢必须满员才能离开车站。这可以通过 `CountDownLatch` 来完成：

```java
public class RollerCoaster {
    private final CountDownLatch latch = new CountDownLatch(2);

    public void boardPassenger(Passenger p) {
        // do some work
        if (isFull()) {
            latch.countDown();
        }
    }

    public void run() {
        try {
            latch.await();
            // do some work
        } catch (InterruptedException e) {
            // handle exception
        }
    }

    // Other methods omitted for brevity
}
```

在此示例中，“run”方法将阻塞，直到两辆车都装满为止。

### 等待多个事件

假设您有一个多线程程序，您希望在继续之前等待多个事件发生。这可以通过 `CountDownLatch` 来完成：

```java
public void doWork() {
    CountDownLatch latch = new CountDownLatch(3);

    // start three threads
    new Thread(new Runnable() {
        public void run() {
            // do some work
            latch.countDown();
        }
    }).start();

    new Thread(new Runnable() {
        public void run() {
            // do some work
            latch.countDown();
        }
    }).start();

    new Thread(new Runnable() {
        public void run() {
            // do some work
            latch.countDown();
        }
    }).start();

    try {
        latch.await();
        // do some work
    } catch (InterruptedException e) {
        // handle exception
    }
}
```

在此示例中，`doWork` 将阻塞，直到所有三个线程都完成为止。

## 结论

`java.util.concurrent.CountDownLatch` 是一种简单灵活的同步辅助工具，可用于解决并发编程中的各种问题。如果您有任何疑问，请随时在下方发表评论。