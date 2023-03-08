---
title: Java's java.util.concurrent.CyclicBarrier for Coordinated Concurrent Processing
description: 
published: true
date: 2023-01-31T14:23:38.721Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:23:35.211Z
---

- [조정된 동시 처리를 위한 Java의 java.util.concurrent.CyclicBarrier***Korean** version of this document is available*](/ko/Knowledge-base/Java/java-s-java-util-concurrent-cyclicbarrier-for-coordinated-concurrent-processing)
{.links-list}
- [調整された同時処理のための Java の java.util.concurrent.CyclicBarrier***Japanese** version of this document is available*](/ja/Knowledge-base/Java/java-s-java-util-concurrent-cyclicbarrier-for-coordinated-concurrent-processing)
{.links-list}
- [用于协调并发处理的 Java java.util.concurrent.CyclicBarrier***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Java/java-s-java-util-concurrent-cyclicbarrier-for-coordinated-concurrent-processing)
{.links-list}


 CyclicBarrier is a synchronization aid that allows a set of threads to all wait for each other to reach a common barrier point.cyclicBarrier.await();

A CyclicBarrier is useful in programs that launch a fixed number of tasks that must coordinate their actions. The barrier is called cyclic because it can be reused after the waiting threads are released.

A common use case for a CyclicBarrier is to divide a problem into N independent parts, solve them in parallel, and then combine the results. For example, you can use a CyclicBarrier to divide an image into NxN tiles, process those tiles in parallel, and then combine the processed tiles to create the final image.

Here's a simple example that uses a CyclicBarrier to divide a problem into four parts, solve them in parallel, and then combine the results:

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

In the example above, we have four threads that execute a task and then wait for all other threads to arrive at the barrier. Once all threads have arrived, the barrier is opened and the waiting threads are released.

The CyclicBarrier can also be used to trigger a action when the first thread arrives at the barrier. This can be useful, for example, to take a snapshot of the state of the system before starting a set of threads that modify the state of the system.

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

In the example above, we have four threads that execute a task and then wait for all other threads to arrive at the barrier. Once all threads have arrived, the barrier is opened and the waiting threads are released.

The CyclicBarrier can also be used to trigger a action when the first thread arrives at the barrier. This can be useful, for example, to take a snapshot of the state of the system before starting a set of threads that modify the state of the system.