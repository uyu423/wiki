---
title: 019: Data Classes in Kotlin: Automatically Generating Equals, HashCode, and ToString Methods
description: 
published: true
date: 2023-02-12T01:55:28.638Z
tags: 
editor: markdown
dateCreated: 2023-02-12T01:55:21.806Z
---

- [019: Clases de datos en Kotlin: generación automática de métodos Equals, HashCode y ToString***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/019-data-classes-in-kotlin-automatically-generating-equals-hashcode-and-tostring-methods)
{.links-list}
- [019：Kotlin 中的数据类：自动生成 Equals、HashCode 和 ToString 方法***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/019-data-classes-in-kotlin-automatically-generating-equals-hashcode-and-tostring-methods)
{.links-list}
- [019: Kotlin의 데이터 클래스: Equals, HashCode 및 ToString 메서드 자동 생성***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/019-data-classes-in-kotlin-automatically-generating-equals-hashcode-and-tostring-methods)
{.links-list}


# Data Classes in Kotlin: Automatically Generating Equals, HashCode, and ToString Methods

Kotlin is a statically typed programming language that runs on the Java Virtual Machine. It is a general-purpose language that is designed to be concise, safe, and interoperable.

One of the features that makes Kotlin stand out is its support for data classes. A data class is a class that is designed to hold data. In Kotlin, data classes come with a lot of built-in functionality, including the ability to generate equals(), hashCode(), and toString() methods automatically.

In this post, we'll take a look at how to use data classes in Kotlin and how to automatically generate equals(), hashCode(), and toString() methods.

## Creating a Data Class

To create a data class, we use the keyword data:

```kotlin
data class User(val name: String, val age: Int)
```

This creates a data class with two properties: name and age. We can also create data classes with mutable properties:

```kotlin
data class User(var name: String, var age: Int)
```

Data classes can also have secondary constructors:

```kotlin
data class User(val name: String, val age: Int) {
    constructor(name: String) : this(name, 0)
}
```

## Generating Equals and HashCode Methods

By default, data classes in Kotlin generate equals() and hashCode() methods. These methods compare the data in two data classes and return true if they are equal.

Here's an example of how the equals() method works:

```kotlin
val user1 = User("John", 30)
val user2 = User("John", 30)

println(user1 == user2) // true
```

In this example, we have two data classes with the same name and age properties. When we compare them using the == operator, the equals() method is called and returns true.

If we change one of the properties, the equals() method will return false:

```kotlin
val user1 = User("John", 30)
val user2 = User("John", 31)

println(user1 == user2) // false
```

## Generating a toString() Method

Data classes in Kotlin also generate a toString() method. This method is used to convert the data in a data class to a string.

Here's an example of how the toString() method works:

```kotlin
val user = User("John", 30)

println(user.toString()) // User(name=John, age=30)
```

As you can see, the toString() method prints out the data in the data class in a readable format.

## Conclusion

In this post, we looked at data classes in Kotlin and how to automatically generate equals(), hashCode(), and toString() methods. Data classes are a great way to create concise and safe code.