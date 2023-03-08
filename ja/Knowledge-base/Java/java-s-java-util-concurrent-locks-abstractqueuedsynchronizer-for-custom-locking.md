---
title: カスタム ロック用の Java の java.util.concurrent.locks.AbstractQueuedSynchronizer
description: 
published: true
date: 2023-01-31T16:43:58.589Z
tags: 
editor: markdown
dateCreated: 2023-01-31T16:43:56.956Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Java's java.util.concurrent.locks.AbstractQueuedSynchronizer for Custom Locking***English** version of this document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-locks-abstractqueuedsynchronizer-for-custom-locking)
{.links-list}


#カスタムロックのためのJavaのjava.util.concurrent.locks.AbstractQueuedSynchronizer

Javaの`java.util.concurrent.locks.AbstractQueuedSynchronizer`（AQS）は、カスタムロックを構築するための強力なツールです。この記事では、AQSを使用して簡単なロックを作成する方法について説明します。また、AQSを使用して公正で再入可能なロックを実装するために使用できる、より複雑なロックを作成する方法を見てみましょう。

## AQSで簡単なロックを作成する

AQSを使って簡単なロックを作成する方法を見てみましょう。最初にすべきことは、 `AbstractQueuedSynchronizer`を拡張するクラスを作成することです。このクラスはロック機能の実装を担当します。

```java
public class MyLock extends AbstractQueuedSynchronizer {

}
```

次に、ロックを取得および解放するために使用するメソッドを追加する必要があります。 'acquire'メソッドはロックを取得するために使用され、 'release'メソッドはロックを解放するために使用されます。 `MyLock`クラスで`acquire`と`release`メソッドをオーバーライドすることでこれらのメソッドを追加できます。

```java
@Override
protected boolean tryAcquire(int arg) {
    // TODO: implement tryAcquire
}

@Override
protected boolean tryRelease(int arg) {
    // TODO: implement tryRelease
}
```

`tryAcquire`メソッドはロック取得を担当します。 `tryRelease`メソッドはロック解除を担当します。

## tryAcquire メソッドの実装

'tryAcquire'メソッドはロックの取得を担当します。 `MyLock`クラスで`acquireQueued`メソッドを呼び出すことで`tryAcquire`メソッドを実装できます。 'acquireQueued'メソッドはロックを取得しようとし、ロックが取得されると 'true'を返します。それ以外の場合は「false」を返します。

```java
@Override
protected boolean tryAcquire(int arg) {
    return acquireQueued（new Node（）、arg）;
}
```

## tryRelease メソッドの実装

`tryRelease`メソッドはロック解除を担当します。 `MyLock`クラスで`release`メソッドを呼び出すことで`tryRelease`メソッドを実装できます。 `release`メソッドはロックを解除し、ロックが解除されると `true`を返します。それ以外の場合は「false」を返します。

```java
@Override
protected boolean tryRelease(int arg) {
    return release（arg）;
}
```

## ロックを使う

ここで `MyLock` クラスを実装したので、それを使う方法を見てみましょう。まず、`MyLock`クラスのインスタンスを作成する必要があります。

```java
MyLock lock = new MyLock();
```

次に、`lock`メソッドを呼び出してロックを取得できます。

```java
lock.lock();
```

ロックを獲得すると、ロックを維持しながら実行する必要がある作業を実行できます。完了したら、 `unlock`メソッドを呼び出してロックを解除できます。

```java
lock.unlock();
```

## AQSで公正なリエントラントロックを作成する

AQSを使用して簡単なロックを作成する方法を見てみましたが、より複雑なロックを作成する方法を見てみましょう。このセクションでは、AQSを使用して公正で再入可能なロックを実装します。

公正な再入ロックは、公正で同じスレッドで複数回獲得できるロックです。スレッドがロックを取得する順序で保護するリソースへのアクセスを許可する場合、ロックは公平です。スレッドが複数のロックを獲得できる場合、ロックは再入可能です。

AQSを使用して公正で再入可能なロックを作成する方法を見てみましょう。最初にすべきことは、 `AbstractQueuedSynchronizer`を拡張するクラスを作成することです。このクラスはロック機能の実装を担当します。

```java
public class MyLock extends AbstractQueuedSynchronizer {

}
```

次に、ロックを取得および解放するために使用するメソッドを追加する必要があります。 'acquire'メソッドはロックを取得するために使用され、 'release'メソッドはロックを解放するために使用されます。 `MyLock`クラスで`acquire`と`release`メソッドをオーバーライドすることでこれらのメソッドを追加できます。

```java
@Override
protected boolean tryAcquire(int arg) {
    // TODO: implement tryAcquire
}

@Override
protected boolean tryRelease(int arg) {
    // TODO: implement tryRelease
}
```

`tryAcquire`メソッドはロック取得を担当します。 `tryRelease`メソッドはロック解除を担当します。

## tryAcquire メソッドの実装

'tryAcquire'メソッドはロックの取得を担当します。 `MyLock`クラスで`acquireQueued`メソッドを呼び出すことで`tryAcquire`メソッドを実装できます。 'acquireQueued'メソッドはロックを取得しようとし、ロックが取得されると 'true'を返します。それ以外の場合は「false」を返します。

```java
@Override
protected boolean tryAcquire(int arg) {
    return acquireQueued（new Node（）、arg）;
}
```

## tryRelease メソッドの実装

`tryRelease`メソッドはロック解除を担当します。 `MyLock`クラスで`release`メソッドを呼び出すことで`tryRelease`メソッドを実装できます。 `release`メソッドはロックを解除し、ロックが解除されると `true`を返します。それ以外の場合は「false」を返します。

```java
@Override
protected boolean tryRelease(int arg) {
    return release（arg）;
}
```

## ロックを使う

ここで `MyLock` クラスを実装したので、それを使う方法を見てみましょう。まず、`MyLock`クラスのインスタンスを作成する必要があります。

```java
MyLock lock = new MyLock();
```

次に、`lock`メソッドを呼び出してロックを取得できます。

```java
lock.lock();
```

ロックを獲得すると、ロックを維持しながら実行する必要がある作業を実行できます。完了したら、 `unlock`メソッドを呼び出してロックを解除できます。

```java
lock.unlock();
```

##結論

この記事では、Javaの `java.util.concurrent.locks.AbstractQueuedSynchronizer`を使って簡単なロックと公正で再入可能なロックを作成する方法を見ました。ロックを取得して解放するために `acquire`と `release`メソッドを使用する方法を見てみました。また、`lock`と`unlock`メソッドを使ってロックを取得して解放する方法も見ました。