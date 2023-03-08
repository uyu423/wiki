---
title: 061: The Factory Method Pattern in Kotlin: Creating Objects with a Factory Method
description: 
published: true
date: 2023-01-31T09:05:00.841Z
tags: 
editor: markdown
dateCreated: 2023-01-31T09:04:57.086Z
---

- [061: Kotlin의 팩토리 메소드 패턴: 팩토리 메소드로 객체 생성***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/061-the-factory-method-pattern-in-kotlin-creating-objects-with-a-factory-method)
{.links-list}
- [061: Kotlin のファクトリー メソッド パターン: ファクトリー メソッドでオブジェクトを作成する***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/061-the-factory-method-pattern-in-kotlin-creating-objects-with-a-factory-method)
{.links-list}
- [061：Kotlin 中的工厂方法模式：使用工厂方法创建对象***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/061-the-factory-method-pattern-in-kotlin-creating-objects-with-a-factory-method)
{.links-list}




# 061: The Factory Method Pattern in Kotlin: Creating Objects with a Factory Method

In software development, the Factory Method Pattern is a creational design pattern that uses factory methods to deal with the problem of creating objects without having to specify the exact class of object that will be created. This is done by creating objects via a factory method instead of by calling a constructor.

In this article we will be discussing the Factory Method Pattern and how it can be used in Kotlin to create objects. We will also look at some code examples to demonstrate how this pattern can be used in practice.

## What is the Factory Method Pattern?

The Factory Method Pattern is a creational design pattern that uses factory methods to deal with the problem of creating objects without having to specify the exact class of object that will be created. This is done by creating objects via a factory method instead of by calling a constructor.

The Factory Method Pattern is also known as the Virtual Constructor Pattern and the Factory Pattern. It is used to abstract away the details of object creation and allow for new objects to be created without the need to hard-code their class names.

## How Does the Factory Method Pattern Work?

The Factory Method Pattern relies on inheritance to work. It defines an interface or abstract class for creating objects, and concrete subclasses that implement the interface or inherit from the abstract class to actually create objects.

The client code that uses the objects created by the Factory Method Pattern does not need to know or care about the concrete classes that are used to create objects, it only needs to know the interface or abstract class.

## When to Use the Factory Method Pattern

The Factory Method Pattern can be used in the following situations:

- When the object to be created is not known ahead of time
- When the object to be created needs to be created in a different part of the code from where it will be used
- When the object to be created needs to be created from data that is not known until run-time

## The Benefits of the Factory Method Pattern

The Factory Method Pattern has the following benefits:

- It allows for the creation of objects without having to hard-code their class names
- It allows for the creation of objects in a different part of the code from where they will be used
- It allows for the creation of objects from data that is not known until run-time

## The Drawbacks of the Factory Method Pattern

The Factory Method Pattern has the following drawbacks:

- It can make the code harder to read and understand
- It can make the code harder to debug
- It can lead to a lot of code duplication

## Kotlin Implementation

Kotlin does not have a built-in support for the Factory Method Pattern, but it is possible to implement it in Kotlin.

One way to implement the Factory Method Pattern in Kotlin is to use acompanion object. A companion object is an object that is associated with a class. A class can have only one companion object and vice versa.

A companion object can be used to implement the Factory Method Pattern as follows:

```kotlin
interface Shape {
    fun draw()
}

class Circle : Shape {
    override fun draw() {
        println("Circle.draw()")
    }
}

class Rectangle : Shape {
    override fun draw() {
        println("Rectangle.draw()")
    }
}

class Triangle : Shape {
    override fun draw() {
        println("Triangle.draw()")
    }
}

object ShapeFactory {
    fun getShape(shapeType: String): Shape? {
        if (shapeType == null) {
            return null
        }
        if (shapeType.equals("CIRCLE", ignoreCase = true)) {
            return Circle()
        } else if (shapeType.equals("RECTANGLE", ignoreCase = true)) {
            return Rectangle()
        } else if (shapeType.equals("TRIANGLE", ignoreCase = true)) {
            return Triangle()
        }
        return null
    }
}
```

In the code above, we have defined an interface Shape and three concrete classes that implement the Shape interface. We have also defined a companion object ShapeFactory that contains a factory method getShape(). This factory method takes a string parameter shapeType and returns an object of type Shape.

We can use the ShapeFactory companion object as follows:

```kotlin
val circle = ShapeFactory.getShape("CIRCLE")
circle?.draw()

val rectangle = ShapeFactory.getShape("RECTANGLE")
rectangle?.draw()

val triangle = ShapeFactory.getShape("TRIANGLE")
triangle?.draw()
```

In the code above, we have used the ShapeFactory companion object to create three objects, one of each type. We have then invoked the draw() method on each object to display its type.

Alternatively, we can use an object declaration to implement the Factory Method Pattern as follows:

```kotlin
interface Shape {
    fun draw()
}

class Circle : Shape {
    override fun draw() {
        println("Circle.draw()")
    }
}

class Rectangle : Shape {
    override fun draw() {
        println("Rectangle.draw()")
    }
}

class Triangle : Shape {
    override fun draw() {
        println("Triangle.draw()")
    }
}

object ShapeFactory {
    fun getShape(shapeType: String): Shape? {
        if (shapeType == null) {
            return null
        }
        if (shapeType.equals("CIRCLE", ignoreCase = true)) {
            return Circle()
        } else if (shapeType.equals("RECTANGLE", ignoreCase = true)) {
            return Rectangle()
        } else if (shapeType.equals("TRIANGLE", ignoreCase = true)) {
            return Triangle()
        }
        return null
    }
}

fun main(args: Array<String>) {
    val circle = ShapeFactory.getShape("CIRCLE")
    circle?.draw()

    val rectangle = ShapeFactory.getShape("RECTANGLE")
    rectangle?.draw()

    val triangle = ShapeFactory.getShape("TRIANGLE")
    triangle?.draw()
}
```

In the code above, we have defined an object declaration ShapeFactory that contains a factory method getShape(). This factory method takes a string parameter shapeType and returns an object of type Shape.

We can use the ShapeFactory object as follows:

```kotlin
val circle = ShapeFactory.getShape("CIRCLE")
circle?.draw()

val rectangle = ShapeFactory.getShape("RECTANGLE")
rectangle?.draw()

val triangle = ShapeFactory.getShape("TRIANGLE")
triangle?.draw()
```

In the code above, we have used the ShapeFactory object to create three objects, one of each type. We have then invoked the draw() method on each object to display its type.

## Comparison with the Abstract Factory Pattern

The Abstract Factory Pattern is similar to the Factory Method Pattern, but it has a different purpose. The Abstract Factory Pattern is used to create families of related or dependent objects, while the Factory Method Pattern is used to create individual objects. 

The Abstract Factory Pattern is also more complex than the Factory Method Pattern. The Abstract Factory Pattern requires the existence of one or more concrete factories, while the Factory Method Pattern only requires a single concrete factory.

## Conclusion

In this article we have discussed the Factory Method Pattern and how it can be used in Kotlin to create objects. We have also looked at some code examples to demonstrate how this pattern can be used in practice.