---
title: 使用 Kotlin 的 Channels 和 Flow 进行并发编程
description: 
published: true
date: 2023-02-08T19:55:19.927Z
tags: 
editor: markdown
dateCreated: 2023-02-08T19:55:18.275Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Concurrent Programming with Kotlin's Channels and Flow***English** document is available*](/en/Knowledge-base/Kotlin/concurrent-programming-with-kotlin-s-channels-and-flow)
{.links-list}


# 使用 Kotlin 的 Channels 和 Flow 进行并发编程

在并发编程中，程序的不同部分可以相互独立运行，以更好地利用 CPU 时间和内存等资源。并发编程的一个常见挑战是协调程序的不同部分以避免冲突。

Kotlin 的通道和流通过允许程序的不同部分相互通信，提供了一种管理并发编程的有用方法。通道就像管道一样，可以将数据从程序的一部分传输到另一部分，流是管理通过这些通道的数据流的一种方式。

下面是一个简单示例，说明如何使用通道和流来协调程序的不同部分。我们有一个需要打印数字列表的程序，但我们想分两部分来完成：一部分打印数字本身，另一部分在打印数字后打印一条消息。

我们可以使用一个通道将程序第一部分的数字发送到第二部分，并使用流来确保只有在所有数字都发送完后才打印消息。


```kotlin
import kotlinx.coroutines.*
import kotlinx.coroutines.flow.*

fun main() {
    val numbers = (1..5).asFlow() // 1
    val printMessage = numbers.onEach { println(it) } // 2
        .collect { println("Done printing numbers") } // 3
    runBlocking {
        launch { printMessage.collect() } // 4
    }
}
```

1. 我们使用 asFlow 扩展函数创建数字流。
2. 我们使用 `onEach` 转换来打印每个流经通道的数字。
3. 我们使用 `collect` 转换等待所有数字打印完毕，然后打印一条消息。
4. 我们启动协程来运行流程。

此示例显示如何使用通道和流来协调程序的不同部分。通道允许程序的不同部分相互通信，流提供了一种管理通过这些通道的数据流的方法。