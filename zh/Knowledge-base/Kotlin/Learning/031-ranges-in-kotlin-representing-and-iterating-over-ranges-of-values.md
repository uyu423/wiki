---
title: 031：Kotlin 中的范围：表示和迭代值的范围
description: 
published: true
date: 2023-02-10T17:55:15.971Z
tags: 
editor: markdown
dateCreated: 2023-02-10T17:55:14.340Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [031: Ranges in Kotlin: Representing and Iterating Over Ranges of Values***English** document is available*](/en/Knowledge-base/Kotlin/Learning/031-ranges-in-kotlin-representing-and-iterating-over-ranges-of-values)
{.links-list}


# Kotlin 中的范围：表示和迭代值的范围

范围是 Kotlin 中的一个基本概念，它允许您表示一系列值。在本文中，我们将了解如何在 Kotlin 中创建和迭代范围。

## 创建范围

在 Kotlin 中有两种创建范围的方法：使用 `..` 运算符，或使用 `rangeTo()` 函数。

`..` 运算符用于创建包含起始值和结束值的范围。例如，以下代码创建一个从 1 到 5 的范围：

```kotlin
val range1 = 1..5
```

另一方面，`rangeTo()` 函数用于创建排除其最终值的范围。例如，以下代码创建一个从 1 到 5 的范围：

```kotlin
val range2 = 1.rangeTo(5)
```

这两个范围都*包含*，这意味着它们包括它们的开始值和结束值。您还可以使用 `until` 关键字而不是 `..` 或 `.rangeTo()` 来创建*独占*范围。例如，以下代码创建一个从 1 到 5 的范围：

```kotlin
val range3 = 1 until 5
```

## 遍历范围

现在我们知道如何创建范围，让我们来看看如何迭代它们。我们可以使用 for 循环来做到这一点：

```kotlin
for (i in 1..5) {
    println(i)
}
```

此代码会将数字 1 到 5 打印到控制台。我们还可以使用 `downTo` 关键字反向迭代范围：

```kotlin
for (i in 5 downTo 1) {
    println(i)
}
```

此代码会将数字 5 到 1 打印到控制台。

## 结论

在这篇文章中，我们了解了如何在 Kotlin 中创建和迭代范围。范围是一个强大的工具，可以在各种情况下使用。我希望你发现它们和我一样有用！