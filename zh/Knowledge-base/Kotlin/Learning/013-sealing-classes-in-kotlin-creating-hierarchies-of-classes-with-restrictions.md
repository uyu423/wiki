---
title: 013：Kotlin 中的密封类：创建有限制的类层次结构
description: 
published: true
date: 2023-01-31T05:43:40.103Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:43:37.795Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [013: Sealing Classes in Kotlin: Creating Hierarchies of Classes with Restrictions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/013-sealing-classes-in-kotlin-creating-hierarchies-of-classes-with-restrictions)
{.links-list}


随着 Kotlin 越来越受欢迎，越来越多的开发人员正在寻找在他们的项目中使用它的方法。 Kotlin 的一个关键特性是它能够密封类，这允许创建有限制的类层次结构。

在本文中，我们将了解什么是密封类以及如何在 Kotlin 项目中使用它。我们还将查看一些代码示例，以了解密封类在实践中是如何工作的。

什么是密封类？

密封类是一种创建具有限制的类层次结构的方法。密封类只能由在同一文件中声明的类进行子类化。这允许更好地控制类层次结构的设计，并可以产生更健壮和可靠的代码。

为什么要使用密封类？

您可能希望在 Kotlin 代码中使用密封类的原因有多种：

* 您可以使用密封类来创建访问受限的类层次结构。这对于创建 API 库很有用，您只希望某些类可供开发人员访问。

* 密封类可以让你的代码更加健壮和可靠。通过限制类的子类化方式，您可以避免代码中的意外行为和错误。

* 密封类可以让你的代码更加简洁。通过密封一个类，可以避免在多个子类中重复代码。

我如何使用密封类？

要在 Kotlin 代码中使用密封类，您需要做两件事：

1. 使用关键字“sealed”声明密封类：

```kotlin
sealed class Shape {
}
```

2. 在与密封类相同的文件中声明您的子类：

```kotlin
class Circle: Shape() {
}
```

您还可以使用参数声明密封类：

```kotlin
sealed class Shape(val name: String) {
}

class Circle: Shape("circle") {
}
```

如果你试图在不同的文件中声明一个密封类的子类，你会得到一个错误：

```kotlin
// Error: Cannot subclass sealed class Shape

class Square: Shape() {
}
```

您可以通过使用伴随对象来解决这个问题：

```kotlin
class Square: Shape() {
    companion object : Shape() {
    }
}
```

另一种使用密封类的方法是将它们声明为抽象类：

```kotlin
abstract sealed class Shape {
}

class Circle: Shape() {
}

class Square: Shape() {
}
```

这允许您在密封类中定义抽象方法，这些方法必须在子类中实现：

```kotlin
abstract sealed class Shape {
    abstract fun getArea(): Double
}

class Circle(val radius: Double): Shape() {
    override fun getArea(): Double {
        return Math.PI * radius * radius
    }
}

class Square(val side: Double): Shape() {
    override fun getArea(): Double {
        return side * side
    }
}
```

您还可以使用密封类来创建枚举：

```kotlin
sealed class Shape {
    class Circle(val radius: Double): Shape()
    class Square(val side: Double): Shape()
}

fun getArea(shape: Shape): Double {
    return when(shape) {
        is Shape.Circle -> Math.PI * shape.radius * shape.radius
        is Shape.Square -> shape.side * shape.side
    }
}
```

这允许您创建具有任意数据的枚举：

```kotlin
enum class Shape(val name: String) {
    CIRCLE("circle"),
    SQUARE("square")
}
```

您还可以使用密封类来创建密封对象：

```kotlin
sealed class Shape {
    object Circle: Shape()
    object Square: Shape()
}

fun getArea(shape: Shape): Double {
    return when(shape) {
        is Shape.Circle -> Math.PI * 1.0 * 1.0
        is Shape.Square -> 1.0 * 1.0
    }
}
```

密封对象是一种单例，这意味着该对象在内存中只能有一个实例。这对于创建缓存或线程池之类的东西很有用。

如果您尝试创建密封对象的第二个实例，您将收到错误消息：

```kotlin
// Error: Object 'Shape.Circle' has already been created

val circle = Shape.Circle
```

您可以在 Kotlin 文档中找到有关密封类的更多信息：

https://kotlinlang.org/docs/reference/sealed-classes.html

您可以在 Kotlin 文档中找到有关单例的更多信息：

https://kotlinlang.org/docs/reference/object-declarations.html#object-declarations

总之，密封类是一种创建具有限制的类层次结构的方法。密封类对于创建 API 库非常有用，您只希望开发人员可以访问某些类。密封类还可以使您的代码更加健壮和可靠。