---
title: 058：Kotlin 中的数据类：使用自动方法简化对象声明
description: 
published: true
date: 2023-02-15T21:55:37.949Z
tags: 
editor: markdown
dateCreated: 2023-02-15T21:55:36.347Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [058: Data Classes in Kotlin: Simplifying Object Declaration with Automatic Methods***English** document is available*](/en/Knowledge-base/Kotlin/Learning/058-data-classes-in-kotlin-simplifying-object-declaration-with-automatic-methods)
{.links-list}


# Kotlin 中的数据类：使用自动方法简化对象声明

Kotlin 是一种 JVM 语言，旨在成为 Java 的更简洁实用的替代方案。它具有许多 Java 开发人员会发现熟悉的功能，以及一些可以使开发更快、更容易的新功能。

这些功能之一是数据类。在 Kotlin 中，数据类是旨在保存数据的类。数据类具有一些不同于常规类的特定功能：

- 它们不能是抽象的、开放的、封闭的或内在的。
- 除了在主构造函数中声明的属性外，它们不能有任何属性。
- 他们可以有一个主构造函数，最多有 26 个参数。
- 所有主构造函数参数必须标记为 val 或 var。
- 数据类不能是通用的。

数据类很有用，因为它们会自动为您生成许多方法。这些方法包括：

- ```toString()```：返回对象的字符串表示形式。
- ```equals()```：比较此对象与指定对象的相等性。
- ```hashCode()```：返回对象的哈希码值。
- ```copy()```：创建对象的副本。

此外，数据类还可以为类中的每个属性生成一个```componentN()``` 函数。此函数可用于以更简洁的方式访问数据类的属性。

要创建数据类，您可以使用 ```data``` 关键字：

```kotlin
data class User(val id: Long, val name: String, val email: String)
```

这将创建一个具有三个属性的数据类：```id```、```name``` 和```email```。请注意，所有属性都标记为“val”，这意味着它们是不可变的。您还可以将属性标记为 ```var```，这意味着它们是可变的。

创建数据类后，您可以使用通常的语法创建该类的对象：

```kotlin
val user = User(1, "John", "john@example.com")
```

然后，您可以使用生成的 ```componentN()``` 函数访问对象的属性：

```kotlin
println(user.id) // 1
println(user.name) // John
println(user.email) // john@example.com
```

您还可以使用生成的```toString()```、```equals()``` 和```hashCode()``` 函数：

```kotlin
println(user.toString()) // User(id=1, name=John, email=john@example.com)

val anotherUser = User(1, "John", "john@example.com")
println(user == anotherUser) // true

val yetAnotherUser = User(2, "John", "john@example.com")
println(user == yetAnotherUser) // false

println(user.hashCode()) // 367910362
println(anotherUser.hashCode()) // 367910362
println(yetAnotherUser.hashCode()) // 367586981
```

最后，您可以使用 ```copy()``` 函数创建一个对象的副本，其中的部分或全部属性已更改：

```kotlin
val user2 = user.copy(id = 2)
println(user2.id) // 2
println(user2.name) // John
println(user2.email) // john@example.com

val user3 = user.copy(name = "Jane")
println(user3.id) // 1
println(user3.name) // Jane
println(user3.email) // john@example.com

val user4 = user.copy(id = 2, name = "Jane", email = "jane@example.com")
println(user4.id) // 2
println(user4.name) // Jane
println(user4.email) // jane@example.com
```

如您所见，数据类是在 Kotlin 中创建和使用对象的一种非常方便的方式。它们不仅使您免于编写大量样板代码，而且还免费提供了许多有用的方法。