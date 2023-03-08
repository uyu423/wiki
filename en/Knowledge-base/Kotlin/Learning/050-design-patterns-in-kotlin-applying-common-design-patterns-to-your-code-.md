---
title: 050: Design Patterns in Kotlin: Applying Common Design Patterns to Your Code.
description: 
published: true
date: 2023-02-16T16:32:56.923Z
tags: 
editor: markdown
dateCreated: 2023-02-16T16:32:48.684Z
---

- [050: Patrones de diseño en Kotlin: aplicación de patrones de diseño comunes a su código.***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/050-design-patterns-in-kotlin-applying-common-design-patterns-to-your-code-)
{.links-list}
- [050：Kotlin 中的设计模式：将通用设计模式应用于您的代码。***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/050-design-patterns-in-kotlin-applying-common-design-patterns-to-your-code-)
{.links-list}
- [050: Kotlin의 디자인 패턴: 일반적인 디자인 패턴을 코드에 적용***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/050-design-patterns-in-kotlin-applying-common-design-patterns-to-your-code-)
{.links-list}


#050: Design Patterns in Kotlin: Applying Common Design Patterns to Your Code

Design patterns are a crucial part of any software developer's toolkit. They provide a common language that developers can use to communicate about solutions to common problems. Design patterns also help to make code more readable and maintainable.

Kotlin is a modern programming language that is growing in popularity. It is a great language for applying design patterns. In this post, we will take a look at some of the most common design patterns and how to apply them in Kotlin.

##Creational Patterns

Creational patterns are concerned with the creation of objects. These patterns help to control the process of object creation.

###Factory Pattern

The factory pattern is a creational pattern that is used to create objects. The factory pattern is useful when you need to create objects that are of the same type but with different data.

To create a factory pattern in Kotlin, we need to create a class that will act as our factory. This class will have a method that will create objects of the type that we specify.

```kotlin
class ObjectFactory {

 fun createObject(type: String): Any {

when (type) {
 "A" -> return ObjectA()
 "B" -> return ObjectB()
 else -> throw IllegalArgumentException("Unknown type")
}
}
}
```

We can then use our factory to create objects of the types that we need.

```kotlin
val factory = ObjectFactory()

val objectA = factory.createObject("A")
val objectB = factory.createObject("B")
```

The factory pattern is a great way to control the creation of objects. It is also a good way to keep your code DRY (Don't Repeat Yourself).

##Structural Patterns

Structural patterns are concerned with the structure of objects and how they are composed. These patterns help us to better understand the relationships between objects.

###Adapter Pattern

The adapter pattern is a structural pattern that is used to adapt one interface to another. The adapter pattern is useful when you need to use an existing class but its interface does not match the interface that you need.

To create an adapter pattern in Kotlin, we need to create a class that will act as our adapter. This class will implement the interface that we need and delegate calls to the existing class.

```kotlin
class Adapter(val existingClass: ExistingClass) : InterfaceX {

override fun method1() {
 existingClass.method1()
}

override fun method2() {
 existingClass.method2()
}
}
```

We can then use our adapter to access the methods of the existing class.

```kotlin
val adapter = Adapter(existingClass)

adapter.method1()
adapter.method2()
```

The adapter pattern is a great way to reuse existing code. It is also a good way to make code more readable and maintainable.

##Behavioral Patterns

Behavioral patterns are concerned with the behavior of objects. These patterns help us to better understand the behavior of objects and how they interact with each other.

###Observer Pattern

The observer pattern is a behavioral pattern that is used to define a one-to-many relationship between objects. The observer pattern is useful when you need to notify multiple objects about changes to a particular object.

To create an observer pattern in Kotlin, we need to create a class that will act as our subject. This class will have a method to register observers and a method to notify observers of changes.

```kotlin
class Subject {

private val observers = mutableListOf<Observer>()

fun registerObserver(observer: Observer) {
 observers.add(observer)
}

fun notifyObservers() {
 for (observer in observers) {
  observer.update()
 }
}
}
```

We can then use our subject to notify observers of changes.

```kotlin
val subject = Subject()

val observer1 = Observer1()
val observer2 = Observer2()

subject.registerObserver(observer1)
subject.registerObserver(observer2)

subject.notifyObservers()
```

The observer pattern is a great way to decouple objects. It is also a good way to make code more readable and maintainable.

##Conclusion

Design patterns are a crucial part of any software developer's toolkit. They provide a common language that developers can use to communicate about solutions to common problems. Design patterns also help to make code more readable and maintainable.

Kotlin is a great language for applying design patterns. In this post, we have looked at some of the most common design patterns and how to apply them in Kotlin.