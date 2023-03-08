---
title: 050：Kotlin 中的设计模式：将通用设计模式应用于您的代码。
description: 
published: true
date: 2023-02-16T16:32:50.588Z
tags: 
editor: markdown
dateCreated: 2023-02-16T16:32:48.679Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [050: Design Patterns in Kotlin: Applying Common Design Patterns to Your Code.***English** document is available*](/en/Knowledge-base/Kotlin/Learning/050-design-patterns-in-kotlin-applying-common-design-patterns-to-your-code-)
{.links-list}


# 050：Kotlin 中的设计模式：将通用设计模式应用于您的代码

设计模式是任何软件开发人员工具包的重要组成部分。它们提供了一种通用语言，开发人员可以使用该语言就常见问题的解决方案进行交流。设计模式还有助于使代码更具可读性和可维护性。

Kotlin 是一种越来越受欢迎的现代编程语言。它是应用设计模式的绝佳语言。在这篇文章中，我们将了解一些最常见的设计模式以及如何在 Kotlin 中应用它们。

## 创作模式

创建型模式与对象的创建有关。这些模式有助于控制对象创建的过程。

### 工厂模式

工厂模式是一种用于创建对象的创建模式。当您需要创建类型相同但数据不同的对象时，工厂模式很有用。

要在 Kotlin 中创建工厂模式，我们需要创建一个类作为我们的工厂。这个类将有一个方法来创建我们指定类型的对象。

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

然后我们可以使用我们的工厂来创建我们需要的类型的对象。

```kotlin
val factory = ObjectFactory()

val objectA = factory.createObject("A")
val objectB = factory.createObject("B")
```

工厂模式是控制对象创建的好方法。这也是保持代码干燥（不要重复自己）的好方法。

## 结构模式

结构模式与对象的结构及其组成方式有关。这些模式帮助我们更好地理解对象之间的关系。

### 适配器模式

适配器模式是一种结构模式，用于将一个接口适配到另一个接口。当您需要使用现有类但其接口与您需要的接口不匹配时，适配器模式很有用。

要在 Kotlin 中创建适配器模式，我们需要创建一个类来充当我们的适配器。该类将实现我们需要的接口并将调用委托给现有类。

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

然后我们可以使用我们的适配器来访问现有类的方法。

```kotlin
val adapter = Adapter(existingClass)

adapter.method1()
adapter.method2()
```

适配器模式是重用现有代码的好方法。这也是使代码更具可读性和可维护性的好方法。

## 行为模式

行为模式与对象的行为有关。这些模式帮助我们更好地理解对象的行为以及它们如何相互作用。

### 观察者模式

观察者模式是一种行为模式，用于定义对象之间的一对多关系。当您需要将特定对象的更改通知多个对象时，观察者模式很有用。

要在 Kotlin 中创建观察者模式，我们需要创建一个类作为我们的主题。这个类将有一个注册观察者的方法和一个通知观察者变化的方法。

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

然后我们可以使用我们的主题来通知观察者变化。

```kotlin
val subject = Subject()

val observer1 = Observer1()
val observer2 = Observer2()

subject.registerObserver(observer1)
subject.registerObserver(observer2)

subject.notifyObservers()
```

观察者模式是解耦对象的好方法。这也是使代码更具可读性和可维护性的好方法。

## 结论

设计模式是任何软件开发人员工具包的重要组成部分。它们提供了一种通用语言，开发人员可以使用该语言就常见问题的解决方案进行交流。设计模式还有助于使代码更具可读性和可维护性。

Kotlin 是一种用于应用设计模式的出色语言。在这篇文章中，我们研究了一些最常见的设计模式以及如何在 Kotlin 中应用它们。