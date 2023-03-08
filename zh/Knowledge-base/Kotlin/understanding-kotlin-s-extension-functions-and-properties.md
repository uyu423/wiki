---
title: 了解 Kotlin 的扩展函数和属性
description: 
published: true
date: 2023-02-02T03:36:28.480Z
tags: 
editor: markdown
dateCreated: 2023-02-02T03:36:26.957Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Understanding Kotlin's Extension Functions and Properties***English** document is available*](/en/Knowledge-base/Kotlin/understanding-kotlin-s-extension-functions-and-properties)
{.links-list}


# 了解 Kotlin 的扩展函数和属性

Kotlin 是一种功能强大的编程语言，它提供了许多使开发更快、更容易的功能。这些特性之一是扩展函数和属性。

扩展函数和属性允许您扩展类的功能而不必继承它。当您想使用库中的功能而不依赖于该库时，这尤其有用。

在本文中，我们将仔细研究 Kotlin 中的扩展函数和属性。我们将学习如何定义它们以及如何在我们自己的代码中使用它们。

## 定义扩展函数和属性

扩展函数和属性分别使用“fun”和“val”关键字定义。它们写在它们扩展的类的名称之后，后跟一个点“.”：

```kotlin
// Extension function
fun String.repeat(times: Int): String {
    return this.repeat(times)
}

// Extension property
val String.length: Int
    get() = this.length
```

在上面的示例中，我们定义了一个扩展函数“repeat”，它允许我们将字符串重复给定的次数。我们还定义了一个扩展属性“length”，它允许我们获取字符串的长度。

请注意，扩展函数和属性实际上并未在它们扩展的类中定义。它们在定义它们的类中被编译为静态方法和属性。这意味着它们可以从任何地方调用，甚至可以从类外部调用。

## 使用扩展函数和属性

扩展函数和属性可以像任何其他函数或属性一样使用。在下面的示例中，我们使用 `repeat` 函数将字符串重复 10 次：

```kotlin
fun main() {
    val s = "Hello, world!".repeat(10)
    println(s)
}
```

我们还可以使用 `length` 属性来获取字符串的长度：

```kotlin
fun main() {
    val s = "Hello, world!"
    println(s.length)
}
```

## 覆盖扩展函数和属性

也可以覆盖扩展函数和属性。当您想要在特定上下文中更改函数或属性的行为时，这会很有用。

要覆盖扩展函数或属性，您只需要以与任何其他函数或属性相同的方式定义它。在下面的示例中，我们覆盖了 `repeat` 函数，以便它返回具有给定数量的感叹号的字符串：

```kotlin
fun main() {
    fun String.repeat(times: Int): String {
        return this + "!".repeat(times)
    }

    val s = "Hello, world!".repeat(10)
    println(s)
}
```

## 结论

扩展函数和属性是 Kotlin 中的一项强大功能，可用于扩展类的功能而无需继承类。它们分别使用 `fun` 和 `val` 关键字定义，并且写在它们扩展的类的名称之后，后跟一个点 `.`

扩展函数和属性可以像任何其他函数或属性一样使用。它们被编译为静态方法和属性，这意味着它们可以从任何地方调用，甚至可以从类外部调用。

也可以覆盖扩展函数和属性。当您想要在特定上下文中更改函数或属性的行为时，这会很有用。