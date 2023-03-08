---
title: 045：Kotlin 中的局部函数：在函数中创建函数
description: 
published: true
date: 2023-02-02T01:43:44.840Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:43:43.189Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [045: Local Functions in Kotlin: Creating Functions Within Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/045-local-functions-in-kotlin-creating-functions-within-functions)
{.links-list}


# Kotlin 中的局部函数：在函数中创建函数

当您在 Kotlin 中编写代码时，您经常会发现自己想要在另一个函数内部创建一个函数。这称为**局部函数**。局部函数很有用，因为它们可以访问外部函数的变量，这意味着它们可以用来简化复杂的代码。

在本文中，我们将了解如何在 Kotlin 中创建本地函数。我们还将讨论使用局部函数的一些好处。

## 定义局部函数

局部函数是在另一个函数体内定义的。这是一个例子：

```kotlin
fun outerFunction() {
    fun localFunction() {
        // Code goes here
    }
}
```

如您所见，局部函数是在外部函数体内定义的。重要的是要注意局部函数只能从外部函数中调用。这意味着局部函数具有**局部作用域**。

还值得注意的是，局部函数可以访问外部函数的变量。这是因为局部函数是**嵌套**在外部函数中的。这是一个例子：

```kotlin
fun outerFunction() {
    val outerVariable = " outer"

    fun localFunction() {
        println(outerVariable) // Prints " outer"
    }
}
```

如您所见，局部函数可以访问在外部函数中定义的 `outerVariable` 变量。

## 调用本地函数

局部函数只能从定义它们的函数中调用。这意味着它们具有**本地范围**。这是一个例子：

```kotlin
fun outerFunction() {
    fun localFunction() {
        // Code goes here
    }

    localFunction() // Calls the local function
}
```

如您所见，局部函数是从外部函数内部调用的。如果我们尝试从外部函数外部调用局部函数，我们会得到一个错误：

```kotlin
fun outerFunction() {
    fun localFunction() {
        // Code goes here
    }
}

localFunction() // Error: localFunction is not defined
```

## 本地函数的好处

局部函数很有用，因为它们可以访问外部函数的变量。这意味着它们可以用来简化复杂的代码。

例如，假设我们有一个计算数字阶乘的函数。一个数的阶乘是所有小于或等于该数的正整数的乘积。例如，5 的阶乘为 5 * 4 * 3 * 2 * 1，即 120。

以下是我们如何编写一个函数来计算 Kotlin 中数字的阶乘：

```kotlin
fun factorial(n: Int): Int {
    if (n == 0) {
        return 1
    }

    return n * factorial(n - 1)
}
```

此函数使用**递归**，这是一种编写调用自身的函数的技术。

这个函数的问题是它**不是尾递归**。这意味着该函数在返回结果之前会多次调用自身。这可能会导致 **stack overflow** 错误，当函数调用自身太多次以至于堆栈溢出时就会发生这种情况。

我们可以通过使用局部函数来解决这个问题：

```kotlin
fun factorial(n: Int): Int {
    tailrec fun factorial(acc: Int, n: Int): Int {
        if (n == 0) {
            return acc
        }

        return factorial(acc * n, n - 1)
    }

    return factorial(1, n)
}
```

此函数是**尾递归**，这意味着该函数在返回结果之前只调用自身一次。这意味着可以使用较大的 `n` 值调用该函数而不会遇到堆栈溢出错误。

## 结论

在本文中，我们了解了如何在 Kotlin 中创建本地函数。我们还讨论了使用局部函数的一些好处。

局部函数很有用，因为它们可以访问外部函数的变量。这意味着它们可以用来简化复杂的代码。

如果您有兴趣了解有关本地函数的更多信息，我建议您阅读以下资源：

- 关于 [本地函数] 的 Kotlin 文档(https://kotlinlang.org/docs/reference/local-functions.html)
- 关于 [Kotlin 中的递归和尾递归] 的博客文章(https://blog.kotlin-academy.com/recursion-and-tail-recursion-in-kotlin-f79bc55a326a)
- 关于 [本地函数的好处] 的博客文章(https://blog.kotlin-academy.com/the-benefits-of-local-functions-f79bc55a326a)