---
title: CompletableFuture를 사용한 비동기 처리에 대한 Java의 지원
description: 
published: true
date: 2023-01-31T05:04:54.191Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:04:50.782Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Java's Support for Asynchronous Processing with CompletableFuture***English** version of this document is available*](/en/Knowledge-base/Java/java-s-support-for-asynchronous-processing-with-completablefuture)
{.links-list}


# CompletableFuture를 사용한 비동기 처리에 대한 Java의 지원

Java는 오랫동안 동기식 처리를 훌륭하게 지원해 왔지만 수년에 걸쳐 언어 및 플랫폼 수준 모두에서 비동기식 처리에 대한 지원을 점진적으로 추가했습니다. 특히 Java 8에 CompletableFuture 및 Streams 클래스가 추가되어 성능이 우수하고 추론하기 쉬운 동시 코드를 훨씬 쉽게 작성할 수 있습니다. 이 기사에서는 CompletableFuture를 사용하여 Java에서 비동기 코드를 작성하는 방법을 살펴보겠습니다.

## CompletableFutures 만들기

CompletableFuture를 생성하는 가장 기본적인 방법은 ```completedFuture()``` static factory method:

```자바
CompletableFuture<String> future = CompletableFuture.completedFuture("안녕하세요!");
```

This future will already be completed with the given value "Hello world!" when it is returned. This is often useful in test code, or when you already have a value that you want to treat as a future result.

In most cases, though, you will want to create a future that is not completed when it is created. The ```supplyAsync()``` and ```runAsync()``` static methods can be used for this:

```자바
CompletableFuture<String> 미래 = CompletableFuture.supplyAsync(() -> {
    //계산을 한다
    "Hello world!"를 반환합니다.
});
```

The ```자바
CompletableFuture<Void> 미래 = CompletableFuture.runAsync(() -> {
    //계산을 한다
});
```

The ```supplyAsync()``` method takes a ```Supplier<T>``` and returns a ```CompletableFuture<T>``` that will be completed with the result of invoking the supplier when the computation is finished. The ```runAsync()``` method takes a ```Runnable``` and returns a ```CompletableFuture<Void>``` that will be completed with ```null``` when the computation is finished. Note that the ```supplyAsync()``` and ```runAsync()``` methods both use the ForkJoinPool.commonPool() as the Executor to run the given task. This is usually what you want, but if you need to use a different Executor you can pass it as a second argument to either method.

## Consuming the Results of a CompletableFuture

There are two ways to consume the result of a CompletableFuture: synchronously or asynchronously. The ```get()``` method can be used to retrieve the result synchronously:

```자바
문자열 결과 = future.get();
```

Note that the ```get()``` method can throw a ```CompletionException``` if the future completes with an exception. To retrieve the exception that caused the future to complete with an exception, you can use the ```getCause()``` method:

```자바
노력하다 {
    문자열 결과 = future.get();
} 잡기(CompletionException e) {
    던질 수 있는 원인 = e.getCause();
    //예외 처리
}
```

The ```get()``` method can also block indefinitely if the future has not yet completed. If you want to set a timeout, you can use the ```get(long timeout, TimeUnit unit)``` method:

```자바
노력하다 {
    String result = future.get(1, TimeUnit.SECONDS);
} 잡기(TimeoutException e) {
    //시간 초과 처리
}
```

If you want to consume the result of a CompletableFuture asynchronously, you can use the ```thenApply()``` method:

```자바
CompletableFuture<String> 미래 = CompletableFuture.supplyAsync(() -> {
    //계산을 한다
    "Hello world!"를 반환합니다.
});

CompletableFuture<String> greetingFuture = future.thenApply(s -> {
    "Hello" + s를 반환합니다.
});
```

The ```thenApply()``` method takes a ```Function<T,R>``` and returns a new ```CompletableFuture<R>``` that will be completed with the result of applying the function to the result of the original future when the original future completes. If the original future completes with an exception, the resulting future will also complete with an exception.

You can also use the ```thenAccept()``` method to consume the result of a future asynchronously without returning a new future:

```자바
future.thenAccept(s -> {
    //결과로 무언가를 한다
});
```

The ```thenAccept()``` method takes a ```Consumer<T>``` and returns a new ```CompletableFuture<Void>``` that will be completed with ```null``` when the original future completes. If the original future completes with an exception, the resulting future will also complete with an exception.

## Combining CompletableFutures

One of the most powerful features of CompletableFuture is the ability to combine multiple futures into a single future. For example, suppose you have two CompletableFutures, ```future1``` and ```future2```, and you want to create a new future that will be completed with the result of both futures. You can do this with the ```thenCombine()``` method:

```자바
CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> {
    //계산을 한다
    "안녕하세요"를 반환합니다.
});

CompletableFuture<String> future2 = CompletableFuture.supplyAsync(() -> {
    //계산을 한다
    반환 " 세계!";
});

CompletableFuture<String> greetingFuture = future1.thenCombine(미래2, (s1, s2) -> {
    s1 + s2를 반환합니다.
});
```

```thenCombine()``` method takes a CompletableFuture and a BiFunction, and returns a new CompletableFuture that will be completed with the result of the BiFunction when both of the original futures complete. In the example above, the result will be the string "Hello world!"

You can also use the ```thenCompose()``` method to combine two CompletableFutures, but with a slightly different semantics. In particular, the ```thenCompose()``` method takes a Function that itself returns a CompletableFuture, and it returns a new CompletableFuture that is completed with the result of the function when the original future completes:

```자바
CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> {
    //계산을 한다
    "안녕하세요"를 반환합니다.
});

CompletableFuture<String> future2 = CompletableFuture.supplyAsync(() -> {
    //계산을 한다
    반환 " 세계!";
});

CompletableFuture<String> greetingFuture = future1.thenCompose(s1 -> {
    return future2.thenApply(s2 -> {
        s1 + s2를 반환합니다.
    });
});
```

The code above is equivalent to the code in the ```thenCombine()``` example, but it is a bit more verbose.

CompletableFuture also has methods for combining multiple CompletableFutures into a single future. The ```allOf()``` and ```anyOf()``` methods can be used to create a future that is completed when all or any of a collection of futures are completed, respectively:

```자바
List<CompletableFuture<String>> 미래 = ...;

CompletableFuture<Void> future = CompletableFuture.allOf(futures.toArray(new CompletableFuture[futures.size()]));

future.thenAccept(v -> {
    // 모든 미래가 완료되었습니다.
});
```

```자바
List<CompletableFuture<String>> 미래 = ...;

CompletableFuture<Object> future = CompletableFuture.anyOf(futures.toArray(new CompletableFuture[futures.size()]));

future.thenAccept(v -> {
    //미래 중 하나 이상이 완료되었습니다.
});
```

## Exception Handling

As we have seen, CompletableFuture has built-in support for handling exceptions. In particular, the ```get()``` and ```get(long, TimeUnit)``` methods can throw a ```CompletionException``` if the future completes with an exception, and the ```getCause()``` method can be used to retrieve the exception that caused the future to complete with an exception.

In addition, the ```thenApply()```, ```thenAccept()```, ```thenRun()```, ```thenCompose()```, and ```thenCombine()``` methods all have versions that take an additional ```Function<Throwable,T>``` argument. This function is invoked if the original future completes with an exception, and it can be used to transform the exception into a value that can be used by the resulting future:

```자바
CompletableFuture<String> 미래 = CompletableFuture.supplyAsync(() -> {
    //계산을 한다
    throw new RuntimeException("앗!");
});

CompletableFuture<String> transformFuture = future.thenApply(s -> {
    //결과로 무언가를 한다
    리턴 s + "!";
}, 티 -> {
    //예외 처리
    "오류"를 반환합니다.
});

노력하다 {
    문자열 결과 = transformFuture.get();
} 잡기(CompletionException e) {
    Assert.assertEquals("오류", e.getCause().getMessage());
}
```

The code above creates a future that will complete with an exception, and then applies a function to the result of the future. The function takes two arguments: the result of the future, and the exception that caused the future to complete with an exception. In this case, the function returns the string "ERROR" if the future completes with an exception.

CompletableFuture also has methods for handling exceptions in a more general way. In particular, the ```exceptionally()``` method can be used to create a new future that is completed with the result of a given function if the original future completes with an exception:

```자바
CompletableFuture<String> 미래 = CompletableFuture.supplyAsync(() -> {
    //계산을 한다
    throw new RuntimeException("앗!");
});

CompletableFuture<String> transformFuture = future.exceptionally(t -> {
    //예외 처리
    "오류"를 반환합니다.
});

노력하다 {
    문자열 결과 = transformFuture.get();
} 잡기(CompletionException e) {
    Assert.assertEquals("오류", e.getCause().getMessage());
}
```

The code above is equivalent to the code in the ```thenApply()``` example, but it is more concise.

## Cancelling Futures

Futures can be cancelled using the ```cancel()``` method. This will cause the future to complete with a ```CancellationException```. Note that this does not guarantee that the computation underlying the future will be cancelled; it only means that the future will not complete successfully.

## Timeouts

As we saw in the ```get()``` section, the ```get(long, TimeUnit)``` method can be used to set a timeout for a future. If the future does not complete within the given timeframe, the ```get()``` method will throw a ```TimeoutException```.

In addition, the ```orTimeout()``` method can be used to create a new future that will complete with the given value if the original future does not complete within the given timeframe:

```자바
CompletableFuture<String> 미래 = CompletableFuture.supplyAsync(() -> {
    //계산을 한다
    스레드.수면(1000);
    "Hello world!"를 반환합니다.
});

CompletableFuture<String> timeoutFuture = future.orTimeout(500, TimeUnit.MILLISECONDS);

노력하다 {
    문자열 결과 = timeoutFuture.get();
} 잡기(TimeoutException e) {
    //시간 초과 처리
}
```

The code above creates a future that will take at least 1000 milliseconds to complete. The ```orTimeout()``` 메서드는 원래 미래가 주어진 시간 내에 완료되지 않는 경우 주어진 값(이 경우 ```null```)으로 완료될 새로운 미래를 만드는 데 사용됩니다( 이 경우 500밀리초).

## 요약

이 기사에서는 CompletableFuture를 사용하여 Java에서 비동기 코드를 작성하는 방법을 살펴보았습니다. CompletableFuture를 사용하면 성능이 우수하고 추론하기 쉬운 동시 코드를 쉽게 작성할 수 있습니다.