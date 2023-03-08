---
title: 054：Kotlin 中的一等公民函数：理解高阶函数
description: 
published: true
date: 2023-02-16T18:33:04.065Z
tags: 
editor: markdown
dateCreated: 2023-02-16T18:32:55.838Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [054: Functions as First-Class Citizens in Kotlin: Understanding Higher-Order Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/054-functions-as-first-class-citizens-in-kotlin-understanding-higher-order-functions)
{.links-list}


## 介绍

Kotlin 是一种运行在 Java 虚拟机上的现代编程语言。它是一种静态类型语言，结合了面向对象和函数式编程的最佳特性。

Kotlin 是 JVM 上的一等公民，这意味着它可以用来开发任何类型的 Java 应用程序，从简单的命令行程序到复杂的 Web 应用程序。

Kotlin 最重要的特性之一是它支持高阶函数。在本文中，我们将学习什么是高阶函数以及如何在 Kotlin 中使用它们。

## 什么是高阶函数？

高阶函数是一种将一个或多个函数作为参数并返回一个函数作为结果的函数。

在 Kotlin 中，高阶函数由“Function<T, R>”类型表示。此类型有两个类型参数：

- ```T``` 是函数参数的类型。
- ```R``` 是函数结果的类型。

```kotlin
val list = listOf("a", "b", "c")

val upperCaseList = list.map { it.toUpperCase() }

// upperCaseList is now a list of strings: ["A", "B", "C"]
```map``` 函数

```kotlin
val list = listOf(1, 2, 3)

val doubleList = list.map { it * 2 }

// doubleList is now a list of integers: [2, 4, 6]
```map``` 函数来做到这一点：

```kotlin
val list = listOf("a", "ab", "abc", "abcd")

val filteredList = list.filter { it.length <= 3 }

// filteredList is now a list of strings: ["a", "ab", "abc"]
```

在上面的示例中，我们有一个字符串列表，我们使用 ```map``` 函数将 ```toUpperCase()``` 函数应用于列表的每个元素。

```kotlin
val list = listOf(1, 2, 3, 4, 5)

val filteredList = list.filter { it % 2 == 0 }

// filteredList is now a list of integers: [2, 4]
```科特林
val 列表 = listOf(1, 2, 3)

val doubleList = list.map { 它 * 2 }

// doubleList 现在是一个整数列表：[2, 4, 6]
```kotlin
val list = listOf(1, 2, 3, 4, 5)

val sum = list.reduce { a, b -> a + b }

// sum is now 15
```filter``` 函数

```kotlin
val list = listOf("a", "b", "c")

val concatenatedString = list.reduce { a, b -> a + b }

// concatenatedString is now "abc"
```filter``` 函数将返回一个新列表，其中仅包含函数返回 ```true``` 的元素。

例如，假设我们有一个字符串列表，我们想过滤掉所有长度超过三个字符的字符串。我们可以使用 ```filter``` 函数来做到这一点：

```科特林
val list = listOf("a", "ab", "abc", "abcd")

val filteredList = list.filter { it.length <= 3 }

// filteredList 现在是一个字符串列表：["a", "ab", "abc"]
```

在上面的示例中，我们有一个字符串列表，我们使用 ```filter``` 函数删除所有长度超过三个字符的字符串。

```filter``` 函数可以用于任何类型的列表，而不仅仅是字符串列表。例如，我们可以将 ```filter``` 与整数列表一起使用：

```科特林
val list = listOf(1, 2, 3, 4, 5)

val filteredList = list.filter { 它 % 2 == 0 }

// filteredList 现在是一个整数列表：[2, 4]
```

在上面的示例中，我们有一个整数列表，我们使用 ```filter``` 函数删除所有奇数。

### ```reduce``` 函数

```reduce``` 函数是一个高阶函数，它将一个函数作为参数并将其应用于列表的每个元素。该函数应采用两个参数并返回一个值。

```reduce``` 函数将返回一个值，该值是将函数应用于列表中每个元素的结果。

例如，假设我们有一个整数列表，我们想要找到列表中所有元素的总和。我们可以使用```reduce```函数来做到这一点：

```科特林
val list = listOf(1, 2, 3, 4, 5)

val sum = list.reduce { a, b -> a + b }

// 总和现在是 15
```

在上面的示例中，我们有一个整数列表，我们使用 ```reduce``` 函数来查找列表中所有元素的总和。

```reduce``` 函数可以用于任何类型的列表，而不仅仅是整数列表。例如，我们可以将 ```reduce``` 与字符串列表一起使用：

```科特林
val list = listOf("a", "b", "c")

val concatenatedString = list.reduce { a, b -> a + b }

// concatenatedString 现在是 "abc"
```

在上面的示例中，我们有一个字符串列表，我们使用 ```reduce``` 函数将所有字符串连接成一个字符串。

## 结论

在本文中，我们了解了高阶函数是什么以及如何在 Kotlin 中使用它们。我们已经看到了如何使用```map```、```filter``` 和```reduce``` 函数来转换和操作列表。

高阶函数是一种强大的工具，可用于编写简洁易读的代码。如果您是 Kotlin 的新手，我鼓励您尝试使用高阶函数，看看您能想出什么。