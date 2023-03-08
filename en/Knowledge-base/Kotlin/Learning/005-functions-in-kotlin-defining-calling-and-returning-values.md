---
title: 005: Functions in Kotlin: Defining, Calling, and Returning Values
description: 
published: true
date: 2023-02-16T02:32:29.712Z
tags: 
editor: markdown
dateCreated: 2023-02-16T02:32:22.077Z
---

- [005: Funciones en Kotlin: definición, llamada y devolución de valores***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/005-functions-in-kotlin-defining-calling-and-returning-values)
{.links-list}
- [005：Kotlin 中的函数：定义、调用和返回值***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/005-functions-in-kotlin-defining-calling-and-returning-values)
{.links-list}
- [005: Kotlin의 함수: 값 정의, 호출 및 반환***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/005-functions-in-kotlin-defining-calling-and-returning-values)
{.links-list}


# Functions in Kotlin: Defining, Calling, and Returning Values

Function is a set of code that performs a specific task. In Kotlin, we can define our own functions to be called later whenever we need to perform that task. In this post, we'll learn how to define functions, call them, and return values from them.

## Defining Functions

In Kotlin, we define functions using the ```fun``` keyword. For example, let's say we want to define a function that prints a greeting message. We can do so like this:

```kotlin
fun printGreeting() {
    println("Hello, world!")
}
```

We can also define functions that take in arguments. For example, let's say we want to define a function that prints a greeting message with a name. We can do so like this:

```kotlin
fun printGreeting(name: String) {
    println("Hello, $name!")
}
```

We can also define functions that return values. For example, let's say we want to define a function that calculates the sum of two numbers. We can do so like this:

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

## Calling Functions

We call functions by simply using their names followed by parentheses ```()```. For example, we can call the ```printGreeting()``` function we defined earlier like this:

```kotlin
printGreeting() // prints "Hello, world!"
```

If we defined a function that takes in arguments, we need to pass in the arguments within the parentheses ```()```. For example, we can call the ```printGreeting(name: String)``` function we defined earlier like this:

```kotlin
printGreeting("John") // prints "Hello, John!"
```

If we defined a function that returns a value, we need to store the return value in a variable. For example, we can call the ```sum(a: Int, b: Int): Int``` function we defined earlier like this:

```kotlin
val result = sum(1, 2) // result is 3
```

## Returning Values

As we saw in the previous section, we can define functions that return values. In Kotlin, we use the ```return``` keyword to return a value from a function. For example, let's say we want to define a function that calculates the sum of two numbers and returns the result. We can do so like this:

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

We can also return values without explicitly using the ```return``` keyword. For example, let's say we want to define a function that calculates the sum of two numbers and returns the result. We can do so like this:

```kotlin
fun sum(a: Int, b: Int): Int = a + b
```

In the latter example, we return the value of ```a + b``` by simply assigning it to the function name ```sum```.

That's it for this post! In summary, we learned how to define functions, call them, and return values from them.