---
title: 071：Kotlin 中的责任链模式：通过对象链委托请求
description: 
published: true
date: 2023-02-17T04:33:28.387Z
tags: 
editor: markdown
dateCreated: 2023-02-17T04:32:36.348Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [071: The Chain of Responsibility Pattern in Kotlin: Delegating Requests Through a Chain of Objects***English** document is available*](/en/Knowledge-base/Kotlin/Learning/071-the-chain-of-responsibility-pattern-in-kotlin-delegating-requests-through-a-chain-of-objects)
{.links-list}


## 介绍

责任链模式是一种设计模式，涉及沿对象链传递请求以找到合适的处理程序。此模式通常与装饰器模式和命令模式结合使用。

## 问题

假设我们有一个系统，其中包含许多可以处理请求的对象。每个对象都有一定的责任，可以处理请求或将其传递给链中的下一个对象。

问题是很难确定哪个对象应该处理特定请求。我们可能还希望在不更改发出请求的代码的情况下从链中添加或删除对象。

## 解决方案

责任链模式通过创建可以处理请求的对象链来解决这些问题。对象链接在一起，请求从一个对象传递到下一个对象，直到它被处理。

## 执行

让我们看看如何在 Kotlin 中实现责任链模式。

我们将从为请求创建一个类开始：

```kotlin
class Request(val data: String)
```

接下来，我们将为处理程序创建一个类。每个处理程序都将引用链中的下一个处理程序：

```kotlin
abstract class Handler(protected var next: Handler?) {

    fun handle(request: Request) {
        if (canHandle(request)) {
            doHandle(request)
        } else {
            next?.handle(request)
        }
    }

    abstract fun canHandle(request: Request): Boolean

    abstract fun doHandle(request: Request)
}
```

最后，我们将为处理程序创建一些具体的类：

```kotlin
class FirstHandler : Handler(null) {

    override fun canHandle(request: Request): Boolean {
        return request.data.startsWith("first")
    }

    override fun doHandle(request: Request) {
        println("First handler handling request: ${request.data}")
    }
}

class SecondHandler : Handler(null) {

    override fun canHandle(request: Request): Boolean {
        return request.data.startsWith("second")
    }

    override fun doHandle(request: Request) {
        println("Second handler handling request: ${request.data}")
    }
}

class ThirdHandler : Handler(null) {

    override fun canHandle(request: Request): Boolean {
        return request.data.startsWith("third")
    }

    override fun doHandle(request: Request) {
        println("Third handler handling request: ${request.data}")
    }
}
```

我们现在可以创建一个处理程序链并通过链传递请求：

```kotlin
val firstHandler = FirstHandler()
val secondHandler = SecondHandler()
val thirdHandler = ThirdHandler()

firstHandler.next = secondHandler
secondHandler.next = thirdHandler

val request = Request("first request")
firstHandler.handle(request)

val request2 = Request("second request")
firstHandler.handle(request2)

val request3 = Request("third request")
firstHandler.handle(request3)
```

## 优点

责任链模式的主要优点是它允许我们将请求的发送者与接收者分离。发送方不需要知道接收方是谁或请求将如何处理。

另一个优点是我们可以在链中动态添加或删除处理程序，而无需更改发出请求的代码。

## 缺点

责任链模式的一个缺点是很难调试，因为很难确定请求的处理位置。

另一个缺点是责任链模式会导致代码难以维护。

## 结论

在本文中，我们了解了如何在 Kotlin 中实施责任链模式。此模式可用于将请求的发送方与接收方解耦，以及从链中动态添加或删除处理程序。