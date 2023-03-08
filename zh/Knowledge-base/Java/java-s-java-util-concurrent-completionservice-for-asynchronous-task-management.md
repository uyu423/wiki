---
title: Java 用于异步任务管理的 java.util.concurrent.CompletionService
description: 
published: true
date: 2023-02-03T22:55:16.447Z
tags: 
editor: markdown
dateCreated: 2023-02-03T22:55:11.466Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Java's java.util.concurrent.CompletionService for Asynchronous Task Management***English** document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-completionservice-for-asynchronous-task-management)
{.links-list}


# Java 的 java.util.concurrent.CompletionService 用于异步任务管理

Java 的 java.util.concurrent.CompletionService 是管理异步任务的强大工具。它允许您提交任务并跟踪其进度，在任务完成时接收通知，甚至在必要时取消任务。

下面是一个简单示例，说明如何使用“CompletionService”提交任务并跟踪其进度：

```java
// Create a CompletionService
CompletionService<String> service = new ExecutorCompletionService<>(executor);

// Submit a task
Future<String> future = service.submit(new Callable<String>() {
    @Override
    public String call() throws Exception {
        // Do some work
        return "Result";
    }
});

// Track the task's progress
while (!future.isDone()) {
    // Do something else
}

// Get the task's result
String result = future.get();
```

如您所见，`CompletionService` 可以轻松提交和跟踪异步任务的进度。它还提供了在任务完成时接收通知以及在必要时取消任务的便捷方法。

外部资源：

- [CompletionService 的 JavaDoc](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CompletionService.html)
- [Java 并发教程：CompletionService](https://www.baeldung.com/java-completion-service)
- [Java 技巧 67：使用 Java CompletionService](https://www.javaworld.com/article/2077322/java-tip-67--use-the-java-completion-service.html)