---
title: Java 对 CompletableFuture 异步处理的支持
description: 
published: true
date: 2023-01-31T05:04:54.191Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:04:50.790Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Java's Support for Asynchronous Processing with CompletableFuture***English** version of this document is available*](/en/Knowledge-base/Java/java-s-support-for-asynchronous-processing-with-completablefuture)
{.links-list}


# Java 对 CompletableFuture 异步处理的支持

Java 长期以来一直对同步处理提供出色的支持，但多年来，它在语言和平台级别上逐渐增加了对异步处理的更好支持。特别是，Java 8 中添加的 CompletableFuture 和 Streams 类使得编写高性能且易于推理的并发代码变得更加容易。在本文中，我们将了解如何使用 CompletableFuture 在 Java 中编写异步代码。

## 创建 CompletableFutures

创建 CompletableFuture 的最基本方法是使用 ```completedFuture()``` static factory method:

```java
CompletableFuture<String> future = CompletableFuture.completedFuture("Hello world!");
```

This future will already be completed with the given value "Hello world!" when it is returned. This is often useful in test code, or when you already have a value that you want to treat as a future result.

In most cases, though, you will want to create a future that is not completed when it is created. The ```supplyAsync()``` and ```runAsync()``` static methods can be used for this:

```java
CompletableFuture<String> 未来 = CompletableFuture.supplyAsync(() -> {
    //做一些计算
    返回“世界，您好！”；
});
```

The ```java
CompletableFuture<Void> 未来 = CompletableFuture.runAsync(() -> {
    //做一些计算
});
```

The ```supplyAsync()``` method takes a ```Supplier<T>``` and returns a ```CompletableFuture<T>``` that will be completed with the result of invoking the supplier when the computation is finished. The ```runAsync()``` method takes a ```Runnable``` and returns a ```CompletableFuture<Void>``` that will be completed with ```null``` when the computation is finished. Note that the ```supplyAsync()``` and ```runAsync()``` methods both use the ForkJoinPool.commonPool() as the Executor to run the given task. This is usually what you want, but if you need to use a different Executor you can pass it as a second argument to either method.

## Consuming the Results of a CompletableFuture

There are two ways to consume the result of a CompletableFuture: synchronously or asynchronously. The ```get()``` method can be used to retrieve the result synchronously:

```java
字符串结果 = future.get();
```

Note that the ```get()``` method can throw a ```CompletionException``` if the future completes with an exception. To retrieve the exception that caused the future to complete with an exception, you can use the ```getCause()``` method:

```java
尝试 {
    字符串结果 = future.get();
} 赶上（CompletionException e）{
    可抛出的原因= e.getCause();
    //处理异常
}
```

The ```get()``` method can also block indefinitely if the future has not yet completed. If you want to set a timeout, you can use the ```get(long timeout, TimeUnit unit)``` method:

```java
尝试 {
    字符串结果 = future.get(1, TimeUnit.SECONDS);
} 赶上（TimeoutException e）{
    //处理超时
}
```

If you want to consume the result of a CompletableFuture asynchronously, you can use the ```thenApply()``` method:

```java
CompletableFuture<String> 未来 = CompletableFuture.supplyAsync(() -> {
    //做一些计算
    返回“世界，您好！”；
});

CompletableFuture<String> greetingFuture = future.thenApply(s -> {
    返回“你好”+ s；
});
```

The ```thenApply()``` method takes a ```Function<T,R>``` and returns a new ```CompletableFuture<R>``` that will be completed with the result of applying the function to the result of the original future when the original future completes. If the original future completes with an exception, the resulting future will also complete with an exception.

You can also use the ```thenAccept()``` method to consume the result of a future asynchronously without returning a new future:

```java
future.thenAccept(s -> {
    //对结果做一些事情
});
```

The ```thenAccept()``` method takes a ```Consumer<T>``` and returns a new ```CompletableFuture<Void>``` that will be completed with ```null``` when the original future completes. If the original future completes with an exception, the resulting future will also complete with an exception.

## Combining CompletableFutures

One of the most powerful features of CompletableFuture is the ability to combine multiple futures into a single future. For example, suppose you have two CompletableFutures, ```future1``` and ```future2```, and you want to create a new future that will be completed with the result of both futures. You can do this with the ```thenCombine()``` method:

```java
CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> {
    //做一些计算
    返回“你好”；
});

CompletableFuture<String> future2 = CompletableFuture.supplyAsync(() -> {
    //做一些计算
    返回“世界！”；
});

CompletableFuture<String> greetingFuture = future1.thenCombine(future2, (s1, s2) -> {
    返回 s1 + s2；
});
```

```thenCombine()``` method takes a CompletableFuture and a BiFunction, and returns a new CompletableFuture that will be completed with the result of the BiFunction when both of the original futures complete. In the example above, the result will be the string "Hello world!"

You can also use the ```thenCompose()``` method to combine two CompletableFutures, but with a slightly different semantics. In particular, the ```thenCompose()``` method takes a Function that itself returns a CompletableFuture, and it returns a new CompletableFuture that is completed with the result of the function when the original future completes:

```java
CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> {
    //做一些计算
    返回“你好”；
});

CompletableFuture<String> future2 = CompletableFuture.supplyAsync(() -> {
    //做一些计算
    返回“世界！”；
});

CompletableFuture<String> greetingFuture = future1.thenCompose(s1 -> {
    返回 future2.thenApply(s2 -> {
        返回 s1 + s2；
    });
});
```

The code above is equivalent to the code in the ```thenCombine()``` example, but it is a bit more verbose.

CompletableFuture also has methods for combining multiple CompletableFutures into a single future. The ```allOf()``` and ```anyOf()``` methods can be used to create a future that is completed when all or any of a collection of futures are completed, respectively:

```java
列表<CompletableFuture<String>> 期货 = ...;

CompletableFuture<Void> future = CompletableFuture.allOf(futures.toArray(new CompletableFuture[futures.size()]));

future.thenAccept(v -> {
    //所有的期货都完成了
});
```

```java
列表<CompletableFuture<String>> 期货 = ...;

CompletableFuture<Object> future = CompletableFuture.anyOf(futures.toArray(new CompletableFuture[futures.size()]));

future.thenAccept(v -> {
    //至少有一个期货已经完成
});
```

## Exception Handling

As we have seen, CompletableFuture has built-in support for handling exceptions. In particular, the ```get()``` and ```get(long, TimeUnit)``` methods can throw a ```CompletionException``` if the future completes with an exception, and the ```getCause()``` method can be used to retrieve the exception that caused the future to complete with an exception.

In addition, the ```thenApply()```, ```thenAccept()```, ```thenRun()```, ```thenCompose()```, and ```thenCombine()``` methods all have versions that take an additional ```Function<Throwable,T>``` argument. This function is invoked if the original future completes with an exception, and it can be used to transform the exception into a value that can be used by the resulting future:

```java
CompletableFuture<String> 未来 = CompletableFuture.supplyAsync(() -> {
    //做一些计算
    抛出新的 RuntimeException（“哎呀！”）;
});

CompletableFuture<String> transformedFuture = future.thenApply(s -> {
    //对结果做一些事情
    返回 s + "!";
}, t -> {
    //处理异常
    返回“错误”；
});

尝试 {
    字符串结果 = transformedFuture.get();
} 赶上（CompletionException e）{
    Assert.assertEquals("错误", e.getCause().getMessage());
}
```

The code above creates a future that will complete with an exception, and then applies a function to the result of the future. The function takes two arguments: the result of the future, and the exception that caused the future to complete with an exception. In this case, the function returns the string "ERROR" if the future completes with an exception.

CompletableFuture also has methods for handling exceptions in a more general way. In particular, the ```exceptionally()``` method can be used to create a new future that is completed with the result of a given function if the original future completes with an exception:

```java
CompletableFuture<String> 未来 = CompletableFuture.supplyAsync(() -> {
    //做一些计算
    抛出新的 RuntimeException（“哎呀！”）;
});

CompletableFuture<String> transformedFuture = future.exceptionally(t -> {
    //处理异常
    返回“错误”；
});

尝试 {
    字符串结果 = transformedFuture.get();
} 赶上（CompletionException e）{
    Assert.assertEquals("错误", e.getCause().getMessage());
}
```

The code above is equivalent to the code in the ```thenApply()``` example, but it is more concise.

## Cancelling Futures

Futures can be cancelled using the ```cancel()``` method. This will cause the future to complete with a ```CancellationException```. Note that this does not guarantee that the computation underlying the future will be cancelled; it only means that the future will not complete successfully.

## Timeouts

As we saw in the ```get()``` section, the ```get(long, TimeUnit)``` method can be used to set a timeout for a future. If the future does not complete within the given timeframe, the ```get()``` method will throw a ```TimeoutException```.

In addition, the ```orTimeout()``` method can be used to create a new future that will complete with the given value if the original future does not complete within the given timeframe:

```java
CompletableFuture<String> 未来 = CompletableFuture.supplyAsync(() -> {
    //做一些计算
    线程.睡眠(1000);
    返回“世界，您好！”；
});

CompletableFuture<String> timeoutFuture = future.orTimeout(500, TimeUnit.MILLISECONDS);

尝试 {
    字符串结果 = timeoutFuture.get();
} 赶上（TimeoutException e）{
    //处理超时
}
```

The code above creates a future that will take at least 1000 milliseconds to complete. The ```orTimeout()``` 方法用于创建一个新的未来，如果原始未来没有在给定的时间范围内完成（在这种情况下，500 毫秒）。

## 概括

在本文中，我们了解了如何使用 CompletableFuture 在 Java 中编写异步代码。 CompletableFuture 使编写高性能且易于推理的并发代码变得容易。