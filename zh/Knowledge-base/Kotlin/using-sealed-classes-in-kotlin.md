---
title: 在 Kotlin 中使用密封类
description: 
published: true
date: 2023-02-15T10:55:47.964Z
tags: 
editor: markdown
dateCreated: 2023-02-15T10:55:40.095Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Using Sealed Classes in Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/using-sealed-classes-in-kotlin)
{.links-list}


# 在 Kotlin 中使用密封类

Kotlin 的密封类是限制类继承的好方法。通过密封一个类，您可以控制哪些其他类可以从它继承。出于多种原因，这可能很有用，包括防止意外继承和创建更多类型安全的代码。

密封类使用 `sealed` 关键字定义：

```kotlin
sealed class MySealedClass
```

密封类可以有子类，但这些子类必须在与密封类相同的文件中声明。这是为了防止从文件外部意外继承。例如，不允许以下内容：

```kotlin
// MySealedClass.kt

sealed class MySealedClass

// MySubclass.kt

class MySubclass: MySealedClass // Error: MySubclass is not a member of the sealed class
```

要解决此问题，您可以将 MySubclass 移动到与 MySealedClass 相同的文件中：

```kotlin
// MySealedClass.kt

sealed class MySealedClass

class MySubclass: MySealedClass // Ok
```

您还可以将密封类声明为“inner”：

```kotlin
class MyClass {
    sealed class MySealedClass
}
```

在这种情况下，子类必须在 MyClass 中声明：

```kotlin
class MyClass {
    sealed class MySealedClass

    class MySubclass: MySealedClass // Ok
}

class MySubclass: MyClass.MySealedClass // Error: MySubclass is not a member of MyClass
```

密封类对于创建类型安全的代码很有用。例如，考虑以下密封类层次结构：

```kotlin
sealed class Shape {
    class Circle(val radius: Double): Shape()
    class Rectangle(val width: Double, val height: Double): Shape()
}
```

您可以使用 when 表达式以类型安全的方式处理 `Shape` 的不同子类：

```kotlin
fun getArea(shape: Shape): Double = when(shape) {
    is Shape.Circle -> Math.PI * shape.radius * shape.radius
    is Shape.Rectangle -> shape.width * shape.height
}
```

在此示例中，编译器可以确定 `shape` 变量只能是 `Circle` 或 `Rectangle` 类型，因此不需要 `else` 分支。

密封类对于限制变量的类型也很有用。例如，考虑以下密封类层次结构：

```kotlin
sealed class Pet {
    class Dog: Pet()
    class Cat: Pet()
}
```

您可以使用密封类将变量的类型限制为特定的子类：

```kotlin
fun getPet(name: String): Pet? = when(name) {
    "Bob" -> Pet.Dog()
    "Mary" -> Pet.Cat()
    else -> null
}

val pet: Pet = getPet("Bob") // Ok
val pet: Pet = getPet("Mary") // Ok
val pet: Pet = getPet("John") // Error: Type mismatch: inferred type is Pet? but Pet was expected
```

在此示例中，如果“name”参数为“Bob”，则“getPet()”函数返回“Dog”；如果“name”参数为“Mary”，则“getPet()”函数返回“Cat”。如果“name”参数既不是“Bob”也不是“Mary”，则“getPet()”返回“null”。

`pet` 变量被声明为 `Pet` 类型，并被赋予 `getPet()` 的返回值。这是有效的，因为编译器知道 getPet() 的返回值只能是 Dog、Cat 或 null。如果 `getPet()` 可以返回 `Pet` 的任何子类，则赋值将无效。

## 参考

- [Kotlin 密封类](https://kotlinlang.org/docs/reference/sealed-classes.html)
- [Kotlin 中的密封类](https://medium.com/@BladeCoder/sealed-classes-in-kotlin-67861b4bfe7d)
- [密封类](https://antonioleiva.com/sealed-classes/)