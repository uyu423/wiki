---
title: 用于受控并发访问的 Java java.util.concurrent.Semaphore
description: 
published: true
date: 2023-02-02T01:23:26.297Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:23:24.776Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Java's java.util.concurrent.Semaphore for Controlled Concurrent Access***English** document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-semaphore-for-controlled-concurrent-access)
{.links-list}


# Java 的 java.util.concurrent.Semaphore 用于受控并发访问

在多线程编程中，通常需要限制在任何给定时间可以访问资源或代码块的线程数。这称为并发控制。

在 Java 中实现并发控制的一种方法是使用 java.util.concurrent.Semaphore 类。

信号量是允许线程进入临界区的标记，临界区是一次只能由一个线程执行的代码块。当线程退出临界区时，它将信号量返回到池中。

信号量可用于控制对任何资源的访问，而不仅仅是代码。例如，信号量可用于控制对打印机或数据库的访问。

## 创建一个信号量

通过指定许可数创建信号量。这是可以同时访问临界区的线程数。例如，要创建一个具有 10 个许可的信号量：

```java
Semaphore semaphore = new Semaphore(10);
```

## 申请许可

线程通过调用 acquire() 方法请求许可。此方法会阻塞线程，直到获得许可为止。例如：

```java
semaphore.acquire();
```

## 发布许可证

当线程退出临界区时，它会调用 release() 方法将许可返回给信号量。例如：

```java
semaphore.release();
```

## 例子

以下示例显示如何使用信号量来控制对打印机的访问。

```java
import java.util.concurrent.Semaphore;

public class Printer {
    private Semaphore semaphore;

    public Printer(int numPermits) {
        semaphore = new Semaphore(numPermits);
    }

    public void print(String document) {
        try {
            semaphore.acquire();
            // print the document
        } catch (InterruptedException e) {
            // handle error
        } finally {
            semaphore.release();
        }
    }
}
```

在此示例中，`print()` 方法在打印文档之前获取许可。如果没有可用的许可，`acquire()` 方法会阻塞线程，直到获得许可为止。打印文档后，“release()”方法将许可返回给信号量。

## 信号量和锁的区别

信号量和锁都是并发控制的机制。但是，它们之间存在一些关键差异。

- 一个信号量可以有多个许可，而一个锁只能有一个。
- 信号量可以由未获取它的线程释放，而锁只能由获取它的线程释放。
- 信号量没有所有权的概念，而锁有。

## 结论

Java 的 java.util.concurrent.Semaphore 类提供了一种并发控制机制。信号量可用于控制对任何资源的访问，而不仅仅是代码。使用信号量时，记住信号量和锁之间的区别很重要。