---
title: 054: Functions as First-Class Citizens in Kotlin: Understanding Higher-Order Functions
description: 
published: true
date: 2023-02-16T18:32:58.485Z
tags: 
editor: markdown
dateCreated: 2023-02-16T18:32:55.843Z
---

- [054: Funciones como ciudadanos de primera clase en Kotlin: comprensión de las funciones de orden superior***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/054-functions-as-first-class-citizens-in-kotlin-understanding-higher-order-functions)
{.links-list}
- [054：Kotlin 中的一等公民函数：理解高阶函数***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/054-functions-as-first-class-citizens-in-kotlin-understanding-higher-order-functions)
{.links-list}
- [054: Kotlin의 일급 시민으로서의 기능: 고차 함수 이해***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/054-functions-as-first-class-citizens-in-kotlin-understanding-higher-order-functions)
{.links-list}


## Introduction

Kotlin is a modern programming language that runs on the Java Virtual Machine. It is a statically typed language that combines the best features of both object-oriented and functional programming.

Kotlin is a first-class citizen on the JVM, which means that it can be used to develop any kind of Java application, from simple command-line programs to complex web applications.

One of the most important features of Kotlin is that it supports higher-order functions. In this article, we will learn what higher-order functions are and how to use them in Kotlin.

## What is a Higher-Order Function?

A higher-order function is a function that takes one or more functions as arguments and returns a function as a result.

In Kotlin, higher-order functions are represented by the ```Function<T, R>``` type. This type has two type parameters:

- ```T``` is the type of the argument to the function.
- ```R``` is the type of the result of the function.

The ```Function<T, R>``` type can be used to represent any function that takes an argument of type ```T``` and returns a result of type ```R```.

## How to Use Higher-Order Functions in Kotlin

There are many built-in higher-order functions in Kotlin that are available for use. In this section, we will learn how to use some of the most commonly used higher-order functions.

### The ```map``` Function

The ```map``` function is a higher-order function that takes a function as an argument and applies it to each element of a list.

For example, suppose we have a list of strings and we want to convert them to uppercase. We can do this using the ```map``` function:

```kotlin
val list = listOf("a", "b", "c")

val upperCaseList = list.map { it.toUpperCase() }

// upperCaseList is now a list of strings: ["A", "B", "C"]
```

In the example above, we have a list of strings and we use the ```map``` function to apply the ```toUpperCase()``` function to each element of the list.

The ```map``` function can be used with any type of list, not just lists of strings. For example, we can use ```map``` with a list of integers:

```kotlin
val list = listOf(1, 2, 3)

val doubleList = list.map { it * 2 }

// doubleList is now a list of integers: [2, 4, 6]
```

### The ```filter``` Function

The ```filter``` function is a higher-order function that takes a function as an argument and applies it to each element of a list. The function should return ```true``` or ```false```.

The ```filter``` function will return a new list that contains only the elements for which the function returns ```true```.

For example, suppose we have a list of strings and we want to filter out all the strings that are longer than three characters. We can do this using the ```filter``` function:

```kotlin
val list = listOf("a", "ab", "abc", "abcd")

val filteredList = list.filter { it.length <= 3 }

// filteredList is now a list of strings: ["a", "ab", "abc"]
```

In the example above, we have a list of strings and we use the ```filter``` function to remove all the strings that are longer than three characters.

The ```filter``` function can be used with any type of list, not just lists of strings. For example, we can use ```filter``` with a list of integers:

```kotlin
val list = listOf(1, 2, 3, 4, 5)

val filteredList = list.filter { it % 2 == 0 }

// filteredList is now a list of integers: [2, 4]
```

In the example above, we have a list of integers and we use the ```filter``` function to remove all the odd numbers.

### The ```reduce``` Function

The ```reduce``` function is a higher-order function that takes a function as an argument and applies it to each element of a list. The function should take two arguments and return a single value.

The ```reduce``` function will return a single value that is the result of applying the function to each element of the list.

For example, suppose we have a list of integers and we want to find the sum of all the elements in the list. We can do this using the ```reduce``` function:

```kotlin
val list = listOf(1, 2, 3, 4, 5)

val sum = list.reduce { a, b -> a + b }

// sum is now 15
```

In the example above, we have a list of integers and we use the ```reduce``` function to find the sum of all the elements in the list.

The ```reduce``` function can be used with any type of list, not just lists of integers. For example, we can use ```reduce``` with a list of strings:

```kotlin
val list = listOf("a", "b", "c")

val concatenatedString = list.reduce { a, b -> a + b }

// concatenatedString is now "abc"
```

In the example above, we have a list of strings and we use the ```reduce``` function to concatenate all the strings into a single string.

## Conclusion

In this article, we have learned what higher-order functions are and how to use them in Kotlin. We have seen how to use the ```map```, ```filter```, and ```reduce``` functions to transform and manipulate lists.

Higher-order functions are a powerful tool that can be used to write concise and readable code. If you are new to Kotlin, I encourage you to experiment with higher-order functions and see what you can come up with.