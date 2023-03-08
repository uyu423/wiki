---
title: 007: Object-Oriented Programming in Kotlin: Classes, Objects, and Inheritance
description: 
published: true
date: 2023-01-31T05:10:53.892Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:10:50.473Z
---

- [007: Kotlin의 객체 지향 프로그래밍: 클래스, 객체 및 상속***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/007-object-oriented-programming-in-kotlin-classes-objects-and-inheritance)
{.links-list}
- [007: Kotlin でのオブジェクト指向プログラミング: クラス、オブジェクト、および継承***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/007-object-oriented-programming-in-kotlin-classes-objects-and-inheritance)
{.links-list}
- [007：Kotlin 中的面向对象编程：类、对象和继承***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/007-object-oriented-programming-in-kotlin-classes-objects-and-inheritance)
{.links-list}




Kotlin is a statically typed programming language that runs on the JVM, and can also be compiled to JavaScript. Kotlin is designed to be interoperable with Java, and is therefore a great choice for developing Android applications. 

Object-oriented programming is a programming paradigm that is based on the concept of objects, which are data structures that contain both data and methods. Kotlin is an object-oriented language, and therefore offers support for classes, objects, and inheritance. 

## Classes, Objects, and Inheritance

In Kotlin, a class is a template for creating objects. A class can contain properties and methods, which are also known as members. A property is a piece of data associated with a class, and a method is a function that can be invoked on an object. 

In order to create a class in Kotlin, the keyword `class` is used, followed by the name of the class. For example, the following code creates a class named `Person`:

```kotlin
class Person {

}
```

A class can contain properties and methods, which are also known as members. A property is a piece of data associated with a class, and a method is a function that can be invoked on an object. 

In order to add a property to a class, the `var` or `val` keyword is used, followed by the name of the property and its type. For example, the following code creates a property named `name` of type `String`:

```kotlin
class Person {
    var name: String
}
```

In order to add a method to a class, the `fun` keyword is used, followed by the name of the method and its parameters. For example, the following code creates a method named `greet` that takes a `name` parameter of type `String`:

```kotlin
class Person {
    fun greet(name: String) {
        println("Hello, $name!")
    }
}
```

In order to create an object from a class, the `new` keyword is used, followed by the name of the class. For example, the following code creates an object from the `Person` class:

```kotlin
val person = Person()
```

In order to invoke a method on an object, the `.` operator is used, followed by the name of the method and its parameters. For example, the following code invokes the `greet` method on the `person` object, passing in the `name` of the person to greet:

```kotlin
person.greet("John")
```

## Inheritance

Inheritance is a mechanism whereby one class can be derived from another. The class that is being derived from is known as the superclass, and the class that is doing the deriving is known as the subclass. 

In Kotlin, a subclass can be defined using the `:` operator, followed by the name of the superclass. For example, the following code defines a `Student` class that inherits from the `Person` class:

```kotlin
class Student: Person {

}
```

A subclass inherits all of the properties and methods of its superclass, and can also define its own properties and methods. 

For example, the `Student` class could define its own `enroll` method, as well as override the `greet` method of the `Person` class, as shown in the following code:

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

## Conclusion

Kotlin is a statically typed object-oriented programming language that offers support for classes, objects, and inheritance. Kotlin is designed to be interoperable with Java, and is therefore a great choice for developing Android applications.