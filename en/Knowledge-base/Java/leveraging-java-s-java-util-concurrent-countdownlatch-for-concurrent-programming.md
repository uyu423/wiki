---
title: Leveraging Java's java.util.concurrent.CountDownLatch for Concurrent Programming
description: 
published: true
date: 2023-02-17T18:16:37.875Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:23:27.398Z
---

- [동시 프로그래밍을 위한 Java의 java.util.concurrent.CountDownLatch 활용***Korean** version of this document is available*](/ko/Knowledge-base/Java/leveraging-java-s-java-util-concurrent-countdownlatch-for-concurrent-programming)
{.links-list}
- [Java の java.util.concurrent.CountDownLatch を並行プログラミングに活用する***Japanese** version of this document is available*](/ja/Knowledge-base/Java/leveraging-java-s-java-util-concurrent-countdownlatch-for-concurrent-programming)
{.links-list}
- [利用 Java 的 java.util.concurrent.CountDownLatch 进行并发编程***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Java/leveraging-java-s-java-util-concurrent-countdownlatch-for-concurrent-programming)
{.links-list}


# Leveraging Java's java.util.concurrent.CountDownLatch for Concurrent Programming

With the release of Java 5, a new set of concurrency utilities was added to the platform. One of these, `java.util.concurrent.CountDownLatch`, is a synchronization aid that allows one or more threads to wait until a set of operations being performed in other threads completes. This article will show how to use `CountDownLatch` to solve common problems in concurrent programming.

## What is a CountDownLatch?

A `CountDownLatch` is initialized with a positive integer `count`. The `await` methods block until the current `count` reaches zero due to invocations of the `countDown` method, after which all waiting threads are unblocked and able to continue. 

A `CountDownLatch` can only be used once. If you need a resettable version, see `java.util.concurrent.CyclicBarrier`.

## Creating a CountDownLatch

Creating a `CountDownLatch` is a simple matter of passing the number of threads that will be counting down to the constructor:

```java
int numThreads = 5;
CountDownLatch latch = new CountDownLatch(numThreads);
```

## Counting Down

Once you have a `CountDownLatch`, you can count down by calling the `countDown` method:

```java
latch.countDown();
```

It is common to do this in a `finally` block to ensure that the `countDown` method is always called, even if an exception is thrown:

```java
try {
    // do some work
} finally {
    latch.countDown();
}
```

## Waiting for the CountDownLatch

Once you have counted down to zero, you can call the `await` method to wait for the others:

```java
latch.await();
```

If you want to wait for a specified amount of time, you can use the `await` method that takes a `long` and a `TimeUnit`:

```java
latch.await(1, TimeUnit.SECONDS);
```

This will wait for up to one second for the `count` to reach zero. If it does not, then `await` will return `false`.

## Use Cases

Now that we've seen how `CountDownLatch` works, let's look at some common use cases.

### Initializing a Component

Suppose you have a component that needs to be initialized before it can be used. This can be done with a `CountDownLatch`:

```java
public class MyComponent {
    private final CountDownLatch latch = new CountDownLatch(1);

    public void init() {
        // do some work
        latch.countDown();
    }

    public void use() {
        try {
            latch.await();
            // do some work
        } catch (InterruptedException e) {
            // handle exception
        }
    }
}
```

In this example, the `use` method will block until `init` has been called.

### Riding the Roller Coaster

Suppose you have a roller coaster with two cars. The cars are identical, so they can be operated in parallel. Each car can carry up to 10 passengers. You want passengers to be able to board the cars in parallel, but the cars cannot leave the station until they are both full. This can be accomplished with a `CountDownLatch`:

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
        try {
            latch.await();
            // do some work
        } catch (InterruptedException e) {
            // handle exception
        }
    }

    // Other methods omitted for brevity
}
```

In this example, the `run` method will block until both cars are full.

### Waiting for Multiple Events

Suppose you have a multi-threaded program and you want to wait for multiple events to occur before proceeding. This can be accomplished with a `CountDownLatch`:

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

    try {
        latch.await();
        // do some work
    } catch (InterruptedException e) {
        // handle exception
    }
}
```

In this example, `doWork` will block until all three threads have finished.

## Conclusion

`java.util.concurrent.CountDownLatch` is a simple and flexible synchronization aid that can be used to solve a variety of problems in concurrent programming. If you have any questions, please feel free to leave a comment below.