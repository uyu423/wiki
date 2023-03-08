---
title: Java の java.util.concurrent.locks.LockSupport を使用してスレッドをブロックする
description: 
published: true
date: 2023-01-31T13:04:28.573Z
tags: 
editor: markdown
dateCreated: 2023-01-31T13:04:25.077Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Working with Java's java.util.concurrent.locks.LockSupport for Thread Blocking***English** version of this document is available*](/en/Knowledge-base/Java/working-with-java-s-java-util-concurrent-locks-locksupport-for-thread-blocking)
{.links-list}



スレッドブロック
===============

Javaでのスレッドのブロックは、スレッドが他のリソースを待っているために作業を続行できない場合です。これは、スレッドが他のスレッドがタスクを完了するのを待つ場合や、スレッドがリソースを使用できるようにするのを待つ場合など、いくつかの理由で発生する可能性があります。

どちらの場合も、スレッドがブロックされたと言われています。スレッドがブロックされると、どのコードも実行できなくなり、ブロックが削除されるまで事実上中断されます。

Javaでスレッドブロックを処理する方法はいくつかあります。一般的なアプローチの1つは、java.util.concurrent.locks.LockSupportクラスを使用することです。

LockSupportは、ロックとブロックを処理するためのいくつかの静的メソッドを提供するユーティリティクラスです。これは、同時アプリケーション開発をサポートするように設計された一連のクラスであるJava並行性ユーティリティの一部です。

LockSupportの最も一般的な用途は、他のスレッドが操作を完了するまでスレッドをブロックすることです。これは、 park() および unpark() メソッドを使用して行うことができます。

park() メソッドは、同じスレッドで unpark() メソッドが呼び出されるまで、現在のスレッドをブロックします。 unpark() メソッドはすべてのスレッドで呼び出すことができますが、スレッドが現在駐車されている場合にのみ効果があります。

スレッドが現在パーキングされていない場合、unpark（）は何もしません。

以下は、他のスレッドがタスクを完了するまでスレッドをブロックするためにpark（）とunpark（）を使用する方法の簡単な例です。

```java
public static void main(String[] args) {
    Thread worker = new Thread(() -> {
        // do some work
        System.out.println("Worker is done.");

        // call unpark to unblock the main スレッド
        LockSupport.unpark(Thread.currentThread());
    }）;

    worker.start();

    System.out.println("Main thread is waiting for worker to finish.");

    // call park to block the main thread until unpark is called
    LockSupport.park();

    System.out.println("Main thread is done.");
}
```

この例では、メインスレッドはpark（）を呼び出して自分自身をブロックします。ワーカースレッドはいくつかの操作を実行し、unpark（）を呼び出してメインスレッドのブロックを解除します。

メインスレッドがブロック解除されたら、実行を続け、「メインスレッドが完了しました」と印刷します。

LockSupportは、ロックとブロックを処理するためのさまざまな方法も提供します。これにはtryLock（）、isParked（）、およびparkNanos（）が含まれます。

tryLock() は park() に似ていますが、現在のスレッドをブロックしません。代わりにロックを取得し、すぐに返します。ロックが利用できない場合、tryLock() は false を返します。

isParked() スレッドが現在ブロックされていることを確認するために使用できます。スレッドがブロックされている場合はtrueを返し、スレッドがブロックされていない場合はfalseを返します。

parkNanos() は park() と似ていますが、指定された時間だけ現在のスレッドをブロックします。時間はナノ秒単位で指定されます。

 LockSupport はスレッドのブロックを処理するのに便利なツールです。スレッドをブロックしてブロック解除し、ロックを試み、取得するために使用できるいくつかの静的メソッドを提供します。