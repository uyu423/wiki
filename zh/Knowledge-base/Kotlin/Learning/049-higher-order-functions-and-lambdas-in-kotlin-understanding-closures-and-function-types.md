---
title: 049：Kotlin 中的高阶函数和 Lambda：了解闭包和函数类型
description: 
published: true
date: 2023-02-16T15:32:43.386Z
tags: 
editor: markdown
dateCreated: 2023-02-16T15:32:41.064Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [049: Higher-Order Functions and Lambdas in Kotlin: Understanding Closures and Function Types***English** document is available*](/en/Knowledge-base/Kotlin/Learning/049-higher-order-functions-and-lambdas-in-kotlin-understanding-closures-and-function-types)
{.links-list}


# 049：Kotlin 中的高阶函数和 Lambda：了解闭包和函数类型

在本文中，我们将了解 Kotlin 中的高阶函数和 lambda。我们将了解它们是什么以及如何使用它们，并了解它们背后的一些概念，例如闭包和函数类型。

## 什么是高阶函数和 lambda？

在 Kotlin 中，高阶函数是一种函数，它接受一个或多个函数作为参数，或者返回一个函数作为结果。 Lambda 是一种匿名函数，这意味着它们没有名称。

让我们来看一个以 lambda 作为参数的高阶函数的简单示例。此函数接受一个 lambda，该 lambda 接受一个 Int 并返回一个布尔值，它返回一个列表，其中包含所有在传递给 lambda 时返回 true 的 Int：

```kotlin
fun filter(predicate: (Int) -> Boolean): List<Int> {
    val list = mutableListOf<Int>()
    for (i in 1..10) {
        if (predicate(i)) {
            list.add(i)
        }
    }
    return list
}
```

我们可以这样调用这个函数：

```kotlin
val evenNumbers = filter { it % 2 == 0 }
```

lambda 中的 it 关键字是传递给 lambda 的参数的占位符。在这种情况下，它表示传递到过滤器函数中的 Int。

## 什么是闭包？

闭包是一种捕获其周围环境状态的函数。换句话说，它可以从定义它的范围访问变量。

这是 Kotlin 中闭包的一个简单示例。我们有一个名为 counter 的变量，以及一个递增计数器并返回新值的函数。这个函数是一个闭包，因为它捕获了计数器变量的状态：

```kotlin
var counter = 0
fun incrementCounter(): Int {
    return ++counter
}
```

如果我们多次调用 incrementCounter 函数，它会跟踪计数器变量的当前值并每次返回新值：

```kotlin
incrementCounter() // returns 1
incrementCounter() // returns 2
incrementCounter() // returns 3
```

## 什么是函数类型？

在 Kotlin 中，每个函数都有一个类型。函数的类型由函数接受的参数类型和函数返回值的类型组成。

例如，上一节中的 incrementCounter 函数的类型是 (() -> Int)。这可以理解为“一个不带参数并返回 Int 的函数”。

第一部分中的过滤器函数的类型是 ((Int) -> Boolean) -> List<Int>。这可以理解为“一个函数接受一个函数，该函数接受一个 Int 并返回一个布尔值，并返回一个 Int 列表”。

函数类型在 Kotlin 中很重要，因为它们允许我们指定我们想要使用的函数类型。例如，我们可以编写一个高阶函数，它接受一个类型为 (Int) -> Boolean 的函数，并返回一个列表，其中包含所有在传递给该函数时返回 true 的 Int：

```kotlin
fun filter(predicate: (Int) -> Boolean): List<Int> {
    val list = mutableListOf<Int>()
    for (i in 1..10) {
        if (predicate(i)) {
            list.add(i)
        }
    }
    return list
}
```

我们可以这样调用这个函数：

```kotlin
val evenNumbers = filter { it % 2 == 0 }
```

lambda 中的 it 关键字是传递给 lambda 的参数的占位符。在这种情况下，它表示传递到过滤器函数中的 Int。

## 结论

在本文中，我们了解了 Kotlin 中的高阶函数和 lambda。我们已经了解了如何使用它们，还了解了它们背后的一些概念，例如闭包和函数类型。