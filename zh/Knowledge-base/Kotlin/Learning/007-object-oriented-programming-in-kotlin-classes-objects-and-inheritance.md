---
title: 007：Kotlin 中的面向对象编程：类、对象和继承
description: 
published: true
date: 2023-01-31T05:10:52.038Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:10:50.470Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [007: Object-Oriented Programming in Kotlin: Classes, Objects, and Inheritance***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/007-object-oriented-programming-in-kotlin-classes-objects-and-inheritance)
{.links-list}




Kotlin 是一种运行在 JVM 上的静态类型编程语言，也可以编译成 JavaScript。 Kotlin 旨在与 Java 互操作，因此是开发 Android 应用程序的绝佳选择。

面向对象编程是一种基于对象概念的编程范式，对象是包含数据和方法的数据结构。 Kotlin 是一种面向对象的语言，因此支持类、对象和继承。

## 类、对象和继承

在 Kotlin 中，类是用于创建对象的模板。类可以包含属性和方法，也称为成员。属性是与类关联的一段数据，方法是可以在对象上调用的函数。

为了在 Kotlin 中创建一个类，使用关键字“class”，后跟类名。例如，以下代码创建了一个名为“Person”的类：

```kotlin
class Person {

}
```

类可以包含属性和方法，也称为成员。属性是与类关联的一段数据，方法是可以在对象上调用的函数。

为了向类添加属性，使用“var”或“val”关键字，后跟属性名称及其类型。例如，以下代码创建一个名为“name”的“String”类型的属性：

```kotlin
class Person {
    var name: String
}
```

为了向类中添加方法，使用“fun”关键字，后跟方法名称及其参数。例如，以下代码创建了一个名为“greet”的方法，该方法采用“String”类型的“name”参数：

```kotlin
class Person {
    fun greet(name: String) {
        println("Hello, $name!")
    }
}
```

为了从一个类创建一个对象，使用了 `new` 关键字，后面跟着类的名称。例如，以下代码从 `Person` 类创建一个对象：

```kotlin
val person = Person()
```

为了在对象上调用方法，使用“.”运算符，后跟方法名称及其参数。例如，以下代码调用 person 对象的 greet 方法，传入要问候的人的 name ：

```kotlin
person.greet("John")
```

## 继承

继承是一种机制，一个类可以从另一个类派生。从中派生的类称为超类，进行派生的类称为子类。

在 Kotlin 中，可以使用“:”运算符定义子类，后跟超类的名称。例如，下面的代码定义了一个继承自 Person 类的 Student 类：

```kotlin
class Student: Person {

}
```

子类继承其超类的所有属性和方法，也可以定义自己的属性和方法。

例如，“Student”类可以定义自己的“enroll”方法，并覆盖“Person”类的“greet”方法，如下代码所示：

```kotlin
class Student: Person {
    fun enroll() {
        // enroll student in class
    }

    override fun greet(name: String) {
        println("Hello, $name! I'm a student.")
    }
}
```

## 结论

Kotlin 是一种静态类型的面向对象的编程语言，它提供对类、对象和继承的支持。 Kotlin 旨在与 Java 互操作，因此是开发 Android 应用程序的绝佳选择。