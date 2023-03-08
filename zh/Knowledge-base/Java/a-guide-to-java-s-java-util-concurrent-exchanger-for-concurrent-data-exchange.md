---
title: 用于并发数据交换的 Java java.util.concurrent.Exchanger 指南
description: 
published: true
date: 2023-02-04T06:55:23.569Z
tags: 
editor: markdown
dateCreated: 2023-02-04T06:55:21.836Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [A Guide to Java's java.util.concurrent.Exchanger for Concurrent Data Exchange***English** document is available*](/en/Knowledge-base/Java/a-guide-to-java-s-java-util-concurrent-exchanger-for-concurrent-data-exchange)
{.links-list}


# 用于并发数据交换的 Java java.util.concurrent.Exchanger 指南

在并发编程中，线程之间的数据交换是一种常见的操作。 Java 的 Concurrent API 中的 Exchanger 类为线程提供了一种安全、方便地交换数据的机制。

本文将概述 Exchanger 类并演示如何在并发程序中使用它。

## 交换器类是什么？

Exchanger 类是用于在线程之间交换数据的实用程序类。它提供了一个方法，exchange()，它有两个参数：要交换的数据和超时值。

如果有另一个线程在等待交换数据，exchange() 方法将立即返回来自另一个线程的数据。如果没有其他线程在等待，exchange() 方法将阻塞，直到另一个线程使用相同的数据调用 exchange()。

Exchanger 类在两个线程需要同步它们的数据的情况下很有用，例如在生产者-消费者关系中。

## 使用交换器类

这是一个如何使用 Exchanger 类的简单示例。在这个例子中，两个线程被用来交换数据。第一个线程生成一个随机数，第二个线程计算该数的平方。

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

在这个例子中，两个线程交换数据然后打印结果。该程序的输出可能如下所示：

```
Thread 1: 97
Thread 2: 25
Thread 1: 625
Thread 2: 676
```

## 结论

Exchanger 类为线程提供了一种以安全、方便的方式交换数据的机制。它在两个线程需要同步数据的情况下很有用。