---
title: 005：Kotlin 中的函数：定义、调用和返回值
description: 
published: true
date: 2023-02-16T02:32:23.664Z
tags: 
editor: markdown
dateCreated: 2023-02-16T02:32:22.071Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [005: Functions in Kotlin: Defining, Calling, and Returning Values***English** document is available*](/en/Knowledge-base/Kotlin/Learning/005-functions-in-kotlin-defining-calling-and-returning-values)
{.links-list}


# Kotlin 中的函数：定义、调用和返回值

函数是一组执行特定任务的代码。在 Kotlin 中，我们可以定义自己的函数，以便稍后在需要执行该任务时调用。在本文中，我们将学习如何定义函数、调用它们以及从中返回值。

## 定义函数

在 Kotlin 中，我们使用 ```fun``` 关键字定义函数。例如，假设我们要定义一个打印问候消息的函数。我们可以这样做：

```kotlin
fun printGreeting() {
    println("Hello, world!")
}
```

我们还可以定义接受参数的函数。例如，假设我们要定义一个函数来打印带有名称的问候消息。我们可以这样做：

```kotlin
fun printGreeting(name: String) {
    println("Hello, $name!")
}
```

我们还可以定义返回值的函数。例如，假设我们要定义一个计算两个数字之和的函数。我们可以这样做：

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

## 调用函数

我们通过简单地使用它们的名称后跟括号```()```来调用函数。例如，我们可以像这样调用之前定义的 ```printGreeting()``` 函数：

```kotlin
printGreeting() // prints "Hello, world!"
```

如果我们定义了一个接受参数的函数，我们需要在括号 ```()``` 中传递参数。例如，我们可以像这样调用我们之前定义的```printGreeting(name: String)``` 函数：

```kotlin
printGreeting("John") // prints "Hello, John!"
```

如果我们定义了一个返回值的函数，我们需要将返回值存储在一个变量中。例如，我们可以像这样调用我们之前定义的```sum(a: Int, b: Int): Int```函数：

```kotlin
val result = sum(1, 2) // result is 3
```

## 返回值

正如我们在上一节中看到的，我们可以定义返回值的函数。在 Kotlin 中，我们使用 ```return``` 关键字从函数返回一个值。例如，假设我们要定义一个函数来计算两个数字的总和并返回结果。我们可以这样做：

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

我们也可以在不显式使用```return```关键字的情况下返回值。例如，假设我们要定义一个函数来计算两个数字的总和并返回结果。我们可以这样做：

```kotlin
fun sum(a: Int, b: Int): Int = a + b
```

在后一个示例中，我们通过简单地将其分配给函数名称 ```sum``` 来返回 ```a + b``` 的值。

这篇文章就是这样！总之，我们学习了如何定义函数、调用它们以及从中返回值。