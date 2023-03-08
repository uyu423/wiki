---
title: 조정된 동시 처리를 위한 Java의 java.util.concurrent.CyclicBarrier
description: 
published: true
date: 2023-01-31T14:23:36.766Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:23:35.210Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Java's java.util.concurrent.CyclicBarrier for Coordinated Concurrent Processing***English** version of this document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-cyclicbarrier-for-coordinated-concurrent-processing)
{.links-list}


 CyclicBarrier는 일련의 스레드가 서로가 공통 장벽 지점에 도달하기를 기다릴 수 있도록 하는 동기화 지원입니다.cyclicBarrier.await();

CyclicBarrier는 작업을 조정해야 하는 고정된 수의 작업을 시작하는 프로그램에서 유용합니다. 대기 중인 스레드가 해제된 후 재사용할 수 있기 때문에 장벽을 순환이라고 합니다.

CyclicBarrier의 일반적인 사용 사례는 문제를 N개의 독립적인 부분으로 나누고 병렬로 해결한 다음 결과를 결합하는 것입니다. 예를 들어 CyclicBarrier를 사용하여 이미지를 NxN 타일로 나누고 이러한 타일을 병렬로 처리한 다음 처리된 타일을 결합하여 최종 이미지를 만들 수 있습니다.

다음은 CyclicBarrier를 사용하여 문제를 네 부분으로 나누고 병렬로 해결한 다음 결과를 결합하는 간단한 예입니다.

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

위의 예에서 작업을 실행한 다음 다른 모든 스레드가 장벽에 도착할 때까지 기다리는 4개의 스레드가 있습니다. 모든 스레드가 도착하면 장벽이 열리고 대기 중인 스레드가 해제됩니다.

CyclicBarrier는 첫 번째 스레드가 장벽에 도달할 때 작업을 트리거하는 데 사용할 수도 있습니다. 예를 들어 시스템 상태를 수정하는 스레드 집합을 시작하기 전에 시스템 상태의 스냅샷을 찍는 데 유용할 수 있습니다.

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

위의 예에서 작업을 실행한 다음 다른 모든 스레드가 장벽에 도착할 때까지 기다리는 4개의 스레드가 있습니다. 모든 스레드가 도착하면 장벽이 열리고 대기 중인 스레드가 해제됩니다.

CyclicBarrier는 첫 번째 스레드가 장벽에 도달할 때 작업을 트리거하는 데 사용할 수도 있습니다. 예를 들어 시스템 상태를 수정하는 스레드 집합을 시작하기 전에 시스템 상태의 스냅샷을 찍는 데 유용할 수 있습니다.