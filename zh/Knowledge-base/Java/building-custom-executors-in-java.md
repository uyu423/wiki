---
title: 在 Java 中构建自定义执行器
description: 
published: true
date: 2023-02-02T23:57:28.250Z
tags: 
editor: markdown
dateCreated: 2023-02-02T23:57:23.577Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Building Custom Executors in Java***English** document is available*](/en/Knowledge-base/Java/building-custom-executors-in-java)
{.links-list}


# 在 Java 中构建自定义执行器

开发人员通常需要创建自定义执行器来并行运行任务。在本文中，我们将探讨如何在 Java 中执行此操作。

## 创建线程池

创建自定义执行器的第一步是创建线程池。这可以使用 ```Executors``` 类来完成：

```java
ExecutorService executor = Executors.newFixedThreadPool(10);
```

这将创建一个包含 10 个线程的线程池。您还可以使用 ```Executors``` 类来创建单线程执行程序：

```java
ExecutorService executor = Executors.newSingleThreadExecutor();
```

## 执行任务

一旦有了执行器，就可以将任务提交给它执行。例如，假设您有一个 ```Runnable``` 任务：

```java
Runnable task = () -> {
    // task logic here
};
```

您可以使用 ```submit()``` 方法将此任务提交给执行者执行：

```java
executor.submit(task);
```

如果你有一个 ```Callable``` 任务，您也可以使用 ```submit()``` 方法提交它：

```java
Callable<T> task = () -> {
    // task logic here
    return result;
};
```

## 终止线程池

完成任务执行后，您将需要关闭线程池。这可以使用 ```shutdown()``` 方法来完成：

```java
executor.shutdown();
```

如果你想立即关闭线程池，你可以使用 ```shutdownNow()``` 方法：

```java
executor.shutdownNow();
```

## 资源

- [Java 执行器和线程池教程](https://www.baeldung.com/java-executors-and-thread-pools)
- [Java 线程池](https://www.geeksforgeeks.org/java-thread-pool/)
- [Java ExecutorService 教程](https://www.journaldev.com/1069/java-executor-service-example-thread-pool-executor)