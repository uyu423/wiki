---
title: 052：Kotlin 中的可空性和空安全性：管理代码中的空值
description: 
published: true
date: 2023-02-14T03:17:31.287Z
tags: 
editor: markdown
dateCreated: 2023-02-14T03:17:29.680Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [052: Nullability and Null Safety in Kotlin: Managing Null Values in Your Code***English** document is available*](/en/Knowledge-base/Kotlin/Learning/052-nullability-and-null-safety-in-kotlin-managing-null-values-in-your-code)
{.links-list}


## 介绍

Kotlin 是一种在 Java 虚拟机上运行的静态类型编程语言。它是一种可与 Java 互操作的 JVM 语言，可用于开发 Android 应用程序。

Kotlin 的关键特性之一是空安全。 Null 安全是避免 NullPointerException 的能力。 Kotlin 通过使用可空类型和非空类型来实现空安全。

可空类型可以保存空值，而非空类型不能。这意味着如果您尝试将空值分配给非空类型，您将收到编译时错误。

## 可空和非空类型

Kotlin 有两种可空类型和非空类型：

* **可空类型**：可以容纳空值的类型。科特林使用 ? （问号）表示可为 null 的类型。

* **非空类型**：不能容纳空值的类型。科特林使用 !! （双感叹号）表示非空类型。

以下是如何声明可空类型和非空类型的示例：

```kotlin
// Nullable type
var name: String? = "John"

// Non-null type
var age: Int = 20
```

如您所见，可空类型使用 ?在类型名称之后，非空类型声明时没有 ?。

## 分配空值

您可以将空值分配给可空类型，但不能将空值分配给非空类型。

如果您尝试将空值分配给非空类型，则会出现编译时错误。

以下是如何将空值分配给可空类型的示例：

```kotlin
var name: String? = "John"

name = null
```

如您所见，我们声明了一个可空类型并为其分配了一个空值。这是允许的，因为类型可以为空。

但是，如果我们尝试对非 null 类型执行相同操作，则会出现编译时错误：

```kotlin
var age: Int = 20

age = null // This will give a compile-time error
```

## 检查空值

在使用它们之前，您应该始终检查空值。 Kotlin 提供了 ?. （安全呼叫运营商）和 !! （非空断言运算符）帮助您检查空值。

这 ？。运算符在访问它之前检查该值是否为空。如果值为 null，它将返回 null。否则，它将返回值。

这是一个如何使用 ? 的示例。操作员：

```kotlin
var name: String? = "John"

// This will print "John"
println(name?.length)

name = null

// This will print "null"
println(name?.length)
```

如您所见，我们在访问其 length 属性之前检查了 name 变量是否为 null。如果 name 变量为 null，则 ?.运算符将返回 null。否则，它将返回值。

这 ！！运算符用于强制解包一个值。这意味着它会返回值，即使它是 null。

这可能很危险，因为如果该值实际上为 null，它可能会导致 NullPointerException。

这是一个如何使用 !! 的示例。操作员：

```kotlin
var name: String? = "John"

// This will print "John"
println(name!!.length)

name = null

// This will give a NullPointerException
println(name!!.length)
```

如您所见，我们使用了 !!运算符强制展开名称变量。即使名称变量为空，!!运算符仍将返回值。

但是，如果我们尝试访问 name 变量的 length 属性，我们将得到一个 NullPointerException，因为 name 变量实际上是 null。

## 结论

在这篇文章中，我们了解了 Kotlin 中的空安全。我们已经了解了可空类型和非空类型以及如何为它们分配空值。我们还了解了 ?。和 ！！运算符以及如何使用它们来检查空值。