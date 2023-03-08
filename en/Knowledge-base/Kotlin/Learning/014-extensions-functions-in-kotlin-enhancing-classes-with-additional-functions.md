---
title: 014: Extensions Functions in Kotlin: Enhancing Classes with Additional Functions
description: 
published: true
date: 2023-01-31T16:57:27.000Z
tags: 
editor: markdown
dateCreated: 2023-01-31T16:57:23.406Z
---

- [014: Kotlin의 확장 기능: 추가 기능으로 클래스 향상***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/014-extensions-functions-in-kotlin-enhancing-classes-with-additional-functions)
{.links-list}
- [014: Kotlin の拡張機能: 追加機能によるクラスの拡張***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/014-extensions-functions-in-kotlin-enhancing-classes-with-additional-functions)
{.links-list}
- [014：Kotlin 中的扩展函数：使用附加函数增强类***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/014-extensions-functions-in-kotlin-enhancing-classes-with-additional-functions)
{.links-list}



# 14: Extensions Functions in Kotlin: Enhancing Classes with Additional Functions

Kotlin is a statically typed programming language for the JVM, Android and the browser. It is known for its interoperability, safety, tooling support, and concise syntax.

One of the most powerful features of Kotlin is extension functions. Extension functions are functions that are added to existing classes, without having to inherit from them. This means that you can add new functionality to existing classes, without having to modify the class itself.

In this article, we'll take a look at how to create extension functions, and how they can be used to enhance existing classes.

## Creating Extension Functions

Creating an extension function is simple. All you need to do is prefix the function name with the name of the class you want to extend, followed by a dot. For example, to create an extension function that adds a `print()` method to the `String` class, you would do the following:

```kotlin
fun String.print() {
    println(this)
}
```

Now, you can call the `print()` method on any string, like so:

```kotlin
"Hello, world!".print() // prints "Hello, world!"
```

As you can see, extension functions are a great way to add new functionality to existing classes.

## Using Extension Functions

Extension functions are particularly useful when you want to add new methods to a class that you don't have control over. For example, let's say you're using a library that has a `User` class, but you want to add a `getFullName()` method to it. With extension functions, you can do this without having to modify the `User` class itself.

First, let's define a `User` class:

```kotlin
class User(val firstName: String, val lastName: String)
```

Now, we can create an extension function that adds a `getFullName()` method to the `User` class:

```kotlin
fun User.getFullName(): String {
    return "$firstName $lastName"
}
```

Now, we can create a `User` object and call the `getFullName()` method on it:

```kotlin
val user = User("John", "Smith")
println(user.getFullName()) // prints "John Smith"
```

As you can see, extension functions are a great way to add new methods to existing classes, without having to modify the class itself.

## Conclusion

In this article, we've taken a look at extension functions in Kotlin. We've seen how to create extension functions, and how they can be used to add new methods to existing classes.