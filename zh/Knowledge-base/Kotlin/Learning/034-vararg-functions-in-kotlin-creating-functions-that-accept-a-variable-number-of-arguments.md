---
title: 034：Kotlin 中的可变参数函数：创建接受可变数量参数的函数
description: 
published: true
date: 2023-02-13T18:55:41.839Z
tags: 
editor: markdown
dateCreated: 2023-02-13T18:55:40.241Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [034: vararg Functions in Kotlin: Creating Functions that Accept a Variable Number of Arguments***English** document is available*](/en/Knowledge-base/Kotlin/Learning/034-vararg-functions-in-kotlin-creating-functions-that-accept-a-variable-number-of-arguments)
{.links-list}


# Kotlin 中的可变参数函数：创建接受可变数量参数的函数

Kotlin 的 vararg 关键字允许我们创建接受可变数量参数的函数。当我们想要编写一个可以接受任意数量参数的函数时，这会很有用，而不必在函数定义中显式指定参数数量。

在本文中，我们将学习如何在 Kotlin 中创建可变参数函数，以及如何在我们的代码中使用它们。我们还将查看一些示例，说明如何使用可变参数函数来简化我们的代码。

## 创建可变参数函数

要在 Kotlin 中创建可变参数函数，我们在函数定义中的参数名称之前使用 vararg 关键字。例如，假设我们要创建一个函数，它接受可变数量的字符串并将它们打印出来。我们可以使用以下函数定义来做到这一点：

```kotlin
fun printStrings(vararg strings: String) {
    for (string in strings) {
        println(string)
    }
}
```

请注意，我们已将 vararg 关键字放在字符串参数之前。这告诉 Kotlin 该函数可以接受任意数量的字符串参数。

我们可以用任意数量的字符串参数调用这个函数，它们都会被打印出来：

```kotlin
printStrings("Hello", "World") // Prints "Hello" and "World"
printStrings("Kotlin", "is", "awesome") // Prints "Kotlin", "is", and "awesome"
```

我们也可以调用不带参数的函数，在这种情况下不会打印任何内容：

```kotlin
printStrings() // Prints nothing
```

## 访问 Vararg 参数

当我们创建一个可变参数函数时，我们可以像访问任何其他参数一样访问函数体中的可变参数。在上面的 printStrings() 函数中，我们在 for 循环中访问了 strings 参数以打印出所有字符串。

我们还可以在函数体之外访问可变参数。为此，我们在调用函数时在参数名称前使用 * 运算符。例如，假设我们有一个可变参数函数，它接受可变数量的整数并将它们打印出来：

```kotlin
fun printInts(vararg ints: Int) {
    for (int in ints) {
        println(int)
    }
}
```

我们可以用任意数量的整数参数调用这个函数，它们都会被打印出来：

```kotlin
printInts(1, 2, 3) // Prints 1, 2, and 3
printInts(4, 5, 6, 7, 8) // Prints 4, 5, 6, 7, and 8
```

我们也可以调用不带参数的函数，在这种情况下不会打印任何内容：

```kotlin
printInts() // Prints nothing
```

现在假设我们有一个整数数组，我们想使用 printInts() 函数将它们全部打印出来。我们可以通过使用 * 运算符将数组“解包”为单独的参数来做到这一点：

```kotlin
val intArray = intArrayOf(1, 2, 3)
printInts(*intArray) // Prints 1, 2, and 3
```

## 可变参数和非可变参数

我们还可以创建具有可变参数和非可变参数的可变参数函数。例如，假设我们要创建一个函数，它接受可变数量的字符串和一个整数，并打印出字符串的次数等于整数：

```kotlin
fun printStringsNTimes(n: Int, vararg strings: String) {
    for (i in 1..n) {
        for (string in strings) {
            println(string)
        }
    }
}
```

在这个函数中，我们有一个非可变参数（n）和一个可变参数（字符串）。我们可以用任意数量的字符串参数调用这个函数，它们都会被打印 n 次：

```kotlin
printStringsNTimes(3, "Hello", "World") // Prints "Hello" and "World" three times
printStringsNTimes(5, "Kotlin", "is", "awesome") // Prints "Kotlin", "is", and "awesome" five times
```

我们也可以调用不带字符串参数的函数，在这种情况下不会打印任何内容：

```kotlin
printStringsNTimes(3) // Prints nothing
```

## 结论

在本文中，我们学习了如何在 Kotlin 中创建可变参数函数，以及如何在我们的代码中使用它们。我们还查看了一些示例，说明如何使用 vararg 函数来简化我们的代码。

如果您想了解有关 Kotlin 的更多信息，请查看 Kotlin 文档。