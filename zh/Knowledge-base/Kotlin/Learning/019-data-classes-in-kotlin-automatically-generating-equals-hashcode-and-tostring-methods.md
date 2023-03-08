---
title: 019：Kotlin 中的数据类：自动生成 Equals、HashCode 和 ToString 方法
description: 
published: true
date: 2023-02-12T01:55:23.410Z
tags: 
editor: markdown
dateCreated: 2023-02-12T01:55:21.800Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [019: Data Classes in Kotlin: Automatically Generating Equals, HashCode, and ToString Methods***English** document is available*](/en/Knowledge-base/Kotlin/Learning/019-data-classes-in-kotlin-automatically-generating-equals-hashcode-and-tostring-methods)
{.links-list}


# Kotlin 中的数据类：自动生成 Equals、HashCode 和 ToString 方法

Kotlin 是一种在 Java 虚拟机上运行的静态类型编程语言。它是一种通用语言，旨在简洁、安全和可互操作。

使 Kotlin 脱颖而出的特性之一是它对数据类的支持。数据类是设计用来保存数据的类。在 Kotlin 中，数据类带有许多内置功能，包括自动生成 equals()、hashCode() 和 toString() 方法的能力。

在这篇文章中，我们将了解如何在 Kotlin 中使用数据类以及如何自动生成 equals()、hashCode() 和 toString() 方法。

## 创建数据类

要创建数据类，我们使用关键字数据：

```kotlin
data class User(val name: String, val age: Int)
```

这将创建一个具有两个属性的数据类：姓名和年龄。我们还可以创建具有可变属性的数据类：

```kotlin
data class User(var name: String, var age: Int)
```

数据类也可以有二级构造函数：

```kotlin
data class User(val name: String, val age: Int) {
    constructor(name: String) : this(name, 0)
}
```

## 生成 Equals 和 HashCode 方法

默认情况下，Kotlin 中的数据类会生成 equals() 和 hashCode() 方法。这些方法比较两个数据类中的数据，如果相等则返回真。

这是 equals() 方法如何工作的示例：

```kotlin
val user1 = User("John", 30)
val user2 = User("John", 30)

println(user1 == user2) // true
```

在此示例中，我们有两个具有相同名称和年龄属性的数据类。当我们使用 == 运算符比较它们时，会调用 equals() 方法并返回 true。

如果我们更改其中一个属性，equals() 方法将返回 false：

```kotlin
val user1 = User("John", 30)
val user2 = User("John", 31)

println(user1 == user2) // false
```

## 生成一个 toString() 方法

Kotlin 中的数据类也会生成一个 toString() 方法。此方法用于将数据类中的数据转换为字符串。

以下是 toString() 方法如何工作的示例：

```kotlin
val user = User("John", 30)

println(user.toString()) // User(name=John, age=30)
```

如您所见，toString() 方法以可读格式打印出数据类中的数据。

## 结论

在本文中，我们了解了 Kotlin 中的数据类以及如何自动生成 equals()、hashCode() 和 toString() 方法。数据类是创建简洁安全代码的好方法。