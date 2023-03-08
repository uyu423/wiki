---
title: 028: Infix Functions in Kotlin: Calling Functions Like Operators
description: 
published: true
date: 2023-02-01T17:23:32.727Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:23:28.844Z
---

- [028: Funciones infijas en Kotlin: funciones de llamada como operadores***Spanish** version of this document is available*](/es/Knowledge-base/Kotlin/Learning/028-infix-functions-in-kotlin-calling-functions-like-operators)
{.links-list}
- [028: Kotlin의 중위 함수: 연산자와 같은 함수 호출***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/028-infix-functions-in-kotlin-calling-functions-like-operators)
{.links-list}
- [028：Kotlin 中的中缀函数：像运算符一样调用函数***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/028-infix-functions-in-kotlin-calling-functions-like-operators)
{.links-list}



#028: Infix Functions in Kotlin: Calling Functions Like Operators
Kotlin is a statically typed programming language for the JVM, Android, and the browser. It is known for its interoperability, safety, tooling support, and concise syntax.

Kotlin has a number of features that make it unique and attractive to developers, one of which is infix functions.

Infix functions are functions that can be called without using the usual dot notation. This means that they can be called like operators, which can make code more concise and readable.

Infix functions are marked with the infix keyword. They must be member functions or extension functions. They can only have one parameter.

Here is a simple example of an infix function:

```kotlin
infix fun Int.times(str: String) = str.repeat(this)

println(2 times "Bye ") // Prints "Bye Bye "
```

In the example above, the `times` function is called with the `2` and `"Bye "` parameters. The `times` function returns the string `"Bye "` repeated `2` times.

Infix functions can be very useful for making code more readable. For example, the `+` operator is often used for concatenating strings. However, it can also be used for addition. This can be confusing for developers who are not familiar with Kotlin.

With infix functions, we can define our own `+` operator for string concatenation, which can make our code more readable:

```kotlin
infix fun String.plus(str: String) = this + str

println("Hello" plus " world") // Prints "Hello world"
```

In the example above, we have defined an infix function for string concatenation. We can now use the `+` operator to concatenate two strings. This can make our code more readable and concise.

Infix functions can also be used for comparison. For example, we can use the `compareTo` function to compare two strings:

```kotlin
infix fun String.compareTo(str: String) = this.compareTo(str)

println("a" compareTo "b") // Prints -1
println("b" compareTo "a") // Prints 1
println("a" compareTo "a") // Prints 0
```

In the example above, we have defined an infix function for string comparison. We can now use the `compareTo` function to compare two strings. This can make our code more readable and concise.

Infix functions are a powerful tool that can make Kotlin code more readable and concise. However, they should be used with caution, as they can make code less readable if used excessively.