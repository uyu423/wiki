---
title: 078：Kotlin 中的策略模式：将算法封装为对象
description: 
published: true
date: 2023-02-14T17:55:28.585Z
tags: 
editor: markdown
dateCreated: 2023-02-14T17:55:26.996Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [078: The Strategy Pattern in Kotlin: Encapsulating Algorithms as Objects***English** document is available*](/en/Knowledge-base/Kotlin/Learning/078-the-strategy-pattern-in-kotlin-encapsulating-algorithms-as-objects)
{.links-list}


# 078：Kotlin 中的策略模式：将算法封装为对象

## 介绍

策略模式是一种行为软件设计模式，可以在运行时选择算法的行为。这在应用程序需要使用不同的算法时很有用，算法的选择可以在运行时根据用户的输入或应用程序的当前状态进行。

策略模式也称为策略模式。

## 问题

假设我们有一个对整数列表进行排序的简单应用程序。我们可以从编写一个简单的“排序”函数开始，如下所示：

```kotlin
fun sort(list: List<Int>): List<Int> {
    // implement sorting algorithm here
}
```

此“排序”函数将整数列表作为输入并返回按升序排序的新整数列表。

现在假设我们想在我们的应用程序中添加另一种排序算法。我们可以编写另一个 `sort` 函数，但这样我们就会有两个名称相同但行为不同的函数。这会让我们的应用程序的用户感到困惑。

相反，我们可以使用策略模式将每个排序算法封装在它自己的对象中。然后我们可以编写一个“排序”函数，它将一个整数列表和一个策略对象作为输入，并使用策略对象对列表进行排序。

## 解决方案

以下是我们如何使用策略模式对整数列表进行排序：

```kotlin
// define a sorting strategy interface
interface SortingStrategy {
    fun sort(list: List<Int>): List<Int>
}

// implement a sorting strategy for ascending order
class AscendingSortingStrategy : SortingStrategy {
    override fun sort(list: List<Int>): List<Int> {
        // implement sorting algorithm here
    }
}

// implement a sorting strategy for descending order
class DescendingSortingStrategy : SortingStrategy {
    override fun sort(list: List<Int>): List<Int> {
        // implement sorting algorithm here
    }
}

// use the strategy pattern to sort a list of integers
fun sort(list: List<Int>, strategy: SortingStrategy): List<Int> {
    return strategy.sort(list)
}
```

在上面的代码中，我们定义了一个表示排序策略的 SortingStrategy 接口。我们还实现了两种排序策略：`AscendingSortingStrategy` 和 `DescendingSortingStrategy`。

最后，我们编写了一个 `sort` 函数，它将整数列表和排序策略作为输入，并使用排序策略对列表进行排序。

我们现在可以像这样使用我们的 `sort` 函数：

```kotlin
// sort a list of integers in ascending order
val ascendingList = sort(list, AscendingSortingStrategy())

// sort a list of integers in descending order
val descendingList = sort(list, DescendingSortingStrategy())
```

## 好处

策略模式有几个好处：

- 它允许在运行时选择算法的行为。

- 它使向应用程序添加新算法变得容易。

- 它使测试算法变得容易。

- 它使代码更具可读性和可维护性。

## 陷阱

使用策略模式时有一些潜在的陷阱：

- 它可以使代码更复杂。

- 它会使代码更难阅读和理解。

- 它会使更改或添加新算法变得更加困难。