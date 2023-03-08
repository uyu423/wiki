---
title: 045: Local Functions in Kotlin: Creating Functions Within Functions
description: 
published: true
date: 2023-02-02T01:43:47.417Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:43:43.194Z
---

- [045: Funciones locales en Kotlin: creación de funciones dentro de funciones***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/045-local-functions-in-kotlin-creating-functions-within-functions)
{.links-list}
- [045：Kotlin 中的局部函数：在函数中创建函数***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/045-local-functions-in-kotlin-creating-functions-within-functions)
{.links-list}
- [045: Kotlin의 로컬 함수: 함수 내에 함수 만들기***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/045-local-functions-in-kotlin-creating-functions-within-functions)
{.links-list}


# Local Functions in Kotlin: Creating Functions Within Functions

When you're writing code in Kotlin, you'll often find yourself wanting to create a function inside of another function. This is called a **local function**. Local functions are useful because they can access the variables of the outer function, which means they can be used to simplify complex code.

In this post, we'll take a look at how to create local functions in Kotlin. We'll also discuss some of the benefits of using local functions.

## Defining Local Functions

A local function is defined within the body of another function. Here's an example:

```kotlin
fun outerFunction() {
    fun localFunction() {
        // Code goes here
    }
}
```

As you can see, the local function is defined inside the body of the outer function. It's important to note that the local function can only be called from within the outer function. This means that the local function has **local scope**.

It's also worth noting that local functions can access the variables of the outer function. This is because local functions are **nested** within the outer function. Here's an example:

```kotlin
fun outerFunction() {
    val outerVariable = " outer"

    fun localFunction() {
        println(outerVariable) // Prints " outer"
    }
}
```

As you can see, the local function can access the `outerVariable` variable, which is defined in the outer function.

## Calling Local Functions

Local functions can only be called from within the function in which they're defined. This means that they have **local scope**. Here's an example:

```kotlin
fun outerFunction() {
    fun localFunction() {
        // Code goes here
    }

    localFunction() // Calls the local function
}
```

As you can see, the local function is called from within the outer function. If we try to call the local function from outside the outer function, we'll get an error:

```kotlin
fun outerFunction() {
    fun localFunction() {
        // Code goes here
    }
}

localFunction() // Error: localFunction is not defined
```

## Benefits of Local Functions

Local functions are useful because they can access the variables of the outer function. This means they can be used to simplify complex code.

For example, let's say we have a function that calculates the factorial of a number. The factorial of a number is the product of all the positive integers less than or equal to the number. For example, the factorial of 5 is 5 * 4 * 3 * 2 * 1, which is 120.

Here's how we could write a function to calculate the factorial of a number in Kotlin:

```kotlin
fun factorial(n: Int): Int {
    if (n == 0) {
        return 1
    }

    return n * factorial(n - 1)
}
```

This function uses **recursion**, which is a technique for writing functions that call themselves.

The problem with this function is that it's **not tail-recursive**. This means that the function calls itself multiple times before it returns a result. This can lead to **stack overflow** errors, which happen when the function calls itself so many times that the stack overflows.

We can solve this problem by using a local function:

```kotlin
fun factorial(n: Int): Int {
    tailrec fun factorial(acc: Int, n: Int): Int {
        if (n == 0) {
            return acc
        }

        return factorial(acc * n, n - 1)
    }

    return factorial(1, n)
}
```

This function is **tail-recursive**, which means that the function calls itself only once before it returns a result. This means that the function can be called with large values of `n` without running into stack overflow errors.

## Conclusion

In this post, we've looked at how to create local functions in Kotlin. We've also discussed some of the benefits of using local functions.

Local functions are useful because they can access the variables of the outer function. This means they can be used to simplify complex code.

If you're interested in learning more about local functions, I recommend reading the following resources:

- The Kotlin documentation on [local functions](https://kotlinlang.org/docs/reference/local-functions.html)
- A blog post on [recursion and tail recursion in Kotlin](https://blog.kotlin-academy.com/recursion-and-tail-recursion-in-kotlin-f79bc55a326a)
- A blog post on [the benefits of local functions](https://blog.kotlin-academy.com/the-benefits-of-local-functions-f79bc55a326a)