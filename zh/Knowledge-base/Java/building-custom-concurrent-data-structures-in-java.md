---
title: 在 Java 中构建自定义并发数据结构”
description: 
published: true
date: 2023-02-01T12:37:03.045Z
tags: 
editor: markdown
dateCreated: 2023-02-01T12:37:01.767Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Building Custom Concurrent Data Structures in Java"***English** version of this document is available*](/en/Knowledge-base/Java/building-custom-concurrent-data-structures-in-java)
{.links-list}


# 在 Java 中构建自定义并发数据结构

并发编程是一种编程形式，其中多个线程独立执行但共享公共数据资源。在 Java 中，java.util.concurrent 包使并发编程变得更容易，它包含许多专为并发访问而设计的高级数据结构。但是，有时您可能需要创建自己的自定义并发数据结构。

在本文中，我们将研究如何做到这一点。我们将从了解 Java 并发编程的基础知识开始，包括 java.util.concurrent 包和 java.util.concurrent.locks 包。然后我们将看看如何创建自定义并发堆栈数据结构。最后，我们将研究如何测试并发数据结构。

## Java 并发编程

并发编程是一种编程形式，其中多个线程独立执行但共享公共数据资源。在 Java 中，java.util.concurrent 包使并发编程变得更容易，它包含许多专为并发访问而设计的高级数据结构。

java.util.concurrent 包包含以下数据结构：

* 数组阻塞队列
* 并发HashMap
* CopyOnWriteArrayList
* 倒数锁存器
* 循环屏障
* 延迟队列
*交换器
* 优先阻塞队列
* 信号量
* 同步队列

这些数据结构可用于创建各种不同的并发程序。例如，您可以使用 ArrayBlockingQueue 创建并发生产者/消费者程序。您可以使用 ConcurrentHashMap 创建可由多个线程访问的共享数据存储。您可以使用 CopyOnWriteArrayList 创建一个可由多个线程访问的线程安全列表。

除了 java.util.concurrent 包中的数据结构之外，java.util.concurrent.locks 包还包含许多不同的锁类型，可用于同步对数据结构的访问。 java.util.concurrent.locks 包中的不同锁类型是：

* 重入锁
* 可重入读写锁
* 冲压锁

java.util.concurrent 和 java.util.concurrent.locks 包为 Java 中的并发编程提供了一组强大的工具。但是，有时您可能需要创建自己的自定义并发数据结构。

## 创建自定义并发堆栈

在本节中，我们将了解如何创建自定义并发堆栈数据结构。堆栈是一种数据结构，允许您以后进先出 (LIFO) 的顺序压入和弹出元素。并发栈是可以被多个线程同时访问的栈。

有几种不同的方法可以创建并发堆栈。一种方法是使用 java.util.concurrent.locks.ReentrantLock 类来同步对标准 java.util.Stack 对象的访问。另一种方法是使用 java.util.concurrent.atomic.AtomicReference 类来创建对标准 java.util.Stack 对象的原子引用。

在此示例中，我们将使用 java.util.concurrent.atomic.AtomicReference 类来创建对标准 java.util.Stack 对象的原子引用。

```java
import java.util.Stack;
import java.util.concurrent.atomic.AtomicReference;

public class ConcurrentStack<E> {

    private AtomicReference<Stack<E>> stack;

    public ConcurrentStack() {
        stack = new AtomicReference<Stack<E>>(new Stack<E>());
    }

    public void push(E element) {
        Stack<E> oldStack;
        Stack<E> newStack;

        do {
            oldStack = stack.get();
            newStack = new Stack<E>();
            newStack.push(element);
            newStack.addAll(oldStack);
        } while (!stack.compareAndSet(oldStack, newStack));
    }

    public E pop() {
        Stack<E> oldStack;
        Stack<E> newStack;

        do {
            oldStack = stack.get();
            if (oldStack.isEmpty()) {
                return null;
            }
            newStack = new Stack<E>();
            newStack.addAll(oldStack);
        } while (!stack.compareAndSet(oldStack, newStack));

        return newStack.pop();
    }

    public boolean isEmpty() {
        return stack.get().isEmpty();
    }
}
```

ConcurrentStack 类包含对 Stack 对象的 AtomicReference。 push() 方法用于将元素压入堆栈。 pop() 方法用于从堆栈中弹出一个元素。 isEmpty() 方法用于检查堆栈是否为空。

## 测试并发数据结构

在本节中，我们将了解如何测试并发数据结构。在测试并发数据结构时，使用可以生成大量线程的工具很重要。一种这样的工具是 JUnit @ParallelTest 注释。

@ParallelTest 注释可用于注释将并行运行的测试方法。 @ParallelTest 注解具有以下属性：

* 线程——要使用的线程数
* 超时 - 时间，以毫秒为单位，之后测试将被中止

在此示例中，我们将使用 @ParallelTest 注释来测试 ConcurrentStack 类。

```java
import org.junit.Test;
import org.junit.runner.RunWith;

import junitparams.JUnitParamsRunner;
import junitparams.Parameters;

@RunWith(JUnitParamsRunner.class)
public class ConcurrentStackTest {

    @Test
    @Parameters({ "10", "100", "1000", "10000", "100000" })
    public void testPush(int threads) throws Exception {
        ConcurrentStack<Integer> stack = new ConcurrentStack<Integer>();

        for (int i = 0; i < threads; i++) {
            stack.push(i);
        }

        assertFalse(stack.isEmpty());
    }

    @Test
    @Parameters({ "10", "100", "1000", "10000", "100000" })
    public void testPop(int threads) throws Exception {
        ConcurrentStack<Integer> stack = new ConcurrentStack<Integer>();

        for (int i = 0; i < threads; i++) {
            stack.push(i);
        }

        for (int i = 0; i < threads; i++) {
            stack.pop();
        }

        assertTrue(stack.isEmpty());
    }
}
```

testPush() 方法用于测试 ConcurrentStack 类的 push() 方法。 testPop() 方法用于测试 ConcurrentStack 类的 pop() 方法。

## 结论

在本文中，我们了解了如何创建自定义并发堆栈数据结构。我们还研究了如何测试并发数据结构。