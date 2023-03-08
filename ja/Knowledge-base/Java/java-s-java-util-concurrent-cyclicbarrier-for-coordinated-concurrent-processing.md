---
title: 調整された同時処理のための Java の java.util.concurrent.CyclicBarrier
description: 
published: true
date: 2023-01-31T14:23:36.765Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:23:35.213Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Java's java.util.concurrent.CyclicBarrier for Coordinated Concurrent Processing***English** version of this document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-cyclicbarrier-for-coordinated-concurrent-processing)
{.links-list}


 CyclicBarrierは、一連のスレッドが互いに共通のバリアポイントに到達するのを待つことを可能にする同期サポートです。cyclicBarrier.await（）;

CyclicBarrierは、ジョブを調整する必要がある固定数のジョブを開始するプログラムで役立ちます。待機中のスレッドが解放された後に再利用できるため、バリアは循環と呼ばれます。

CyclicBarrierの一般的な使用例は、問題をN個の独立した部分に分割し、並列に解決し、結果を組み合わせることです。たとえば、CyclicBarrierを使用して画像をNxNタイルに分割し、これらのタイルを並列に処理し、処理されたタイルを結合して最終画像を作成できます。

以下は、CyclicBarrierを使用して問題を4つの部分に分割し、並列に解決し、結果を組み合わせる簡単な例です。

```java
import java.util.concurrent.BrokenBarrierException;
import java.util.concurrent.CyclicBarrier;

public class CyclicBarrierExample {

    public static void main(String[] args) {

        //Create a CyclicBarrier with four parties
        CyclicBarrier barrier = new CyclicBarrier(4, new Runnable() {
            @Override
            public void run() {
                // This task will be executed once all parties will reach the barrier
                System.out.println("All parties have arrived at the barrier, lets move on...");
            }
        }）;

        // Create four separate threads, each executing a task
        Thread t1 = new Thread(new Task(barrier));
        Thread t2 = new Thread(new Task(barrier));
        Thread t3 = new Thread(new Task(barrier));
        Thread t4 = new Thread(new Task(barrier));

        // Start the four threads
        t1.start();
        t2.start();
        t3.start();
        t4.start();

    }

    // A task that takes some time to complete
    static class Task implements Runnable {

        private CyclicBarrier barrier;

        public Task(CyclicBarrier barrier) {
            this.barrier = barrier;
        }

        @Override
        public void run() {
            try{
                System.out.println("Thread " + Thread.currentThread().getId() + " is doing its work...");
                Thread.sleep(1000); // simulated task
                System.out.println("Thread " + Thread.currentThread().getId() + " has finished its work");
                barrier.await(); // waiting for all parties to arrive
            } catch(InterruptedException e) {
                // ...
            } catch(BrokenBarrierException e) {
                // ...
            }
        }
    }
}
```

上記の例では、ジョブを実行してから他のすべてのスレッドが障壁に到達するのを待つ4つのスレッドがあります。すべてのスレッドが到着すると、バリアが開き、待機しているスレッドが解放されます。

CyclicBarrierは、最初のスレッドが障壁に達したときにアクションをトリガーするためにも使用できます。たとえば、システム状態を変更する一連のスレッドを開始する前に、システム状態のスナップショットを撮るのに役立ちます。

```java
import java.util.concurrent.BrokenBarrierException;
import java.util.concurrent.CyclicBarrier;

public class CyclicBarrierExample {

    public static void main(String[] args) {

        //Create a CyclicBarrier with four parties and a barrier action
        CyclicBarrier barrier = new CyclicBarrier(4, new Runnable() {
            @Override
            public void run() {
                // This task will be executed once all parties will reach the barrier
                System.out.println("All parties have arrived at the barrier, lets move on...");
            }
        }）;

        // Create four separate threads, each executing a task
        Thread t1 = new Thread(new Task(barrier));
        Thread t2 = new Thread(new Task(barrier));
        Thread t3 = new Thread(new Task(barrier));
        Thread t4 = new Thread(new Task(barrier));

        // Start the four threads
        t1.start();
        t2.start();
        t3.start();
        t4.start();

    }

    // A task that takes some time to complete
    static class Task implements Runnable {

        private CyclicBarrier barrier;

        public Task(CyclicBarrier barrier) {
            this.barrier = barrier;
        }

        @Override
        public void run() {
            try{
                System.out.println("Thread " + Thread.currentThread().getId() + " is doing its work...");
                Thread.sleep(1000); // simulated task
                System.out.println("Thread " + Thread.currentThread().getId() + " has finished its work");
                barrier.await(); // waiting for all parties to arrive
            } catch(InterruptedException e) {
                // ...
            } catch(BrokenBarrierException e) {
                // ...
            }
        }
    }
}
```

上記の例では、ジョブを実行してから、他のすべてのスレッドが障壁に到達するのを待つ4つのスレッドがあります。すべてのスレッドが到着すると、バリアが開き、待機しているスレッドが解放されます。

CyclicBarrierは、最初のスレッドが障壁に達したときにアクションをトリガーするためにも使用できます。たとえば、システム状態を変更する一連のスレッドを開始する前に、システム状態のスナップショットを撮るのに役立ちます。