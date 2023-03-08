---
title: 049: Higher-Order Functions and Lambdas in Kotlin: Understanding Closures and Function Types
description: 
published: true
date: 2023-02-16T15:32:51.367Z
tags: 
editor: markdown
dateCreated: 2023-02-16T15:32:41.803Z
---

- [049: Funciones de orden superior y Lambdas en Kotlin: comprensión de cierres y tipos de funciones***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/049-higher-order-functions-and-lambdas-in-kotlin-understanding-closures-and-function-types)
{.links-list}
- [049：Kotlin 中的高阶函数和 Lambda：了解闭包和函数类型***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/049-higher-order-functions-and-lambdas-in-kotlin-understanding-closures-and-function-types)
{.links-list}
- [049: Kotlin의 고차 함수 및 람다: 클로저 및 함수 유형 이해***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/049-higher-order-functions-and-lambdas-in-kotlin-understanding-closures-and-function-types)
{.links-list}


# 049: Higher-Order Functions and Lambdas in Kotlin: Understanding Closures and Function Types

In this post, we'll be taking a look at higher-order functions and lambdas in Kotlin. We'll learn about what they are and how to use them, as well as understand some of the concepts behind them, such as closures and function types.

## What are higher-order functions and lambdas?

In Kotlin, a higher-order function is a function that takes one or more functions as arguments, or returns a function as a result. Lambdas are a type of anonymous function, which means they don't have a name.

Let's take a look at a simple example of a higher-order function that takes a lambda as an argument. This function takes a lambda that takes an Int and returns a Boolean, and it returns a list of all the Ints that return true when passed into the lambda:

```kotlin
fun filter(predicate: (Int) -> Boolean): List<Int> {
    val list = mutableListOf<Int>()
    for (i in 1..10) {
        if (predicate(i)) {
            list.add(i)
        }
    }
    return list
}
```

We can call this function like this:

```kotlin
val evenNumbers = filter { it % 2 == 0 }
```

The it keyword in the lambda is a placeholder for the argument that is passed into the lambda. In this case, it represents the Int that is passed into the filter function.

## What are closures?

A closure is a function that captures the state of its surrounding environment. In other words, it can access variables from the scope in which it was defined.

Here's a simple example of a closure in Kotlin. We have a variable called counter, and a function that increments the counter and returns the new value. This function is a closure because it captures the state of the counter variable:

```kotlin
var counter = 0
fun incrementCounter(): Int {
    return ++counter
}
```

If we call the incrementCounter function multiple times, it will keep track of the current value of the counter variable and return the new value each time:

```kotlin
incrementCounter() // returns 1
incrementCounter() // returns 2
incrementCounter() // returns 3
```

## What are function types?

In Kotlin, every function has a type. The type of a function is made up of the types of the arguments that the function takes, and the type of the value that the function returns.

For example, the type of the incrementCounter function from the previous section is (() -> Int). This can be read as "a function that takes no arguments and returns an Int."

The type of the filter function from the first section is ((Int) -> Boolean) -> List<Int>. This can be read as "a function that takes a function that takes an Int and returns a Boolean, and returns a List of Ints."

Function types are important in Kotlin because they allow us to specify what type of functions we want to work with. For example, we can write a higher-order function that takes a function with the type (Int) -> Boolean and returns a list of all the Ints that return true when passed into the function:

```kotlin
fun filter(predicate: (Int) -> Boolean): List<Int> {
    val list = mutableListOf<Int>()
    for (i in 1..10) {
        if (predicate(i)) {
            list.add(i)
        }
    }
    return list
}
```

We can call this function like this:

```kotlin
val evenNumbers = filter { it % 2 == 0 }
```

The it keyword in the lambda is a placeholder for the argument that is passed into the lambda. In this case, it represents the Int that is passed into the filter function.

## Conclusion

In this post, we've learned about higher-order functions and lambdas in Kotlin. We've seen how to use them, and we've also learned about some of the concepts behind them, such as closures and function types.