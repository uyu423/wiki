---
title: 042：Kotlin 中的密封类：限制类层次结构
description: 
published: true
date: 2023-01-31T10:36:17.267Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:36:15.748Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [042: Sealed Classes in Kotlin: Restricting Class Hierarchies***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/042-sealed-classes-in-kotlin-restricting-class-hierarchies)
{.links-list}



# 042：Kotlin 中的密封类：限制类层次结构

密封类是 Kotlin 中用于限制类层次结构的强大工具。通过密封一个类，我们可以防止它被任何其他类扩展。这在很多情况下都很有用，例如，当我们想限制一个类只能由同一文件中的类扩展时。

密封类使用 sealed 关键字声明：

```kotlin
sealed class MySealedClass
```

一旦一个类被密封，它就不能被任何其他类扩展，除了那些在与密封类相同的文件中声明的类。例如，下面的代码将不会编译：

```kotlin
// MySealedClass.kt

sealed class MySealedClass

class MySubclass : MySealedClass() // Will not compile
```

为了扩展密封类，子类必须在与密封类相同的文件中声明。这被称为*本地密封类*

```kotlin
// MySealedClass.kt

sealed class MySealedClass

class MySubclass : MySealedClass() // Compiles
```

密封类也可以*嵌套*在其他类或对象中。在这种情况下，密封类只能由在同一父类或对象*内部*声明的类扩展。例如：

```kotlin
// MyOuterClass.kt

class MyOuterClass {

    sealed class MySealedClass

    class MySubclass : MySealedClass() // Compiles
}

class MyOtherSubclass : MyOuterClass.MySealedClass() // Will not compile
```

密封类是限制类层次结构的有用工具，可用于许多不同的情况。特别是，它们有助于确保一个类只能由同一文件中的类扩展。