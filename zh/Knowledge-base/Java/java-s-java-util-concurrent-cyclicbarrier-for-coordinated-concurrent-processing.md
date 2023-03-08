---
title: 用于协调并发处理的 Java java.util.concurrent.CyclicBarrier
description: 
published: true
date: 2023-01-31T14:23:36.858Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:23:35.218Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Java's java.util.concurrent.CyclicBarrier for Coordinated Concurrent Processing***English** version of this document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-cyclicbarrier-for-coordinated-concurrent-processing)
{.links-list}


 CyclicBarrier 是一种同步辅助工具，它允许一组线程全部等待彼此到达一个共同的障碍点。cyclicBarrier.await();

CyclicBarrier 在启动固定数量的任务且必须协调它们的操作的程序中很有用。屏障之所以称为循环屏障，是因为它可以在等待线程被释放后重新使用。

CyclicBarrier 的一个常见用例是将一个问题分成 N 个独立的部分，并行解决它们，然后组合结果。例如，您可以使用 CyclicBarrier 将图像分成 NxN 个图块，并行处理这些图块，然后组合处理后的图块以创建最终图像。

下面是一个简单的示例，它使用 CyclicBarrier 将问题分为四个部分，并行解决它们，然后合并结果：

```java
import java.util.concurrent.BrokenBarrierException;
import java.util.concurrent.CyclicBarrier;

public class CyclicBarrierExample {

    public static void main(String[] args) {

        // Create a CyclicBarrier with four parties
        CyclicBarrier barrier = new CyclicBarrier(4, new Runnable() {
            @Override
            public void run() {
                // This task will be executed once all parties will reach the barrier
                System.out.println("All parties have arrived at the barrier, lets move on...");
            }
        });

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
            try {
                System.out.println("Thread " + Thread.currentThread().getId() + " is doing its work...");
                Thread.sleep(1000); // simulated task
                System.out.println("Thread " + Thread.currentThread().getId() + " has finished its work");
                barrier.await(); // waiting for all parties to arrive
            } catch (InterruptedException e) {
                // ...
            } catch (BrokenBarrierException e) {
                // ...
            }
        }
    }
}
```

在上面的例子中，我们有四个线程执行一个任务，然后等待所有其他线程到达屏障。一旦所有线程都到达，屏障就会打开并释放等待的线程。

CyclicBarrier 也可用于在第一个线程到达屏障时触发操作。这可能很有用，例如，在启动一组修改系统状态的线程之前获取系统状态的快照。

```java
import java.util.concurrent.BrokenBarrierException;
import java.util.concurrent.CyclicBarrier;

public class CyclicBarrierExample {

    public static void main(String[] args) {

        // Create a CyclicBarrier with four parties and a barrier action
        CyclicBarrier barrier = new CyclicBarrier(4, new Runnable() {
            @Override
            public void run() {
                // This task will be executed once all parties will reach the barrier
                System.out.println("All parties have arrived at the barrier, lets move on...");
            }
        });

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
            try {
                System.out.println("Thread " + Thread.currentThread().getId() + " is doing its work...");
                Thread.sleep(1000); // simulated task
                System.out.println("Thread " + Thread.currentThread().getId() + " has finished its work");
                barrier.await(); // waiting for all parties to arrive
            } catch (InterruptedException e) {
                // ...
            } catch (BrokenBarrierException e) {
                // ...
            }
        }
    }
}
```

在上面的例子中，我们有四个线程执行一个任务，然后等待所有其他线程到达屏障。一旦所有线程都到达，屏障就会打开并释放等待的线程。

CyclicBarrier 也可用于在第一个线程到达屏障时触发操作。这可能很有用，例如，在启动一组修改系统状态的线程之前获取系统状态的快照。