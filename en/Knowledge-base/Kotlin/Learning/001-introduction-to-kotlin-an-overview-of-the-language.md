---
title: 001: Introduction to Kotlin: An Overview of the Language
description: 
published: true
date: 2023-01-31T06:04:19.991Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:04:16.531Z
---

- [001: Kotlin 소개: 언어 개요***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/001-introduction-to-kotlin-an-overview-of-the-language)
{.links-list}
- [001: Kotlin の紹介: 言語の概要***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/001-introduction-to-kotlin-an-overview-of-the-language)
{.links-list}
- [001：Kotlin 简介：语言概述***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/001-introduction-to-kotlin-an-overview-of-the-language)
{.links-list}



# Kotlin

Kotlin is a statically typed programming language that runs on the Java Virtual Machine and can also be compiled to JavaScript source code. Kotlin is developed by JetBrains, the company behind the IntelliJ IDEA Java IDE.

Kotlin is a cross-platform, statically typed, general-purpose programming language with type inference. Kotlin is designed to interoperate fully with Java, and the JVM version of its standard library depends on the Java Class Library, but type inference allows its syntax to be more concise.

## Features

Kotlin has the following features:

- **Null safety**: Kotlin's type system prevents null references from being dereferenced.

- **Extension functions**: Kotlin allows you to extend a class with new functionality without having to inherit from the class.

- **Higher-order functions and lambdas**: Kotlin provides support for higher-order functions and lambdas.

- **Data classes**: Kotlin provides a concise way to create classes that contain only data.

- **Companion objects**: Kotlin allows you to define static members of a class in a companion object.

- **Object-oriented**: Kotlin is object-oriented, but also provides support for functional programming.

- **Kotlin standard library**: Kotlin comes with a standard library that contains a rich set of functions and types.

## Syntax

Kotlin has a concise syntax that is easy to learn.

```kotlin
// Define a function that takes two Int arguments and returns an Int.
fun sum(a: Int, b: Int): Int {
   return a + b
}

// Define a data class.
data class User(val name: String, val age: Int)

// Define a companion object.
object MyClass {
   fun doSomething() { ... }
}

// Define a higher-order function.
fun MyClass.myFunction(a: Int, b: Int, f: (Int, Int) -> Int): Int {
   return f(a, b)
}

// Use a lambda expression.
val result = MyClass.myFunction(1, 2) { a, b -> a + b }

// Define an extension function.
fun String.toUpperCase(): String {
   return this.toUpperCase()
}
```

## Getting started

To get started with Kotlin, you can download the Kotlin plugin for IntelliJ IDEA or Eclipse.

You can also use the Kotlin command line compiler to compile your Kotlin source code to JavaScript or JVM bytecode.

To learn more about Kotlin, you can take a look at the following resources:

- The Kotlin website: https://kotlinlang.org

- The Kotlin Koans: https://kotlinlang.org/docs/tutorials/koans.html

- The Kotlin standard library documentation: https://kotlinlang.org/api/latest/jvm/stdlib/

- The Kotlin reference: https://kotlinlang.org/docs/reference/

## Conclusion

Kotlin is a concise, safe, and fun to use programming language that runs on the JVM and can also be compiled to JavaScript.