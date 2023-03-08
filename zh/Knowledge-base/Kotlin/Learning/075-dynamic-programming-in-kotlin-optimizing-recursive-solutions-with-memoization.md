---
title: 075：Kotlin 中的动态编程：使用记忆优化递归解决方案
description: 
published: true
date: 2023-01-31T18:04:34.388Z
tags: 
editor: markdown
dateCreated: 2023-01-31T18:04:32.808Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [075: Dynamic Programming in Kotlin: Optimizing Recursive Solutions with Memoization***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/075-dynamic-programming-in-kotlin-optimizing-recursive-solutions-with-memoization)
{.links-list}



# 075：Kotlin 中的动态编程：使用记忆优化递归解决方案

动态规划是一种通过将复杂问题分解为更小、更简单的子问题来解决复杂问题的强大技术。它可用于通过存储子问题的结果来优化递归解决方案，以便它们可以重复使用而不是重新计算。

在本文中，我们将学习如何使用动态规划来优化 Kotlin 中的递归解决方案。我们将从一个简单的示例开始来说明该技术，然后将其应用于更复杂的问题。

## 一个简单的例子

假设我们要计算第 n 个斐波那契数。我们可以使用以下代码递归地执行此操作：

```kotlin
fun fib(n: Int): Int {
    if (n <= 1) return n
    return fib(n - 1) + fib(n - 2)
}
```

然而，这段代码非常低效，因为它重新计算子问题的结果。例如，当我们计算 `fib(5)` 时，我们计算 `fib(4)` 和 `fib(3)` 两次：

![斐波那契计算](fibonacci.png)

我们可以使用动态规划通过存储子问题的结果来优化这段代码，以便它们可以被重用。我们可以通过使用一个数组来跟踪已经计算出的斐波那契数来做到这一点：

```kotlin
fun fib(n: Int): Int {
    if (n <= 1) return n
    val fibs = IntArray(n + 1)
    fibs[0] = 0
    fibs[1] = 1
    for (i in 2..n) {
        fibs[i] = fibs[i - 1] + fibs[i - 2]
    }
    return fibs[n]
}
```

现在，当我们计算 `fib(5)` 时，我们可以重用 `fib(4)` 和 `fib(3)` 的结果：

![带记忆的斐波那契计算](fibonacci-memoized.png)

这段代码效率更高，因为我们不必重新计算子问题的结果。

## 一个更复杂的例子

现在让我们将动态规划应用于更复杂的问题：背包问题。在背包问题中，给定了一组物品，每件物品都有重量和价值。我们的目标是选择一部分物品，使总价值最大化，同时保持在给定的重量限制以下。

例如，假设我们有以下项目：

|项目 |重量 |价值 |
| --- | --- | --- |
|一个| 2 | 6 |
|乙 | 2 | 10 |
|丙 | 3 | 12 |

并且我们想要找到总重量为 5 或更小且总价值最大化的项目子集。在这种情况下，最佳解决方案是选择项目 A 和 C，它们的总权重为 5，总值为 18。

我们可以使用动态规划来解决背包问题。我们将使用一个数组来跟踪每个重量可以达到的最大值，直到重量限制：

```kotlin
fun knapsack(items: Array<Item>, weightLimit: Int): Int {
    val values = IntArray(weightLimit + 1)
    for (i in items.indices) {
        val item = items[i]
        for (w in weightLimit downTo item.weight) {
            values[w] = max(values[w], values[w - item.weight] + item.value)
        }
    }
    return values[weightLimit]
}
```

在此代码中，“values[w]”表示权重为“w”或更小时可以达到的最大值。我们通过依次考虑每个项目并查看它是否值得添加到背包中来计算这个值。如果是，我们相应地更新 values[w] 。

例如，假设我们正在考虑权重为 2 且值为 6 的项目 A。我们将 `values[2]` 更新为 6（项目 A 的值）并将 `values[3]` 更新为 8（项目 A 的值加上权重为 1) 时我们可以获得的最佳值。

![背包计算](knapsack.png)

我们将继续这个过程，直到我们考虑了所有项目。最后，“values[weightLimit]”包含权重为“weightLimit”或更小时可以达到的最大值。

## 结论

在本文中，我们学习了如何使用动态规划来优化 Kotlin 中的递归解决方案。我们已经看到了如何使用记忆来存储子问题的结果以便它们可以被重用，并且我们已经将这种技术应用于背包问题。