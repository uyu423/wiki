---
title: 016：Kotlin 中的异常处理：抛出和捕获异常
description: 
published: true
date: 2023-02-05T10:17:20.882Z
tags: 
editor: markdown
dateCreated: 2023-02-05T10:17:19.267Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [016: Exception Handling in Kotlin: Throwing and Catching Exceptions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/016-exception-handling-in-kotlin-throwing-and-catching-exceptions)
{.links-list}


# Kotlin 中的异常处理：抛出和捕获异常

异常是在程序执行期间发生的中断正常指令流的事件。当抛出异常时，它会创建一个异常对象，其中包含有关错误的信息，例如异常的类型和发生错误时程序的状态。

异常可能由多种原因引起，包括但不限于：

- 代码中的错误
- 无效的用户输入
- 硬件故障

Kotlin 中有两种类型的异常：未检查和检查。未经检查的异常是那些扩展```RuntimeException``` 类的异常，而检查异常是那些扩展```Exception``` 类的异常。

## 抛出异常

可以使用 ```throw``` 关键字手动抛出异常。当您想因错误而中止程序的执行时，这很有用。例如，假设我们有一个计算两个数字的平均值的函数。如果用户传入无效输入，我们希望抛出异常。

```kotlin
fun average(a: Int, b: Int): Double {
    if (a < 0 || b < 0) {
        throw IllegalArgumentException("Numbers must be positive.")
    }
    return (a + b) / 2.0
}
```

在上面的代码中，如果输入为负，我们抛出一个```IllegalArgumentException```。现在，如果我们尝试用负数调用 ```average``` 函数，将抛出异常并且程序将中止。

```kotlin
average(-1, 2) // Throws an IllegalArgumentException
```

## 捕捉异常

可以使用 ```try```/```catch``` 关键字捕获异常。这对于优雅地处理错误和继续执行程序很有用。例如，假设我们想要捕获我们的```average``` 函数抛出的异常并向用户打印一条错误消息。

```kotlin
fun average(a: Int, b: Int): Double {
    if (a < 0 || b < 0) {
        throw IllegalArgumentException("Numbers must be positive.")
    }
    return (a + b) / 2.0
}

fun main(args: Array<String>) {
    val a = -1
    val b = 2
    try {
        val avg = average(a, b)
        println("The average of $a and $b is $avg")
    } catch (e: IllegalArgumentException) {
        println("Error: ${e.message}")
    }
}
```

在上面的代码中，我们捕获了由我们的 ```average``` 函数抛出的 ```IllegalArgumentException```。然后我们向用户打印一条错误消息。

## 附加信息

- 可以使用 ```try```/```catch``` 关键字捕获异常。
- 可以使用 ```throw``` 关键字手动抛出异常。
- 未经检查的异常是那些扩展 ```RuntimeException``` 类的异常。
- 检查的异常是那些扩展```Exception```类的异常。