---
title: 並行フェーズ操作のための Java の java.util.concurrent.Phaser の使用
description: 
published: true
date: 2023-02-17T18:07:01.076Z
tags: 
editor: markdown
dateCreated: 2023-01-30T15:43:33.422Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Working with Java's java.util.concurrent.Phaser for Concurrent Phased Operations***English** version of this document is available*](/en/Knowledge-base/Java/working-with-java-s-java-util-concurrent-phaser-for-concurrent-phased-operations)
{.links-list}


フェイザーとは何ですか？
----------------

Java の Phaser クラスは、一連の連携ジョブスケジューリングをサポートするマルチスレッド同期サポートです。つまり、Phaser を使用して、複数のスレッドで一連のジョブ実行をスケジュールおよび調整できます。

Phaserは、特に同時マルチチーム開発環境での使用に適しています。たとえば、開発者チームと共に大規模なプロジェクトを進めているとします。各開発者は異なるタスクを実行しており、各タスクには異なるタイムラインがあります。すべての開発者のタスクを調整するには、Phaserを使用してタスクをスケジュールできます。

ページャはいつ使うべきですか？
--------------------------

Phaserは、複数のスレッドが作業を共同で実行する必要がある状況で最も一般的に使用されます。たとえば、Phaserを使用してマルチスレッド開発チームのタスクをスケジュールできます。

Phaser は、必ずしも開発に関連していないタスクをスケジュールするために使用できます。たとえば、Phaserを使用して、CPUの複数のコアで一連のジョブ実行をスケジュールできます。

使用法
-----

Phaserを使用する前に、Phaserインスタンスを作成する必要があります。その後、Phaserインスタンスを使用してジョブをスケジュールできます。

Phaserインスタンスを作成するのは簡単です。 Phaserインスタンスを使用するスレッド数を指定するだけです。たとえば、Phaserを使用して4スレッド開発チームのタスクをスケジュールする場合は、スレッド数として4を指定します。

```java
Phaser phaser = new Phaser(4);
```

Phaserインスタンスを作成したら、それを使用してタスクをスケジュールできます。これを行うには、Phaserインスタンスの ```register（） '' method of the Phaser instance。この例では、タスク1のタスクのタスクをスケジュールし、「register（）」のメソッドを follows：

「Java
phaser.register();
```

After calling the ```register() ''` method, the thread will be added to the Phaser instance and will be able to participate in the Phaser's scheduling.

スレッドは、Phaser instanceを持っています。 「arriveAndAwaitAdvance（）」のメソッドは、Phaser and then wait for all of the other threads to arriveを返します。 Once all of the threads have arrived, the Phaser will allow the threads to proceed.

Here is a simple example that shows how to use Phaser to schedule the tasks of a four-threaded development team:

「Java
フェイザーphaser = new Phaser（4）;

for(int i = 0; i < 4; i++) {
    最後のint threadId = i;
    新しいスレッド（（） - > {
        System.out.println("Thread" + threadId + "開始操作");
        phaser.arriveAndAwaitAdvance();
        System.out.println("Thread" + threadId + "ジョブ完了");
    }）。開始（）;
}
```

In the example, we first create a Phaser instance with four threads. We then create four threads and register them with the Phaser instance. Finally, we use the Phaser's ```arriveAndAwaitAdvance() '' ` method to have the threads cooperatively work on the task.

When the example is run, the output will be as follows:

```
スレッド0開始ジョブ
スレッド1の起動操作
スレッド2の起動操作
スレッド3の起動操作
スレッド0完了タスク
スレッド1完了タスク
スレッド2完了タスク
スレッド3完了タスク
```

ご覧のように、Phaserはスレッドがジョブの実行に協力するようにしました。

結論
----------

この記事では、JavaのPhaserクラスを使用してマルチスレッド開発チームのタスクをスケジュールする方法について説明しました。 Phaserは、複数のスレッドの操作を調整するために使用できる強力なツールです。