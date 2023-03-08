---
title: 038：Kotlin 中的具体类型：在运行时访问类型
description: 
published: true
date: 2023-02-02T01:57:39.013Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:57:37.398Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [038: Reified Types in Kotlin: Accessing Types at Runtime***English** document is available*](/en/Knowledge-base/Kotlin/Learning/038-reified-types-in-kotlin-accessing-types-at-runtime)
{.links-list}


# 介绍

Kotlin 是一种运行在 JVM 上的静态类型语言。它与 Java 具有出色的互操作性，是开发 Android 应用程序的绝佳选择。

Kotlin 最强大的功能之一是它对具体化类型的支持。这允许您在运行时访问类型，这在 Java 中是不可能的。

在本文中，我们将了解什么是具体化类型以及如何在 Kotlin 中使用它们。我们还将看到一些示例，说明如何使用具体化类型来简化开发。

# 什么是具体化类型？

具体化类型是可以在运行时访问的类型。这在 Java 中是不可能的，其中类型仅在编译时可用。

具体化类型对于处理反射非常有用。反射是一种在运行时动态访问类及其成员的方法。它经常用于框架和库中。

在 Kotlin 中，具体化类型是使用关键字“具体化”声明的。例如，我们可以像这样声明一个具体化的类型：

```kotlin
reified val myType: String = "Hello, world!"
```

现在我们可以在运行时访问 myType 的类型：

```kotlin
val type = myType::class
```

`type` 变量将包含 `String` 类。

我们还可以访问泛型的类型：

```kotlin
reified val myList: List<String> = listOf("Hello", "world!")

val type = myList::class
```

`type` 变量将包含 `List` 类。

# 如何使用具体化的类型？

具体化的类型可以以多种方式使用。我们将看看一些最常见的用例。

## 使用反射

正如我们所见，具体化类型对于处理反射非常有用。反射是一种在运行时动态访问类及其成员的方法。

在 Java 中，反射通常用于框架和库中。例如，Spring 框架使用反射来动态创建对象。

在 Kotlin 中，我们可以使用反射来访问类的成员：

```kotlin
reified val myClass: MyClass = MyClass()

val members = myClass::class.members
```

`members` 变量将包含 `MyClass` 类的所有成员的列表。

我们还可以使用反射来访问类的注解：

```kotlin
reified val myClass: MyClass = MyClass()

val annotations = myClass::class.annotations
```

`annotations` 变量将包含 `MyClass` 类的所有注释的列表。

## 使用泛型类型

具体化类型对于处理泛型类型也非常有用。在 Java 中，不可能在运行时访问泛型类型。这会使使用泛型类型变得困难。

在 Kotlin 中，我们可以使用具体化类型来访问泛型类型：

```kotlin
reified val myList: List<String> = listOf("Hello", "world!")

val type = myList::class
```

`type` 变量将包含 `List` 类。

我们还可以使用具体化类型来创建泛型类型：

```kotlin
inline fun <reified T> createList(): List<T> {
    return listOf()
}

val myList = createList<String>()
```

`myList` 变量将包含一个空的 `List<String>`。

## 使用 Kotlin 反射

Kotlin 反射是一种在运行时动态访问 Kotlin 类及其成员的方法。它与 Java 反射非常相似，但更易于使用。

在 Kotlin 中，我们可以使用具体化类型来访问类的成员：

```kotlin
reified val myClass: MyClass = MyClass()

val members = myClass::class.members
```

`members` 变量将包含 `MyClass` 类的所有成员的列表。

我们还可以使用具体化类型来访问类的注解：

```kotlin
reified val myClass: MyClass = MyClass()

val annotations = myClass::class.annotations
```

`annotations` 变量将包含 `MyClass` 类的所有注释的列表。

# 结论

在本文中，我们了解了具体化类型是什么以及如何在 Kotlin 中使用它们。我们还看到了一些如何使用具体化类型来简化开发的示例。

具体化类型是 Kotlin 的一项强大功能，可以通过多种方式使用。如果您使用的是反射类型或泛型类型，具体化类型可能会有很大帮助。