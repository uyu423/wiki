---
title: 013: Sealing Classes in Kotlin: Creating Hierarchies of Classes with Restrictions
description: 
published: true
date: 2023-01-31T05:43:40.409Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:43:37.794Z
---

- [013: Kotlin에서 클래스 봉인: 제한이 있는 클래스의 계층 구조 만들기***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/013-sealing-classes-in-kotlin-creating-hierarchies-of-classes-with-restrictions)
{.links-list}
- [013: Kotlin でクラスを封印する: 制限付きのクラスの階層を作成する***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/013-sealing-classes-in-kotlin-creating-hierarchies-of-classes-with-restrictions)
{.links-list}
- [013：Kotlin 中的密封类：创建有限制的类层次结构***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/013-sealing-classes-in-kotlin-creating-hierarchies-of-classes-with-restrictions)
{.links-list}


As Kotlin continues to grow in popularity, more and more developers are looking for ways to use it in their projects. One of the key features of Kotlin is its ability to seal classes, which allows for the creation of hierarchies of classes with restrictions.

In this article, we'll take a look at what sealing classes is and how it can be used in Kotlin projects. We'll also look at some code examples to see how sealing classes works in practice.

What are sealing classes?

Sealing classes are a way of creating hierarchies of classes with restrictions. A sealed class can only be subclassed by classes that are declared in the same file. This allows for greater control over the design of a class hierarchy, and can lead to more robust and reliable code.

Why use sealing classes?

There are several reasons why you might want to use sealing classes in your Kotlin code:

* You can use sealing classes to create a hierarchy of classes with restricted access. This can be useful for creating API libraries, where you only want certain classes to be accessible to developers.

* Sealing classes can make your code more robust and reliable. By restricting the way a class can be subclassed, you can avoid unexpected behaviour and errors in your code.

* Sealing classes can make your code more concise. By sealing a class, you can avoid repeating code in multiple subclasses.

How do I use sealing classes?

To use sealing classes in your Kotlin code, you need to do two things:

1. Declare your sealed class using the keyword "sealed":

```kotlin
sealed class Shape {
}
```

2. Declare your subclass in the same file as the sealed class:

```kotlin
class Circle: Shape() {
}
```

You can also declare sealed classes with parameters:

```kotlin
sealed class Shape(val name: String) {
}

class Circle: Shape("circle") {
}
```

If you try to declare a subclass of a sealed class in a different file, you'll get an error:

```kotlin
// Error: Cannot subclass sealed class Shape

class Square: Shape() {
}
```

You can get around this by using a companion object:

```kotlin
class Square: Shape() {
    companion object : Shape() {
    }
}
```

Another way to use sealing classes is to declare them as abstract:

```kotlin
abstract sealed class Shape {
}

class Circle: Shape() {
}

class Square: Shape() {
}
```

This allows you to define abstract methods in your sealed class, which must be implemented in subclasses:

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

You can also use sealed classes to create enums:

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

This allows you to create an enum with arbitrary data:

```kotlin
enum class Shape(val name: String) {
    CIRCLE("circle"),
    SQUARE("square")
}
```

You can also use sealed classes to create sealed objects:

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

Sealed objects are a type of singleton, which means there can only be one instance of the object in memory. This can be useful for creating things like caches or thread pools.

If you try to create a second instance of a sealed object, you'll get an error:

```kotlin
// Error: Object 'Shape.Circle' has already been created

val circle = Shape.Circle
```

You can find more information about sealed classes in the Kotlin documentation:

https://kotlinlang.org/docs/reference/sealed-classes.html

And you can find more information about singletons in the Kotlin documentation:

https://kotlinlang.org/docs/reference/object-declarations.html#object-declarations

In summary, sealing classes is a way of creating hierarchies of classes with restrictions. Sealing classes can be useful for creating API libraries, where you only want certain classes to be accessible to developers. Sealing classes can also make your code more robust and reliable.