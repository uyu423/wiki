---
title: 071: The Chain of Responsibility Pattern in Kotlin: Delegating Requests Through a Chain of Objects
description: 
published: true
date: 2023-02-17T04:33:37.376Z
tags: 
editor: markdown
dateCreated: 2023-02-17T04:32:36.375Z
---

- [071: El patrón de cadena de responsabilidad en Kotlin: Delegar solicitudes a través de una cadena de objetos***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/071-the-chain-of-responsibility-pattern-in-kotlin-delegating-requests-through-a-chain-of-objects)
{.links-list}
- [071：Kotlin 中的责任链模式：通过对象链委托请求***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/071-the-chain-of-responsibility-pattern-in-kotlin-delegating-requests-through-a-chain-of-objects)
{.links-list}
- [071: Kotlin의 책임 사슬 패턴: 개체 사슬을 통한 요청 위임***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/071-the-chain-of-responsibility-pattern-in-kotlin-delegating-requests-through-a-chain-of-objects)
{.links-list}


## Introduction

The chain of responsibility pattern is a design pattern that involves passing requests along a chain of objects in order to find the appropriate handler. This pattern is often used in conjunction with the decorator and command patterns.

## The Problem

Suppose we have a system with a number of objects that can handle requests. Each object has a certain responsibility and can either handle the request or pass it on to the next object in the chain.

The problem is that it can be difficult to determine which object should handle a particular request. We may also want to add or remove objects from the chain without having to change the code that makes the request.

## The Solution

The chain of responsibility pattern solves these problems by creating a chain of objects that can handle the request. The objects are linked together and the request is passed from one object to the next until it is handled.

## Implementation

Let's see how we can implement the chain of responsibility pattern in Kotlin.

We'll start by creating a class for the request:

```kotlin
class Request(val data: String)
```

Next, we'll create a class for the handlers. Each handler will have a reference to the next handler in the chain:

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

Finally, we'll create some concrete classes for the handlers:

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

We can now create a chain of handlers and pass requests through the chain:

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

## Advantages

The main advantage of the chain of responsibility pattern is that it allows us to decouple the sender of a request from the receiver. The sender does not need to know who the receiver is or how the request will be handled.

Another advantage is that we can dynamically add or remove handlers from the chain without having to change the code that makes the request.

## Disadvantages

One disadvantage of the chain of responsibility pattern is that it can be difficult to debug because it can be hard to determine where a request is being handled.

Another disadvantage is that the chain of responsibility pattern can lead to code that is difficult to maintain.

## Conclusion

In this post, we've seen how to implement the chain of responsibility pattern in Kotlin. This pattern can be useful for decoupling the sender of a request from the receiver and for dynamically adding or removing handlers from the chain.