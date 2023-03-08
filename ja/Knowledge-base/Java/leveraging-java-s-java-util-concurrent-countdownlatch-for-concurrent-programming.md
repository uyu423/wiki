---
title: Java の java.util.concurrent.CountDownLatch を並行プログラミングに活用する
description: 
published: true
date: 2023-02-17T18:16:40.606Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:23:27.400Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Leveraging Java's java.util.concurrent.CountDownLatch for Concurrent Programming***English** version of this document is available*](/en/Knowledge-base/Java/leveraging-java-s-java-util-concurrent-countdownlatch-for-concurrent-programming)
{.links-list}


#同時プログラミングのためのJavaのjava.util.concurrent.CountDownLatchの活用

Java 5 リリースとともに、新しい並行性ユーティリティのセットがプラットフォームに追加されました。これらのうちの1つである「java.util.concurrent.CountDownLatch」は、他のスレッドで実行されている一連の操作が完了するまで1つ以上のスレッドが待機できるようにする同期サポートです。この記事では、`CountDownLatch`を使って同時プログラミングで一般的な問題を解決する方法を説明します。

## CountDownLatchとは何ですか？

'CountDownLatch' は正の整数 'count' で初期化されます。 `await`メソッドは`countDown`メソッドの呼び出しによって現在の`count`が0に達するまでブロックされ、その後はすべての待機中のスレッドがブロック解除され続けることができます。

「CountDownLatch」は一度だけ使用できます。リセット可能なバージョンが必要な場合は、 `java.util.concurrent.CyclicBarrier`を参照してください。

## CountDownLatchの作成

`CountDownLatch`を生成することは、カウントダウンするスレッドの数をコンストラクタに渡す簡単な問題です。

```java
int numThreads = 5;
CountDownLatch latch = new CountDownLatch（numThreads）;
```

##カウントダウン

`CountDownLatch`がある場合は、 `countDown`メソッドを呼び出してカウントダウンできます。

```java
latch.countDown();
```

例外が発生しても `countDown`メソッドが常に呼び出されるように `finally`ブロックでこれを行うのが一般的です。

```java
try{
    // do some work
} finally {
    latch.countDown();
}
```

## CountDownLatchを待っています

0までカウントダウンすると、 `await`メソッドを呼び出して他のものを待つことができます。

```java
latch.await();
```

指定された時間待つには、`long`と`TimeUnit`を使用する`await`メソッドを使うことができます。

```java
latch.await(1, TimeUnit.SECONDS);
```

これは、「カウント」が0になるまで最大1秒待ちます。それ以外の場合、`await`は`false`を返します。

## ユースケース

ここで `CountDownLatch` の仕組みを見てみましたが、いくつかの一般的なユースケースを見てみましょう。

### コンポーネントの初期化

使用する前に初期化する必要があるコンポーネントがあるとします。これは `CountDownLatch`で行うことができます。

```java
public class MyComponent {
    private final CountDownLatch latch = new CountDownLatch(1);

    public void init() {
        // do some work
        latch.countDown();
    }

    public void use() {
        try{
            latch.await();
            // do some work
        } catch(InterruptedException e) {
            // handle exception
        }
    }
}
```

この例では、`use`メソッドは`init`が呼び出されるまでブロックされます。

###ジェットコースターに乗る

2台の車があるジェットコースターがあるとしましょう。車は同じなので、並列に動作できます。各車は最大10人の乗客を燃やすことができます。乗客が並列に車に乗ることができるようにしたいのですが、車両がいっぱいになるまで駅を出ることはできません。これは `CountDownLatch`で行うことができます。

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
        try{
            latch.await();
            // do some work
        } catch(InterruptedException e) {
            // handle exception
        }
    }

    // Other methods omitted for brevity
}
```

この例では、`run`メソッドは2つの車がいっぱいになるまでブロックされます。

###複数のイベントを待っています

マルチスレッドプログラムがあり、進む前に複数のイベントが発生するのを待ちたいとします。これは `CountDownLatch`で行うことができます。

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

    try{
        latch.await();
        // do some work
    } catch(InterruptedException e) {
        // handle exception
    }
}
```

この例では、`doWork`は3つのスレッドがすべて完了するまでブロックされます。

##結論

`java.util.concurrent.CountDownLatch`は、同時プログラミングのさまざまな問題を解決するために使用できるシンプルで柔軟な同期支援ツールです。ご質問がございましたら、下記にコメントを残してください。