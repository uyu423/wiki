---
title: 010：Kotlin 中的协程：让异步编程变得简单
description: 
published: true
date: 2023-01-31T05:27:21.992Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:27:20.312Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [010: Coroutines in Kotlin: Asynchronous Programming Made Easy***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/010-coroutines-in-kotlin-asynchronous-programming-made-easy)
{.links-list}


Kotlin 协程允许您以顺序方式编写异步代码。这意味着您可以像同步运行一样编写代码，而不必处理线程的复杂性。

协程在 1.1 版中被添加到 Kotlin 中，它们提供了一种编写异步代码的强大方法。在本文中，我们将了解协程是什么、它们如何工作以及如何在您自己的代码中使用它们。

## 什么是协程？

协程是一种以顺序方式编写异步代码的方法。这意味着您可以像同步运行一样编写代码，而不必处理线程的复杂性。

协程在 1.1 版中被添加到 Kotlin 中，它们提供了一种编写异步代码的强大方法。在本文中，我们将了解协程是什么、它们如何工作以及如何在您自己的代码中使用它们。

## 协程如何工作？

协程是可以挂起和恢复的轻量级线程。这意味着协程可以在执行过程中暂停并在稍后恢复。

协程的结构如下：

- 协程是用父协程创建的。
- 一个协程有一个上下文，它决定了它的生命周期以及它如何与其他协程交互。
- 协程有一个suspend函数，用于暂停协程。
- 协程有一个resume函数，用于恢复协程。

当一个协程被创建时，它被赋予一个父协程。这个父协程负责管理子协程的执行。在父协程恢复之前，子协程无法恢复。

协程的上下文决定了它的生命周期。协程可以被取消，这将导致它终止。协程也可以完成，这意味着它已经完成了执行。

可以使用 suspend 函数暂停协程。此函数将挂起函数作为参数。当suspend函数被调用时，协程被暂停，suspend函数被执行。

resume 函数用于恢复协程。此函数将恢复函数作为参数。当调用 resume 函数时，恢复协程并执行 resume 函数。

## 如何使用协程

使用协程很简单。只需将以下行添加到您的代码中：

```kotlin
import kotlinx.coroutines.*
```

此行从 Kotlin 导入协程库。

现在您可以在代码中使用协程。例如，下面的代码创建一个协程然后暂停它：

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

在这段代码中，我们创建了一个带有启动函数的协程。此函数创建一个新协程并返回对它的引用。我们将此引用存储在子变量中。

然后我们使用 suspend 函数暂停子协程。此函数将挂起函数作为参数。在这种情况下，暂停功能是延迟。此函数将协程暂停指定时间（1000 毫秒）。

当我们运行这段代码时，我们会看到以下输出：

```
Main coroutine
Child coroutine
```

子协程在调用 delay 函数后暂停。主协程继续运行并打印“Main coroutine”。

我们可以使用 resume 函数恢复子协程：

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

在这段代码中，我们使用 resume 函数来恢复子协程。此函数将恢复函数作为参数。在这种情况下，恢复功能是延迟。此函数将协程暂停指定时间（1000 毫秒）。

当我们运行这段代码时，我们会看到以下输出：

```
Main coroutine
Child coroutine
Child coroutine after delay
```

子协程在调用 delay 函数后恢复。主协程继续运行并打印“Main coroutine”。

## 取消协程

您可以使用 cancel 函数取消协程：

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

在这段代码中，我们使用取消函数来取消子协程。此函数将挂起函数作为参数。在这种情况下，暂停功能是延迟。此函数将协程暂停指定时间（1000 毫秒）。

当我们运行这段代码时，我们会看到以下输出：

```
Main coroutine
Child coroutine
```

调用delay函数后子协程被取消。主协程继续运行并打印“Main coroutine”。

## 结论

在本文中，我们了解了 Kotlin 中的协程。我们已经了解了它们是什么、它们如何工作以及如何在您自己的代码中使用它们。协程是一种编写异步代码的强大方式。