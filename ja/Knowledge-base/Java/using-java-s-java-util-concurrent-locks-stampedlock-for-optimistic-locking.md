---
title: Java の java.util.concurrent.locks.StampedLock を楽観的ロックに使用する
description: 
published: true
date: 2023-02-01T07:17:42.167Z
tags: 
editor: markdown
dateCreated: 2023-02-01T07:17:40.595Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Using Java's java.util.concurrent.locks.StampedLock for Optimistic Locking***English** version of this document is available*](/en/Knowledge-base/Java/using-java-s-java-util-concurrent-locks-stampedlock-for-optimistic-locking)
{.links-list}



#楽観的ロックにJavaでjava.util.concurrent.locks.StampedLockを使用する

楽観的ロックは、データが複数のスレッドによって同時に変更されないようにする戦略です。ロックのオーバーヘッドを避けながらデータ破損に対する保護を提供するために、同時プログラミングで広く使用されている技術です。

Javaのjava.util.concurrent.locks.StampedLockは楽観的ロックのためのメカニズムを提供します。この記事では、Javaで楽観的ロックを達成するためにStampedLockクラスを使用する方法について説明します。

##楽観的なロックとは何ですか？

楽観的ロックは、データが複数のスレッドによって同時に変更されないようにする戦略です。ロックのオーバーヘッドを避けながらデータ破損に対する保護を提供するために、同時プログラミングで広く使用されている技術です。

楽観的ロックを使用する場合、各スレッドは最初にデータを読み取ります。データが他のスレッドによって変更されていない場合、スレッドはデータを安全に更新できます。データが別のスレッドによって変更された場合、更新は中断され、データが再ロードされます。

## StampedLockはどのように機能しますか？

StampedLockは、3つのロックモード（楽観的、読み取り、書き込み）を持つ再入口ロックです。

楽観モードはデフォルトモードです。楽観モードでは、スレッドはブロックせずにロックをロックできます。ロックが別のスレッドによってすでにロックされている場合、ロックの試行は失敗します。

読み取りモードでは、複数のスレッドが読み取りのためにロックをロックできます。書き込みのためにロックがすでにロックされている場合、ロックの試行は失敗します。

書き込みモードでは、1つのスレッドだけが書き込みのためにロックをロックできます。読み取りまたは書き込みのためにロックがすでにロックされている場合、ロックの試行は失敗します。

## StampedLockを使う

以下は、同時修正からデータを保護するためにStampedLockを使用する簡単な例です。

```java
import java.util.concurrent.locks.StampedLock;

public class OptimisticLocking {

    private static final StampedLock lock = new StampedLock();
    private static int data = 0;

    public static void main(String[] args) {
        // スレッド 1 tries to read data
        long stamp = lock.tryOptimisticRead();
        int localData = data;
        if(!lock.validate(stamp)) {
            // data has been modified, need to acquire read lock
            stamp = lock.readLock();
            try{
                localData = data;
            } finally {
                lock.unlockRead（stamp）;
            }
        }
        // data has not been modified, can use localData safely

        // スレッド 2 tries to update data
        long stamp = lock.writeLock();
        try{
            data = localData + 1;
        } finally {
            lock.unlockWrite（stamp）;
        }
    }
}
```

上記の例では、スレッド 1 はデータの読み取りを試みます。データが他のスレッドによって変更されていない場合、読み取りは成功し、スレッド1はデータを安全に使用できます。データが別のスレッドによって変更された場合、読み取りは失敗し、スレッド1がデータを読み取るには読み取りロックを取得する必要があります。

スレッド２はデータの更新を試みる。データが他のスレッドによって変更されていない場合、更新は成功します。データが別のスレッドによって変更された場合、更新は失敗し、スレッド2はデータを更新するために書き込みロックを取得する必要があります。

## StampedLockを使用している場合

StampedLockは、Javaで楽観的ロックを達成するのに便利なツールです。楽観的ロックを使用する場合は、パフォーマンスと精度のバランスを考慮することが重要です。

楽観的ロックは、ロックオーバーヘッドを回避することでパフォーマンスを向上させることができます。ただし、データ破損のリスクが高くなります。データが同時スレッドによって頻繁に変更される場合、楽観的ロックが最善の戦略ではない可能性があります。

##結論

この記事では、楽観的ロックを達成するためにJavaのjava.util.concurrent.locks.StampedLockを使用する方法について説明しました。我々は、楽観的なロックを使用するときに考慮すべき長所と短所も見ました。