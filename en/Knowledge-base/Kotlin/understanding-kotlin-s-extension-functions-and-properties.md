---
title: Understanding Kotlin's Extension Functions and Properties
description: 
published: true
date: 2023-02-02T03:36:31.255Z
tags: 
editor: markdown
dateCreated: 2023-02-02T03:36:26.959Z
---

- [Comprender las funciones y propiedades de extensión de Kotlin***Spanish** document is available*](/es/Knowledge-base/Kotlin/understanding-kotlin-s-extension-functions-and-properties)
{.links-list}
- [了解 Kotlin 的扩展函数和属性***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/understanding-kotlin-s-extension-functions-and-properties)
{.links-list}
- [Kotlin의 확장 기능 및 속성 이해***Korean** document is available*](/ko/Knowledge-base/Kotlin/understanding-kotlin-s-extension-functions-and-properties)
{.links-list}


# Understanding Kotlin's Extension Functions and Properties

Kotlin is a powerful programming language that offers many features to make development faster and easier. One of these features are extension functions and properties.

Extension functions and properties allow you to extend the functionality of a class without having to inherit from it. This is especially useful when you want to use features from a library without depending on that library.

In this article, we'll take a closer look at extension functions and properties in Kotlin. We'll learn how to define them and how to use them in our own code.

## Defining Extension Functions and Properties

Extension functions and properties are defined using the `fun` and `val` keywords, respectively. They are written after the name of the class that they are extending, followed by a dot `.`:

```kotlin
// Extension function
fun String.repeat(times: Int): String {
    return this.repeat(times)
}

// Extension property
val String.length: Int
    get() = this.length
```

In the example above, we've defined an extension function `repeat` that allows us to repeat a string a given number of times. We've also defined an extension property `length` that allows us to get the length of a string.

Note that extension functions and properties are not actually defined in the class that they are extending. They are compiled as static methods and properties in the class that they are defined in. This means that they can be called from anywhere, even from outside of the class.

## Using Extension Functions and Properties

Extension functions and properties can be used just like any other function or property. In the example below, we use the `repeat` function to repeat a string 10 times:

```kotlin
fun main() {
    val s = "Hello, world!".repeat(10)
    println(s)
}
```

We can also use the `length` property to get the length of a string:

```kotlin
fun main() {
    val s = "Hello, world!"
    println(s.length)
}
```

## Overriding Extension Functions and Properties

It's also possible to override extension functions and properties. This can be useful when you want to change the behavior of a function or property in a specific context.

To override an extension function or property, you just need to define it in the same way as you would any other function or property. In the example below, we override the `repeat` function so that it returns a string with the given number of exclamation points:

```kotlin
fun main() {
    fun String.repeat(times: Int): String {
        return this + "!".repeat(times)
    }

    val s = "Hello, world!".repeat(10)
    println(s)
}
```

## Conclusion

Extension functions and properties are a powerful feature in Kotlin that can be used to extend the functionality of a class without having to inherit from it. They are defined using the `fun` and `val` keywords, respectively, and they are written after the name of the class that they are extending, followed by a dot `.`

Extension functions and properties can be used just like any other function or property. They are compiled as static methods and properties, which means that they can be called from anywhere, even from outside of the class.

It's also possible to override extension functions and properties. This can be useful when you want to change the behavior of a function or property in a specific context.