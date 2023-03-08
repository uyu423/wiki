---
title: 037：Kotlin 中的内联函数：使用内联函数提高性能
description: 
published: true
date: 2023-02-16T10:32:23.640Z
tags: 
editor: markdown
dateCreated: 2023-02-16T10:32:21.636Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [037: Inline Functions in Kotlin: Improving Performance with Inlined Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/037-inline-functions-in-kotlin-improving-performance-with-inlined-functions)
{.links-list}


## 介绍

Kotlin 是一种静态类型的编程语言，运行在 Java 虚拟机上，也可以编译成 JavaScript 源代码。

在这篇文章中，我们将看看如何在 Kotlin 中使用内联函数来提高性能。

## 什么是内联函数？

在 Kotlin 中，内联函数是在调用者主体中展开的函数。这与非内联函数不同，非内联函数像往常一样被调用。

内联函数可用于通过减少函数调用的开销来提高性能。此外，内联函数可以访问调用者的变量，这也可以提高性能。

## 如何使用内联函数

为了使用内联函数，您需要使用 `inline` 关键字注释函数。

例如，假设我们有一个要内联的函数“foo()”：

```kotlin
inline fun foo() {
    // do something
}
```

现在，每当我们调用 foo() 时，函数体都会在调用者中展开。

## 何时使用内联函数

通常，只有在确定内联函数会提高性能时才应使用内联函数。

此外，如果函数又小又简单，则只应使用内联函数。这是因为内联一个复杂的函数会导致代码膨胀，实际上会降低性能。

最后，如果您确定不会从多个地方调用该函数，则只应使用内联函数。这是因为如果从多个地方调用函数，内联函数会导致重复代码。

## 结论

在本文中，我们了解了 Kotlin 中的内联函数以及如何使用它们来提高性能。通常，只有在确定内联函数会提高性能时才应使用内联函数。此外，如果函数又小又简单，则只应使用内联函数。