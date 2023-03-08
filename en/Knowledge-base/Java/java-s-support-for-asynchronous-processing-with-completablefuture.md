---
title: Java's Support for Asynchronous Processing with CompletableFuture
description: 
published: true
date: 2023-01-31T05:04:52.553Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:04:50.781Z
---

- [CompletableFuture를 사용한 비동기 처리에 대한 Java의 지원***Korean** version of this document is available*](/ko/Knowledge-base/Java/java-s-support-for-asynchronous-processing-with-completablefuture)
{.links-list}
- [CompletableFuture による Java の非同期処理のサポート***Japanese** version of this document is available*](/ja/Knowledge-base/Java/java-s-support-for-asynchronous-processing-with-completablefuture)
{.links-list}
- [Java 对 CompletableFuture 异步处理的支持***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Java/java-s-support-for-asynchronous-processing-with-completablefuture)
{.links-list}


# Java's Support for Asynchronous Processing with CompletableFuture

Java has long had excellent support for synchronous processing, but over the years it has added progressively better support for asynchronous processing on both the language and platform level. In particular, the additions of the CompletableFuture  and Streams  classes in Java 8 have made it much easier to write concurrent code that is both performant and easy to reason about. In this article, we will take a look at how CompletableFuture can be used to write asynchronous code in Java.

## Creating CompletableFutures

The most basic way to create a CompletableFuture is to use the ```completedFuture()``` static factory method:

```java
CompletableFuture<String> future = CompletableFuture.completedFuture("Hello world!");
```

This future will already be completed with the given value "Hello world!" when it is returned. This is often useful in test code, or when you already have a value that you want to treat as a future result.

In most cases, though, you will want to create a future that is not completed when it is created. The ```supplyAsync()``` and ```runAsync()``` static methods can be used for this:

```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
    //Do some computation
    return "Hello world!";
});
```

```java
CompletableFuture<Void> future = CompletableFuture.runAsync(() -> {
    //Do some computation
});
```

The ```supplyAsync()``` method takes a ```Supplier<T>``` and returns a ```CompletableFuture<T>``` that will be completed with the result of invoking the supplier when the computation is finished. The ```runAsync()``` method takes a ```Runnable``` and returns a ```CompletableFuture<Void>``` that will be completed with ```null``` when the computation is finished. Note that the ```supplyAsync()``` and ```runAsync()``` methods both use the ForkJoinPool.commonPool() as the Executor to run the given task. This is usually what you want, but if you need to use a different Executor you can pass it as a second argument to either method.

## Consuming the Results of a CompletableFuture

There are two ways to consume the result of a CompletableFuture: synchronously or asynchronously. The ```get()``` method can be used to retrieve the result synchronously:

```java
String result = future.get();
```

Note that the ```get()``` method can throw a ```CompletionException``` if the future completes with an exception. To retrieve the exception that caused the future to complete with an exception, you can use the ```getCause()``` method:

```java
try {
    String result = future.get();
} catch (CompletionException e) {
    Throwable cause = e.getCause();
    //Handle exception
}
```

The ```get()``` method can also block indefinitely if the future has not yet completed. If you want to set a timeout, you can use the ```get(long timeout, TimeUnit unit)``` method:

```java
try {
    String result = future.get(1, TimeUnit.SECONDS);
} catch (TimeoutException e) {
    //Handle timeout
}
```

If you want to consume the result of a CompletableFuture asynchronously, you can use the ```thenApply()``` method:

```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
    //Do some computation
    return "Hello world!";
});

CompletableFuture<String> greetingFuture = future.thenApply(s -> {
    return "Hello " + s;
});
```

The ```thenApply()``` method takes a ```Function<T,R>``` and returns a new ```CompletableFuture<R>``` that will be completed with the result of applying the function to the result of the original future when the original future completes. If the original future completes with an exception, the resulting future will also complete with an exception.

You can also use the ```thenAccept()``` method to consume the result of a future asynchronously without returning a new future:

```java
future.thenAccept(s -> {
    //Do something with the result
});
```

The ```thenAccept()``` method takes a ```Consumer<T>``` and returns a new ```CompletableFuture<Void>``` that will be completed with ```null``` when the original future completes. If the original future completes with an exception, the resulting future will also complete with an exception.

## Combining CompletableFutures

One of the most powerful features of CompletableFuture is the ability to combine multiple futures into a single future. For example, suppose you have two CompletableFutures, ```future1``` and ```future2```, and you want to create a new future that will be completed with the result of both futures. You can do this with the ```thenCombine()``` method:

```java
CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> {
    //Do some computation
    return "Hello";
});

CompletableFuture<String> future2 = CompletableFuture.supplyAsync(() -> {
    //Do some computation
    return " world!";
});

CompletableFuture<String> greetingFuture = future1.thenCombine(future2, (s1, s2) -> {
    return s1 + s2;
});
```

The ```thenCombine()``` method takes a CompletableFuture and a BiFunction, and returns a new CompletableFuture that will be completed with the result of the BiFunction when both of the original futures complete. In the example above, the result will be the string "Hello world!"

You can also use the ```thenCompose()``` method to combine two CompletableFutures, but with a slightly different semantics. In particular, the ```thenCompose()``` method takes a Function that itself returns a CompletableFuture, and it returns a new CompletableFuture that is completed with the result of the function when the original future completes:

```java
CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> {
    //Do some computation
    return "Hello";
});

CompletableFuture<String> future2 = CompletableFuture.supplyAsync(() -> {
    //Do some computation
    return " world!";
});

CompletableFuture<String> greetingFuture = future1.thenCompose(s1 -> {
    return future2.thenApply(s2 -> {
        return s1 + s2;
    });
});
```

The code above is equivalent to the code in the ```thenCombine()``` example, but it is a bit more verbose.

CompletableFuture also has methods for combining multiple CompletableFutures into a single future. The ```allOf()``` and ```anyOf()``` methods can be used to create a future that is completed when all or any of a collection of futures are completed, respectively:

```java
List<CompletableFuture<String>> futures = ...;

CompletableFuture<Void> future = CompletableFuture.allOf(futures.toArray(new CompletableFuture[futures.size()]));

future.thenAccept(v -> {
    //All of the futures have completed
});
```

```java
List<CompletableFuture<String>> futures = ...;

CompletableFuture<Object> future = CompletableFuture.anyOf(futures.toArray(new CompletableFuture[futures.size()]));

future.thenAccept(v -> {
    //At least one of the futures have completed
});
```

## Exception Handling

As we have seen, CompletableFuture has built-in support for handling exceptions. In particular, the ```get()``` and ```get(long, TimeUnit)``` methods can throw a ```CompletionException``` if the future completes with an exception, and the ```getCause()``` method can be used to retrieve the exception that caused the future to complete with an exception.

In addition, the ```thenApply()```, ```thenAccept()```, ```thenRun()```, ```thenCompose()```, and ```thenCombine()``` methods all have versions that take an additional ```Function<Throwable,T>``` argument. This function is invoked if the original future completes with an exception, and it can be used to transform the exception into a value that can be used by the resulting future:

```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
    //Do some computation
    throw new RuntimeException("Oops!");
});

CompletableFuture<String> transformedFuture = future.thenApply(s -> {
    //Do something with the result
    return s + "!";
}, t -> {
    //Handle exception
    return "ERROR";
});

try {
    String result = transformedFuture.get();
} catch (CompletionException e) {
    Assert.assertEquals("ERROR", e.getCause().getMessage());
}
```

The code above creates a future that will complete with an exception, and then applies a function to the result of the future. The function takes two arguments: the result of the future, and the exception that caused the future to complete with an exception. In this case, the function returns the string "ERROR" if the future completes with an exception.

CompletableFuture also has methods for handling exceptions in a more general way. In particular, the ```exceptionally()``` method can be used to create a new future that is completed with the result of a given function if the original future completes with an exception:

```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
    //Do some computation
    throw new RuntimeException("Oops!");
});

CompletableFuture<String> transformedFuture = future.exceptionally(t -> {
    //Handle exception
    return "ERROR";
});

try {
    String result = transformedFuture.get();
} catch (CompletionException e) {
    Assert.assertEquals("ERROR", e.getCause().getMessage());
}
```

The code above is equivalent to the code in the ```thenApply()``` example, but it is more concise.

## Cancelling Futures

Futures can be cancelled using the ```cancel()``` method. This will cause the future to complete with a ```CancellationException```. Note that this does not guarantee that the computation underlying the future will be cancelled; it only means that the future will not complete successfully.

## Timeouts

As we saw in the ```get()``` section, the ```get(long, TimeUnit)``` method can be used to set a timeout for a future. If the future does not complete within the given timeframe, the ```get()``` method will throw a ```TimeoutException```.

In addition, the ```orTimeout()``` method can be used to create a new future that will complete with the given value if the original future does not complete within the given timeframe:

```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
    //Do some computation
    Thread.sleep(1000);
    return "Hello world!";
});

CompletableFuture<String> timeoutFuture = future.orTimeout(500, TimeUnit.MILLISECONDS);

try {
    String result = timeoutFuture.get();
} catch (TimeoutException e) {
    //Handle timeout
}
```

The code above creates a future that will take at least 1000 milliseconds to complete. The ```orTimeout()``` method is used to create a new future that will complete with the given value (in this case, ```null```) if the original future does not complete within the given timeframe (in this case, 500 milliseconds).

## Summary

In this article, we have looked at how CompletableFuture can be used to write asynchronous code in Java. CompletableFuture makes it easy to write concurrent code that is both performant and easy to reason about.