---
title: 015: Nullable Types and Null Safety in Kotlin: Dealing with Null Values
description: 
published: true
date: 2023-02-16T04:33:02.979Z
tags: 
editor: markdown
dateCreated: 2023-02-16T04:32:54.825Z
---

- [015: Tipos anulables y seguridad nula en Kotlin: manejo de valores nulos***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/015-nullable-types-and-null-safety-in-kotlin-dealing-with-null-values)
{.links-list}
- [015：Kotlin 中的可空类型和空安全：处理空值***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/015-nullable-types-and-null-safety-in-kotlin-dealing-with-null-values)
{.links-list}
- [015: Kotlin의 Null 허용 유형 및 Null 안전성: Null 값 처리***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/015-nullable-types-and-null-safety-in-kotlin-dealing-with-null-values)
{.links-list}


## Introduction

Kotlin is a statically typed programming language that runs on the Java Virtual Machine. It is a general-purpose language that is designed to be concise, safe, and interoperable.

One of the key features of Kotlin is null safety. Null safety is a mechanism for preventing null pointer exceptions. Kotlin's type system is designed to eliminate the possibility of null references from code.

Nullable types are a way of representing types that can be null. In Kotlin, all types are non-nullable by default. This means that a variable of a non-null type cannot hold a null value.

To create a nullable type, we use the question mark (?) after the type name. For example, the following code defines a nullable String variable:

```kotlin
var str: String? = "Hello"
```

Now, the str variable can hold either a string value or null.

If we try to assign a null value to a variable of a non-null type, we will get a compilation error:

```kotlin
var str: String = "Hello"
str = null // error: null can not be a value of a non-null type String
```

To fix this, we can either change the type of the str variable to a nullable type or use a non-null assertion. A non-null assertion is an operator that tells the compiler that a variable is not null. We use it like this:

```kotlin
var str: String = "Hello"
str = null // error: null can not be a value of a non-null type String

str!!.length // non-null assertion
```

The non-null assertion operator is a double exclamation mark (!!). It should be used only when we are sure that a variable is not null. Otherwise, we will get a runtime exception.

## Checking for Null

In Kotlin, we can check if a variable is null using the `isNullOrEmpty()` function:

```kotlin
fun main() {
    var str: String? = "Hello"
    if (str.isNullOrEmpty()) {
        println("str is null or empty")
    } else {
        println(str.length)
    }
}
```

The `isNullOrEmpty()` function returns true if the string is null or empty. Otherwise, it returns false.

We can also use the `?` operator to check if a variable is null:

```kotlin
fun main() {
    var str: String? = "Hello"
    val length = str?.length // str is not null, so length is not null
    println(length)
}
```

The `?` operator is called the safe call operator. It checks if the variable is null before calling the length property. If the variable is null, it returns null. Otherwise, it returns the length of the string.

We can use the `?` operator to call a function on a nullable variable:

```kotlin
fun main() {
    var str: String? = "Hello"
    str?.let {
        println(it.length) // it is not null, so we can call the length property
    }
}
```

The `let` function is a higher-order function that takes a lambda as an argument. The lambda is only executed if the variable is not null.

We can also use the `?` operator to execute a block of code if a variable is not null:

```kotlin
fun main() {
    var str: String? = "Hello"
    str?.let {
        println(it.length) // it is not null, so we can call the length property
    }
}
```

The `?` operator is called the safe call operator. It checks if the variable is null before executing the lambda. If the variable is null, it does nothing. Otherwise, it executes the lambda.

## The Elvis Operator

The Elvis operator is a way of assigning a default value to a nullable variable. We use it like this:

```kotlin
fun main() {
    var str: String? = "Hello"
    val length = str?.length ?: 0 // if str is null, length is 0
    println(length)
}
```

If the `str` variable is null, the `length` variable is assigned the value 0. Otherwise, it is assigned the value of `str.length`.

The Elvis operator is often used with the `let` function:

```kotlin
fun main() {
    var str: String? = "Hello"
    str?.let {
        println(it.length) // it is not null, so we can call the length property
    } ?: println("str is null") // if str is null, print "str is null"
}
```

If the `str` variable is null, the `println("str is null")` statement is executed. Otherwise, the `println(it.length)` statement is executed.

## The Not-Null Assertion Operator

The not-null assertion operator is a way of telling the compiler that a variable is not null. We use it like this:

```kotlin
fun main() {
    var str: String? = "Hello"
    str!!.length // str is not null, so we can call the length property
}
```

The not-null assertion operator is a double exclamation mark (!!). It should be used only when we are sure that a variable is not null. Otherwise, we will get a runtime exception.

## The !! Operator

The !! operator is a way of telling the compiler that a variable is not null. We use it like this:

```kotlin
fun main() {
    var str: String? = "Hello"
    str!!.length // str is not null, so we can call the length property
}
```

The !! operator is a double exclamation mark (!!). It should be used only when we are sure that a variable is not null. Otherwise, we will get a runtime exception.

## Conclusion

In this article, we've learned about null safety in Kotlin. We've seen how to use nullable types and the different ways of checking for null values. We've also seen how to use the Elvis operator and the not-null assertion operator.