---
title: A Guide to Java's java.util.concurrent.Exchanger for Concurrent Data Exchange
description: 
published: true
date: 2023-02-04T06:55:27.279Z
tags: 
editor: markdown
dateCreated: 2023-02-04T06:55:21.842Z
---

- [Una guía para java.util.concurrent.Exchanger de Java para el intercambio de datos concurrente***Spanish** document is available*](/es/Knowledge-base/Java/a-guide-to-java-s-java-util-concurrent-exchanger-for-concurrent-data-exchange)
{.links-list}
- [用于并发数据交换的 Java java.util.concurrent.Exchanger 指南***Chinese Simplified** document is available*](/zh/Knowledge-base/Java/a-guide-to-java-s-java-util-concurrent-exchanger-for-concurrent-data-exchange)
{.links-list}
- [동시 데이터 교환을 위한 Java의 java.util.concurrent.Exchanger 가이드***Korean** document is available*](/ko/Knowledge-base/Java/a-guide-to-java-s-java-util-concurrent-exchanger-for-concurrent-data-exchange)
{.links-list}


# A Guide to Java's java.util.concurrent.Exchanger for Concurrent Data Exchange

In concurrent programming, data exchange between threads is a common operation. The Exchanger class in Java's Concurrent API provides a mechanism for threads to exchange data in a safe and convenient way.

This article will give an overview of the Exchanger class and demonstrate how it can be used in a concurrent program.

## What is the Exchanger Class?

The Exchanger class is a utility class for exchanging data between threads. It provides a single method, exchange(), which takes two arguments: the data to be exchanged, and a timeout value.

If there is another thread waiting to exchange data, the exchange() method will return immediately with the data from the other thread. If there is no other thread waiting, the exchange() method will block until another thread calls exchange() with the same data.

The Exchanger class is useful for situations where two threads need to synchronize their data, such as in a producer-consumer relationship.

## Using the Exchanger Class

Here is a simple example of how the Exchanger class can be used. In this example, two threads are used to exchange data. The first thread generates a random number, and the second thread calculates the square of that number.

```java
import java.util.concurrent.Exchanger;

public class ExchangerExample {
    public static void main(String[] args) {
        Exchanger<Integer> exchanger = new Exchanger<>();
        
        new Thread(() -> {
            try {
                int data = (int) (Math.random() * 100);
                System.out.println("Thread 1: " + data);
                
                data = exchanger.exchange(data);
                
                System.out.println("Thread 1: " + data);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();
        
        new Thread(() -> {
            try {
                int data = (int) (Math.random() * 100);
                System.out.println("Thread 2: " + data);
                
                data = exchanger.exchange(data);
                
                System.out.println("Thread 2: " + data);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();
    }
}
```

In this example, the two threads exchange data and then print the results. The output of this program might look something like this:

```
Thread 1: 97
Thread 2: 25
Thread 1: 625
Thread 2: 676
```

## Conclusion

The Exchanger class provides a mechanism for threads to exchange data in a safe and convenient way. It is useful for situations where two threads need to synchronize their data.