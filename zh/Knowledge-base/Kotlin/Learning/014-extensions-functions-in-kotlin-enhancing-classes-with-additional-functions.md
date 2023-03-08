---
title: 014：Kotlin 中的扩展函数：使用附加函数增强类
description: 
published: true
date: 2023-01-31T16:57:24.971Z
tags: 
editor: markdown
dateCreated: 2023-01-31T16:57:23.409Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [014: Extensions Functions in Kotlin: Enhancing Classes with Additional Functions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/014-extensions-functions-in-kotlin-enhancing-classes-with-additional-functions)
{.links-list}



# 14：Kotlin 中的扩展函数：使用附加函数增强类

Kotlin 是一种用于 JVM、Android 和浏览器的静态类型编程语言。它以其互操作性、安全性、工具支持和简洁的语法而闻名。

Kotlin 最强大的功能之一是扩展功能。扩展函数是添加到现有类的函数，而不必从它们继承。这意味着您可以向现有类添加新功能，而无需修改类本身。

在本文中，我们将了解如何创建扩展函数，以及如何使用它们来增强现有类。

## 创建扩展函数

创建扩展函数很简单。您需要做的就是在函数名称前加上您要扩展的类的名称，后跟一个点。例如，要创建一个向 String 类添加 print() 方法的扩展函数，您可以执行以下操作：

```kotlin
fun String.print() {
    println(this)
}
```

现在，您可以在任何字符串上调用 `print()` 方法，如下所示：

```kotlin
"Hello, world!".print() // prints "Hello, world!"
```

如您所见，扩展函数是向现有类添加新功能的好方法。

## 使用扩展函数

当您想向您无法控制的类添加新方法时，扩展函数特别有用。例如，假设您正在使用一个包含 `User` 类的库，但您想向其中添加一个 `getFullName()` 方法。使用扩展函数，您无需修改 User 类本身即可执行此操作。

首先，让我们定义一个 `User` 类：

```kotlin
class User(val firstName: String, val lastName: String)
```

现在，我们可以创建一个扩展函数，将 getFullName() 方法添加到 User 类：

```kotlin
fun User.getFullName(): String {
    return "$firstName $lastName"
}
```

现在，我们可以创建一个 User 对象并对其调用 getFullName() 方法：

```kotlin
val user = User("John", "Smith")
println(user.getFullName()) // prints "John Smith"
```

如您所见，扩展函数是向现有类添加新方法的好方法，而无需修改类本身。

## 结论

在本文中，我们了解了 Kotlin 中的扩展函数。我们已经了解了如何创建扩展函数，以及如何使用它们向现有类添加新方法。