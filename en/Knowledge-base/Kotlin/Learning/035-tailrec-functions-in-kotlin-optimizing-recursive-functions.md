---
title: 035: Tailrec Functions in Kotlin: Optimizing Recursive Functions
description: 
published: true
date: 2023-02-16T09:32:28.709Z
tags: 
editor: markdown
dateCreated: 2023-02-16T09:32:26.425Z
---

- [035: Funciones Tailrec en Kotlin: Optimización de funciones recursivas***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/035-tailrec-functions-in-kotlin-optimizing-recursive-functions)
{.links-list}
- [035：Kotlin 中的 Tailrec 函数：优化递归函数***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/035-tailrec-functions-in-kotlin-optimizing-recursive-functions)
{.links-list}
- [035: Kotlin의 Tailrec 함수: 재귀 함수 최적화***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/035-tailrec-functions-in-kotlin-optimizing-recursive-functions)
{.links-list}


# 035: Tailrec Functions in Kotlin: Optimizing Recursive Functions

In this post, we'll take a look at how to use tailrec functions in Kotlin to optimize recursive functions.

Recursive functions are those that call themselves, either directly or indirectly. A tailrec function is a special type of recursive function where the last statement in the function is the recursive call.

Tailrec functions are more efficient than regular recursive functions because they are compiled to use a loop instead of making multiple function calls. This can result in a significant performance improvement, especially for recursive functions that are called many times.

To create a tailrec function in Kotlin, we use the tailrec keyword before the function name. For example, here's a tailrec function that calculates the factorial of a given number:

```kotlin
tailrec fun factorial(n: Int, result: Int = 1): Int {
    if (n == 1) return result
    return factorial(n - 1, n * result)
}
```

In this example, we're using the tailrec keyword before the fun keyword. We've also specified the function's return type (Int) and we've given the function two parameters: n and result.

The result parameter has a default value of 1, which is used when the function is first called.

The function calls itself recursively until the value of n is 1. At that point, the function returns the value of result.

You can see how this function works by calling it with different values:

```kotlin
factorial(5) // 120
factorial(10) // 3628800
```

As you can see, the tailrec function is a more efficient way to calculate the factorial of a number.

There are some restrictions on tailrec functions:

- The function must be a member of a class or an object
- The function must be marked with the tailrec keyword
- The function must have a single parameter
- The function must call itself recursively
- The function must return the same type as the parameter

If you try to create a tailrec function that doesn't meet these criteria, you'll get a compiler error.

## Additional Information

Here are some additional resources that you may find helpful:

- [Tail Recursion in Kotlin](https://kotlinlang.org/docs/reference/tail-recursion.html)
- [Tail Call Optimization in Kotlin](https://kotlinlang.org/docs/reference/tail-call-optimization.html)