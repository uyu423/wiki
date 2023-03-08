---
title: 017：Kotlin 中的泛型：使用类型参数编写可重用代码
description: 
published: true
date: 2023-02-02T02:57:44.922Z
tags: 
editor: markdown
dateCreated: 2023-02-02T02:57:43.261Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [017: Generics in Kotlin: Writing Reusable Code with Type Parameters***English** document is available*](/en/Knowledge-base/Kotlin/Learning/017-generics-in-kotlin-writing-reusable-code-with-type-parameters)
{.links-list}


# Kotlin 中的泛型：使用类型参数编写可重用代码

Kotlin 的类型系统旨在帮助您用更少的代码完成更多的工作。它实现此目的的方法之一是允许您编写通用代码，或可在一系列类型中重用的代码。在本文中，我们将了解泛型在 Kotlin 中的工作原理，以及如何使用它们来编写更简洁、更具表现力的代码。

## 什么是泛型？

泛型是许多编程语言的一个特性，它允许您编写可以处理多种类型的代码。这与特定于一种类型的代码相反，例如“Int”或“String”。

泛型最常见的例子之一是 `List` 类型。 `List` 可以包含任何类型的元素，因此它被称为_generic_。在 Kotlin 中，我们可以像这样创建一个包含 `Int` 的 `List`：

```kotlin
val list: List<Int> = listOf(1, 2, 3)
```

我们还可以创建一个 `String` 的 `List`：

```kotlin
val list: List<String> = listOf("a", "b", "c")
```

如您所见，这两个 List 之间唯一不同的是它们包含的元素的类型。 `List` 类型本身是通用的。

## 为什么要使用泛型？

泛型很有用，因为它们允许您编写可用于多种类型的代码。这可以使您的代码更加简洁和富有表现力。

例如，考虑以下打印出 `List` 元素的代码：

```kotlin
fun printList(list: List<Any>) {
    for (element in list) {
        println(element)
    }
}
```

此代码适用于任何 `List`，无论其元素的类型如何。我们可以用它来打印出 `Int` 的 `List`：

```kotlin
val list: List<Int> = listOf(1, 2, 3)
printList(list)
```

我们可以用它来打印出 `String` 的 `List`：

```kotlin
val list: List<String> = listOf("a", "b", "c")
printList(list)
```

如果我们不使用泛型，我们将不得不编写两个不同的函数，一个用于 `Int` 的 `List`，一个用于 `String` 的 `List`。泛型允许我们编写一个可用于多种类型的函数。

## 泛型如何工作？

Kotlin 中的泛型是使用_类型参数_实现的。类型参数是特定类型的占位符。创建泛型类型时，您指定一个或多个类型参数。例如，“List”类型有一个名为“T”的类型参数。

当您创建泛型类型的实例时，您指定类型参数应替换为的类型。例如，当我们创建一个 List<Int> 时，我们指定类型参数 T 应该替换为 Int 类型。

## 使用类型参数

可以通过多种方式使用类型参数。最常见的是指定集合中元素的类型。例如，“List”类型有一个类型参数，用于指定“List”中元素的类型。

我们已经了解了如何使用类型参数来指定 `List` 中元素的类型。我们还可以使用类型参数来指定 `Map` 中键和值的类型：

```kotlin
val map: Map<String, Int> = mapOf("a" to 1, "b" to 2, "c" to 3)
```

在此示例中，我们已指定 `Map` 中键的类型应为 `String`，值的类型应为 `Int`。

类型参数也可用于指定“可空”类型中值的类型：

```kotlin
val nullable: String? = null
```

在此示例中，我们已指定 `Nullable` 类型中值的类型应为 `String`。

## 声明类型参数

创建泛型类型时，您指定一个或多个类型参数。例如，“List”类型有一个名为“T”的类型参数。

您可以使用 typeparam 关键字声明类型参数。例如，我们可以创建一个名为 MyType 的泛型类型，它带有一个名为 `T` 的类型参数，如下所示：

```kotlin
typealias MyType<T> = T
```

## 边界

有时您可能希望限制可用作类型参数的类型。例如，您可能希望指定类型参数必须是“Any”的子类型。 Kotlin 将其称为_上限_。

您可以使用“where”关键字指定上限。例如，我们可以创建一个名为“MyType”的泛型类型，其类型参数名为“T”，其上限为“Any”，如下所示：

```kotlin
typealias MyType<T> where T : Any
```

在此示例中，我们指定类型参数“T”必须是“Any”的子类型。这意味着我们可以使用任何类型作为类型参数 `T`，包括 `Int`、`String`、`List` 等等。

我们还可以使用“where”关键字指定下限。例如，我们可以创建一个名为“MyType”的泛型类型，其类型参数名为“T”，下限为“Any”，如下所示：

```kotlin
typealias MyType<T> where T : Any
```

在此示例中，我们指定类型参数“T”必须是“Any”的超类型。这意味着我们可以使用任何类型作为类型参数“T”，包括“Any”、“Any?”等。

## 通配符

有时您可能希望在不指定类型的情况下使用类型参数。例如，您可能想要创建一个可以打印出任何 `List` 元素的函数。

在 Kotlin 中，您可以使用通配符来指定类型参数可以是任何类型。例如，我们可以创建一个函数来打印出任何 `List` 的元素，如下所示：

```kotlin
fun printList(list: List<*>) {
    for (element in list) {
        println(element)
    }
}
```

在此示例中，我们使用通配符指定类型参数“T”可以是任何类型。这意味着我们可以将 printList 函数与任何 List 一起使用，而不管其元素的类型如何。

## 结论

在本文中，我们了解了泛型在 Kotlin 中的工作原理。我们已经了解了如何使用类型参数来编写更简洁、更具表现力的代码。我们还了解了如何声明类型参数以及如何使用边界和通配符。