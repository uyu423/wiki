---
title: CompletableFuture による Java の非同期処理のサポート
description: 
published: true
date: 2023-01-31T05:04:54.191Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:04:50.790Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Java's Support for Asynchronous Processing with CompletableFuture***English** version of this document is available*](/en/Knowledge-base/Java/java-s-support-for-asynchronous-processing-with-completablefuture)
{.links-list}


# CompletableFuture를 사용한 비동기 처리에 대한 Java의 지원

java는오랫동안오랫동안처리를를훌륭하게해해수년걸쳐언어언어및플랫폼수준수준비동기식처리비동기식에대한지원 특히 Java 8 から CompletableFuture まで Streams が実装されています。 이 기사에서는 CompletableFuture は Java で実装されています.

## CompletableFutures 続きを読む

CompletableFuture が実装されている場合は、 ```completedFuture()````static factory method:

```

このフューチャは、与えられた値「Hello world!」ですでに完了しています。返されたとき。これは、多くの場合、テスト コードで、または将来の結果として扱いたい値が既にある場合に役立ちます。

ただし、ほとんどの場合、作成された時点で完了していない未来を作成する必要があります。これには ```

This future will already be completed with the given value "Hello world!" when it is returned. This is often useful in test code, or when you already have a value that you want to treat as a future result.

In most cases, though, you will want to create a future that is not completed when it is created. The ```

「자바」
CompletableFuture<Void> メソッド = CompletableFuture.runAsync(() -> {
    //계산을 한다
});
````and ```runAsync()````static methods can be used for this:

```supplyAsync()```

```get()```

The ```

get() メソッドは、Future が例外で完了した場合に CompletionException をスローする可能性があることに注意してください。 future が例外で完了する原因となった例外を取得するには、````method takes a ```Supplier<T>````and returns a ```CompletableFuture<T>````that will be completed with the result of invoking the supplier when the computation is finished. The ```runAsync()````method takes a ```Runnable````and returns a ```CompletableFuture<Void>````that will be completed with ```null````when the computation is finished. Note that the ```supplyAsync()````and ```runAsync()````methods both use the ForkJoinPool.commonPool() as the Executor to run the given task. This is usually what you want, but if you need to use a different Executor you can pass it as a second argument to either method.

## Consuming the Results of a CompletableFuture

There are two ways to consume the result of a CompletableFuture: synchronously or asynchronously. The ```

get() メソッドは、フューチャーがまだ完了していない場合、無期限にブロックすることもできます。タイムアウトを設定したい場合は、 ````method can be used to retrieve the result synchronously:

```

CompletableFuture の結果を非同期的に消費したい場合は、```

Note that the ```

````method can throw a ```CompletionException````if the future completes with an exception. To retrieve the exception that caused the future to complete with an exception, you can use the ```getCause()````method:

```thenAccept()```

The ```

thenAccept() メソッドは、Consumer<T> を取り、新しい CompletableFuture<Void> を返します。元の未来が完成します。元のフューチャが例外で完了する場合、結果のフューチャも例外で完了します。

## CompletableFuture の組み合わせ

CompletableFuture の最も強力な機能の 1 つは、複数の先物を単一の先物に結合する機能です。たとえば、2 つの CompletableFutures、````method can also block indefinitely if the future has not yet completed. If you want to set a timeout, you can use the ```get(long timeout, TimeUnit unit)````method:

```

```

If you want to consume the result of a CompletableFuture asynchronously, you can use the ```thenCompose()````method:

```

上のコードは ```

The ```allOf()````method takes a ```Function<T,R>````and returns a new ```CompletableFuture<R>````that will be completed with the result of applying the function to the result of the original future when the original future completes. If the original future completes with an exception, the resulting future will also complete with an exception.

You can also use the ```

「자바」
List<CompletableFuture<String>> メソッド = ...;

CompletableFuture<Object> future = CompletableFuture.anyOf(futures.toArray(new CompletableFuture[futures.size()]));

future.thenAccept(v -> {
    //미래 중 하나 이상이 완료되었습니다.
});
````method to consume the result of a future asynchronously without returning a new future:

```get()```

The ```thenApply()````method takes a ```Consumer<T>````and returns a new ```CompletableFuture<Void>````that will be completed with ```null````when the original future completes. If the original future completes with an exception, the resulting future will also complete with an exception.

## Combining CompletableFutures

One of the most powerful features of CompletableFuture is the ability to combine multiple futures into a single future. For example, suppose you have two CompletableFutures, ```

上記のコードは、例外で完了するフューチャを作成し、フューチャの結果に関数を適用します。この関数は 2 つの引数を取ります: フューチャーの結果と、フューチャーが例外で完了する原因となった例外です。この場合、future が例外で完了すると、関数は文字列 "ERROR" を返します。

CompletableFuture には、より一般的な方法で例外を処理するためのメソッドもあります。特に、 ````and ```future2```, and you want to create a new future that will be completed with the result of both futures. You can do this with the ```thenCombine()````method:

```

上のコードは ```

The ```cancel()````method takes a CompletableFuture and a BiFunction, and returns a new CompletableFuture that will be completed with the result of the BiFunction when both of the original futures complete. In the example above, the result will be the string "Hello world!"

You can also use the ```get()````method to combine two CompletableFutures, but with a slightly different semantics. In particular, the ```thenCompose()````method takes a Function that itself returns a CompletableFuture, and it returns a new CompletableFuture that is completed with the result of the function when the original future completes:

```orTimeout()```

The code above is equivalent to the code in the ```

上記のコードは、完了するまでに少なくとも 1000 ミリ秒かかる未来を作成します。 ````ortimeout（）` `````메서드는원래주어진주어진시간시간내완료완료되지경우경우주어진값값경우 ````null` `）으로으로 초)。

## 요약

이 기사에서는 CompletableFuture は Java で実装されています. CompletableFuture は、これを使用して作成されたものであり、新しいバージョンが作成されました。