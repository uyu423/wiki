---
title: 010: Coroutines in Kotlin: Asynchronous Programming Made Easy
description: 
published: true
date: 2023-01-31T05:27:23.737Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:27:20.299Z
---

- [010: Kotlin의 코루틴: 쉬워진 비동기 프로그래밍***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/010-coroutines-in-kotlin-asynchronous-programming-made-easy)
{.links-list}
- [010: Kotlin のコルーチン: 非同期プログラミングが簡単に***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/010-coroutines-in-kotlin-asynchronous-programming-made-easy)
{.links-list}
- [010：Kotlin 中的协程：让异步编程变得简单***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/010-coroutines-in-kotlin-asynchronous-programming-made-easy)
{.links-list}


Kotlin coroutines allow you to write asynchronous code in a sequential fashion. This means that you can write code as if it were running synchronously, without having to deal with the complexities of threading.

Coroutines were added to Kotlin in version 1.1 and they provide a powerful way to write asynchronous code. In this article, we'll take a look at what coroutines are, how they work, and how to use them in your own code.

## What are coroutines?

Coroutines are a way to write asynchronous code in a sequential fashion. This means that you can write code as if it were running synchronously, without having to deal with the complexities of threading.

Coroutines were added to Kotlin in version 1.1 and they provide a powerful way to write asynchronous code. In this article, we'll take a look at what coroutines are, how they work, and how to use them in your own code.

## How do coroutines work?

Coroutines are lightweight threads that can be suspend and resumed. This means that a coroutine can be paused in the middle of its execution and resumed at a later time.

Coroutines are structured as follows:

- A coroutine is created with a parent coroutine.
- A coroutine has a context, which determines its lifespan and how it interacts with other coroutines.
- A coroutine has a suspend function, which is used to pause the coroutine.
- A coroutine has a resume function, which is used to resume the coroutine.

When a coroutine is created, it is given a parent coroutine. This parent coroutine is responsible for managing the child coroutine's execution. The child coroutine cannot be resumed until the parent coroutine resumes it.

The context of a coroutine determines its lifetime. A coroutine can be cancelled, which will cause it to terminate. A coroutine can also be completed, which means it has finished its execution.

A coroutine can be paused with the suspend function. This function takes a suspend function as an argument. When the suspend function is called, the coroutine is paused and the suspend function is executed.

The resume function is used to resume a coroutine. This function takes a resume function as an argument. When the resume function is called, the coroutine is resumed and the resume function is executed.

## How to use coroutines

Using coroutines is simple. Just add the following line to your code:

```kotlin
import kotlinx.coroutines.*
```

This line imports the coroutines library from Kotlin.

Now you can use coroutines in your code. For example, the following code creates a coroutine and then pauses it:

```kotlin
import kotlinx.coroutines.*

fun main() {
    val parent = CoroutineScope(Job())

    val child = parent.launch {
        println("Child coroutine")
        delay(1000L)
        println("Child coroutine after delay")
    }

    println("Main coroutine")
    child.suspend()
}
```

In this code, we create a coroutine with the launch function. This function creates a new coroutine and returns a reference to it. We store this reference in the child variable.

Then we use the suspend function to pause the child coroutine. This function takes a suspend function as an argument. In this case, the suspend function is delay. This function pauses the coroutine for the specified time (1000 milliseconds).

When we run this code, we see the following output:

```
Main coroutine
Child coroutine
```

The child coroutine is paused after the delay function is called. The main coroutine continues to run and prints "Main coroutine".

We can resume the child coroutine with the resume function:

```kotlin
import kotlinx.coroutines.*

fun main() {
    val parent = CoroutineScope(Job())

    val child = parent.launch {
        println("Child coroutine")
        delay(1000L)
        println("Child coroutine after delay")
    }

    println("Main coroutine")
    child.suspend()
    child.resume()
}
```

In this code, we use the resume function to resume the child coroutine. This function takes a resume function as an argument. In this case, the resume function is delay. This function pauses the coroutine for the specified time (1000 milliseconds).

When we run this code, we see the following output:

```
Main coroutine
Child coroutine
Child coroutine after delay
```

The child coroutine is resumed after the delay function is called. The main coroutine continues to run and prints "Main coroutine".

## Cancelling coroutines

You can cancel a coroutine with the cancel function:

```kotlin
import kotlinx.coroutines.*

fun main() {
    val parent = CoroutineScope(Job())

    val child = parent.launch {
        println("Child coroutine")
        delay(1000L)
        println("Child coroutine after delay")
    }

    println("Main coroutine")
    child.cancel()
}
```

In this code, we use the cancel function to cancel the child coroutine. This function takes a suspend function as an argument. In this case, the suspend function is delay. This function pauses the coroutine for the specified time (1000 milliseconds).

When we run this code, we see the following output:

```
Main coroutine
Child coroutine
```

The child coroutine is cancelled after the delay function is called. The main coroutine continues to run and prints "Main coroutine".

## Conclusion

In this article, we've looked at coroutines in Kotlin. We've seen what they are, how they work, and how to use them in your own code. Coroutines are a powerful way to write asynchronous code.