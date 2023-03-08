---
title: 利用 Java 的 java.util.concurrent.ForkJoinPool 进行递归任务处理
description: 
published: true
date: 2023-02-04T21:17:23.914Z
tags: 
editor: markdown
dateCreated: 2023-02-04T21:17:22.307Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Leveraging Java's java.util.concurrent.ForkJoinPool for Recursive Task Processing***English** document is available*](/en/Knowledge-base/Java/leveraging-java-s-java-util-concurrent-forkjoinpool-for-recursive-task-processing)
{.links-list}


# 利用 Java 的 java.util.concurrent.ForkJoinPool 进行递归任务处理

Java 的 ForkJoinPool 是用于递归任务处理的强大工具，与单线程相比，它可以更有效地执行任务。在本文中，我们将了解如何使用 ForkJoinPool 递归处理任务，重点是如何正确管理线程安全。

## 什么是 ForkJoinPool？

ForkJoinPool 是一个专门执行 ForkJoinTasks 的 Java ExecutorService。 ForkJoinTask 是一个任务，可以分成更小的子任务，可以并发执行。 ForkJoinPool 将自动在可用线程之间分配任务，并且还将自动重用已用于其他任务的线程。

## 为什么要使用 ForkJoinPool？

ForkJoinPool 与传统的 ExecutorService 相比有很多优势。首先，它旨在利用多个处理器（如果可用）。其次，它使用工作窃取在线程之间分配任务。这意味着如果一个线程空闲，它可以从另一个繁忙的线程中窃取工作。这可以导致更有效地使用线程，并且通常可以导致更短的整体执行时间。

## 如何使用 ForkJoinPool

使用 ForkJoinPool 相对简单。首先，创建一个 ForkJoinPool：

```java
ForkJoinPool pool = new ForkJoinPool();
```

接下来，创建一个 ForkJoinTask。有两种类型的 ForkJoinTasks：RecursiveAction 和 RecursiveTask。 RecursiveAction 用于不返回结果的任务，而 RecursiveTask 用于返回结果的任务。在此示例中，我们将使用 RecursiveTask：

```java
RecursiveTask<Integer> task = new RecursiveTask<Integer>() {
    protected Integer compute() {
        // TODO: compute something
    }
};
```

请注意，compute() 方法是完成任务工作的地方。您可以在此处放置将任务划分为更小的子任务的代码，然后执行这些子任务。

创建任务后，可以将其提交给 ForkJoinPool 执行：

```java
pool.submit(task);
```

submit() 方法将返回一个 Future 对象，该对象可用于检查任务的状态，或获取任务的结果（如果它是 RecursiveTask）。

## 线程安全

使用 ForkJoinPool 时，重要的是要意识到潜在的线程安全问题。这是因为 ForkJoinTask 可以由多个线程同时执行。因此，由 ForkJoinTask 执行的任何代码都必须正确同步。

有几种方法可以实现正确的同步。最直接的方法是使用 Java synchronized 关键字。例如，如果您有一个正在被 ForkJoinTask 访问的共享数据结构，您可以使用 synchronized 关键字来确保一次只有一个线程可以访问该数据结构：

```java
synchronized(data) {
    // TODO: access data
}
```

实现正确同步的另一种方法是使用 Java 的 Atomic 类。这些类提供了许多可用于安全访问共享数据的原子操作。例如，AtomicInteger 类提供了原子自增操作：

```java
AtomicInteger i = new AtomicInteger();
// TODO: increment i
i.incrementAndGet();
```

Atomic 类的用途远不止增加一个值。它们还可以用于添加两个值或比较和交换等操作。有关 Atomic 类的更多信息，请参阅 Java 文档。

## 结论

ForkJoinPool 是递归任务处理的强大工具，与单线程相比，任务执行效率更高。使用 ForkJoinPool 时，重要的是要了解潜在的线程安全问题，并采取措施确保您的代码正确同步。