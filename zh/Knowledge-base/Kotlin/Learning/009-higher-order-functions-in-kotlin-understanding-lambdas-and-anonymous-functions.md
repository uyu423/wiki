---
title: 009：Kotlin 中的高阶函数：了解 Lambda 和匿名函数
description: 
published: true
date: 2023-01-31T05:36:06.422Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:36:02.791Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [009: Higher-Order Functions in Kotlin: Understanding Lambdas and Anonymous Functions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/009-higher-order-functions-in-kotlin-understanding-lambdas-and-anonymous-functions)
{.links-list}


# 009：Kotlin 中的高阶函数：理解 Lambda 和匿名函数

在计算机编程中，高阶函数是一种将一个或多个函数作为参数（即过程参数）并返回一个新函数作为其结果的函数。

在 Kotlin 中，高阶函数非常常见，因为该语言拥有丰富的内置函数集，而且函数是一等公民，这意味着它们可以存储在变量中并作为参数传递给其他函数。

Kotlin 中最常用的高阶函数之一是 apply 函数，它用于在对象上执行给定的代码块，然后返回对象本身。例如，考虑以下代码：

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

在上面的代码中，`apply` 函数用于在 `list` 对象上执行给定的代码块（即大括号之间的代码），然后返回 `list` 对象本身。然后使用 also 函数对 list 对象执行一些额外的操作（在本例中，将其打印到控制台）。

了解高阶函数的关键之一是它们可用于抽象出重复的代码模式。例如，考虑以下代码：

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

在上面的代码中，`apply` 函数用于向 `list` 添加一个新元素，然后返回 `list`。这种特殊的代码模式非常常见，以至于 Kotlin 提供了一个内置的 `+=` 运算符，可以用来代替：

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list += 5
    list += listOf(6, 7, 8)

    println(list)
}
```

`+=` 运算符只是 `apply` 函数的简写，这意味着它等同于以下代码：

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }

    println(list)
}
```

如您所见，`+=` 运算符可用于抽象出将元素添加到列表（或任何其他可变集合）的常见代码模式。

另一个常见的高阶函数是 let 函数，它用于在对象上执行给定的代码块，然后返回代码的结果。例如，考虑以下代码：

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list.let {
        it.add(5)
        it.addAll(listOf(6, 7, 8))
        it
    }

    println(newList)
}
```

在上面的代码中，`let` 函数用于在 `list` 对象上执行给定的代码块，然后返回 `list` 对象本身。 `it` 变量用于引用代码块内的 `list` 对象。

与 apply 函数类似，let 函数可用于抽象出重复的代码模式。例如，考虑以下代码：

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list.let {
        it.add(5)
        it.addAll(listOf(6, 7, 8))
        it
    }

    println(newList)
}
```

在上面的代码中，`let` 函数用于向 `list` 添加一个新元素，然后返回 `list`。这种特殊的代码模式非常常见，以至于 Kotlin 提供了一个内置的 `+=` 运算符，可以用来代替：

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list += 5
    val newList = list += listOf(6, 7, 8)

    println(newList)
}
```

`+=` 运算符只是 `let` 函数的简写，这意味着它等同于以下代码：

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list.let {
        it.add(5)
        it.addAll(listOf(6, 7, 8))
        it
    }

    println(newList)
}
```

如您所见，`+=` 运算符可用于抽象出将元素添加到列表（或任何其他可变集合）的常见代码模式。

最后，值得一提的是，高阶函数通常与 lambda 结合使用，lambda 是没有名称的匿名函数。 Lambdas 通常用于将代码块作为参数传递给高阶函数。例如，考虑以下代码：

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        this.add(5)
        this.addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

在上面的代码中，`apply` 函数用于在 `list` 对象上执行给定的 lambda，然后返回 `list` 对象本身。然后使用 also 函数对 list 对象执行一些额外的操作（在本例中，将其打印到控制台）。

如您所见，lambda 可用于抽象出重复的代码模式。例如，考虑以下代码：

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

在上面的代码中，`apply` 函数用于向 `list` 添加一个新元素，然后返回 `list`。这种特殊的代码模式非常常见，以至于 Kotlin 提供了一个内置的 `+=` 运算符，可以用来代替：

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list += 5
    list += listOf(6, 7, 8)

    println(list)
}
```

`+=` 运算符只是 `apply` 函数的简写，这意味着它等同于以下代码：

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }

    println(list)
}
```

如您所见，`+=` 运算符可用于抽象出将元素添加到列表（或任何其他可变集合）的常见代码模式。

关键点：
- 高阶函数是将一个或多个函数作为参数并返回一个新函数作为其结果的函数。
- 在 Kotlin 中，高阶函数非常普遍，这是由于语言丰富的内置函数集以及函数是一等公民这一事实。
- Kotlin 中最常用的高阶函数之一是 `apply` 函数，它用于在对象上执行给定的代码块，然后返回对象本身。
- 另一个常见的高阶函数是 `let` 函数，它用于在对象上执行给定的代码块，然后返回代码的结果。
- 高阶函数通常与 lambda 结合使用，lambda 是没有名称的匿名函数。