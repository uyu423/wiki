---
title: 了解 Kotlin 中的 CoroutineScope
description: 
published: true
date: 2023-02-14T07:55:19.641Z
tags: 
editor: markdown
dateCreated: 2023-02-14T07:55:17.874Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Understanding the CoroutineScope in Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/understanding-the-coroutinescope-in-kotlin)
{.links-list}


# 了解 Kotlin 中的 CoroutineScope

协程是 Kotlin 中并发编程的强大工具。它们是轻量级线程，可用于提高 Kotlin 应用程序的性能。

在本文中，我们将了解 CoroutineScope 以及如何使用它来管理应用程序中的协程。

## 什么是CoroutineScope？

CoroutineScope 是 Kotlin 协程库中的一个类，用于管理协程的生命周期。它提供了一种方法，可以在取消范围时取消在其范围内启动的所有协程。

可以使用 coroutineScope 构建器函数创建范围。此构建器函数创建一个新范围并将其添加到当前范围。

让我们看一个简单的例子：

```kotlin
fun main() {
    // create a new scope
    val scope = coroutineScope {
        // launch a coroutine in the scope
        launch {
            delay(1000L)
            println("World!")
        }
        println("Hello")
    }
}
```

在上面的示例中，我们使用 coroutineScope 构建器函数来创建一个新的范围。然后我们在范围内启动协程。协程将延迟一秒钟，然后打印“World!”。

请注意协程已在范围内启动。这意味着协程将在范围被取消时被取消。

## 取消 CoroutineScope

 可以使用 cancel 方法取消 CoroutineScope。此方法将取消范围内启动的所有协程。让我们看一个简单的例子：

```kotlin
fun main() {
    // create a new scope
    val scope = coroutineScope {
        // launch a coroutine in the scope
        launch {
            delay(1000L)
            println("World!")
        }
        println("Hello")
    }
    // cancel the scope
    scope.cancel()
}
```

在上面的示例中，我们创建了一个新范围并在该范围内启动了一个协程。协程将延迟一秒钟，然后打印“World!”。

然后我们调用作用域上的取消方法。这将取消范围内启动的所有协程。在这种情况下，协程不会打印“World!”因为它在有机会运行之前就被取消了。

## 结论

在本文中，我们了解了 CoroutineScope 以及如何使用它来管理应用程序中的协程。我们还看到了如何取消范围以及这将如何取消范围内启动的所有协程。