---
title: 035：Kotlin 中的 Tailrec 函数：优化递归函数
description: 
published: true
date: 2023-02-16T09:32:34.425Z
tags: 
editor: markdown
dateCreated: 2023-02-16T09:32:26.419Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [035: Tailrec Functions in Kotlin: Optimizing Recursive Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/035-tailrec-functions-in-kotlin-optimizing-recursive-functions)
{.links-list}


# 035：Kotlin 中的 Tailrec 函数：优化递归函数

在本文中，我们将了解如何在 Kotlin 中使用 tailrec 函数来优化递归函数。

递归函数是那些直接或间接调用自身的函数。 tailrec 函数是一种特殊类型的递归函数，其中函数中的最后一条语句是递归调用。

Tailrec 函数比常规递归函数更有效，因为它们被编译为使用循环而不是进行多个函数调用。这可以显着提高性能，尤其是对于多次调用的递归函数。

要在 Kotlin 中创建 tailrec 函数，我们在函数名称前使用 tailrec 关键字。例如，这是一个计算给定数字的阶乘的 tailrec 函数：

```kotlin
tailrec fun factorial(n: Int, result: Int = 1): Int {
    if (n == 1) return result
    return factorial(n - 1, n * result)
}
```

在此示例中，我们在 fun 关键字之前使用了 tailrec 关键字。我们还指定了函数的返回类型 (Int)，并为函数提供了两个参数：n 和 result。

result 参数的默认值为 1，在首次调用该函数时使用。

该函数递归调用自身，直到 n 的值为 1。此时，该函数返回 result 的值。

您可以通过使用不同的值调用它来查看此函数的工作原理：

```kotlin
factorial(5) // 120
factorial(10) // 3628800
```

如您所见，tailrec 函数是计算数字阶乘的更有效方法。

tailrec 函数有一些限制：

- 函数必须是类或对象的成员
- 该函数必须用 tailrec 关键字标记
- 函数必须有一个参数
- 函数必须递归调用自身
- 函数必须返回与参数相同的类型

如果您尝试创建不符合这些条件的 tailrec 函数，您将收到编译器错误。

## 附加信息

以下是一些您可能会觉得有用的其他资源：

- [Kotlin 中的尾递归](https://kotlinlang.org/docs/reference/tail-recursion.html)
- [Kotlin 中的尾调用优化](https://kotlinlang.org/docs/reference/tail-call-optimization.html)