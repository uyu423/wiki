---
title: 016: Exception Handling in Kotlin: Throwing and Catching Exceptions
description: 
published: true
date: 2023-02-05T10:17:24.785Z
tags: 
editor: markdown
dateCreated: 2023-02-05T10:17:19.271Z
---

- [016: Manejo de excepciones en Kotlin: lanzar y capturar excepciones***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/016-exception-handling-in-kotlin-throwing-and-catching-exceptions)
{.links-list}
- [016：Kotlin 中的异常处理：抛出和捕获异常***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/016-exception-handling-in-kotlin-throwing-and-catching-exceptions)
{.links-list}
- [016: Kotlin의 예외 처리: 예외 발생 및 포착***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/016-exception-handling-in-kotlin-throwing-and-catching-exceptions)
{.links-list}


# Exception Handling in Kotlin: Throwing and Catching Exceptions

Exceptions are events that occur during the execution of a program that disrupt the normal flow of instructions. When an exception is thrown, it creates an exception object that contains information about the error, such as the type of exception and the state of the program when the error occurred.

Exceptions can be caused by many things, including but not limited to:

- A bug in the code
- Invalid user input
- A hardware failure

There are two types of exceptions in Kotlin: unchecked and checked. Unchecked exceptions are those that extend the ```RuntimeException``` class, and checked exceptions are those that extend the ```Exception``` class.

## Throwing Exceptions

Exceptions can be thrown manually using the ```throw``` keyword. This is useful when you want to abort the execution of a program due to an error. For example, let's say we have a function that calculates the average of two numbers. If the user passes in an invalid input, we want to throw an exception.

```kotlin
fun average(a: Int, b: Int): Double {
    if (a < 0 || b < 0) {
        throw IllegalArgumentException("Numbers must be positive.")
    }
    return (a + b) / 2.0
}
```

In the code above, we throw an ```IllegalArgumentException``` if the inputs are negative. Now, if we try to call the ```average``` function with negative numbers, an exception will be thrown and the program will be aborted.

```kotlin
average(-1, 2) // Throws an IllegalArgumentException
```

## Catching Exceptions

Exceptions can be caught using the ```try```/```catch``` keywords. This is useful for gracefully handling errors and continuing the execution of the program. For example, let's say we want to catch the exception thrown by our ```average``` function and print an error message to the user.

```kotlin
fun average(a: Int, b: Int): Double {
    if (a < 0 || b < 0) {
        throw IllegalArgumentException("Numbers must be positive.")
    }
    return (a + b) / 2.0
}

fun main(args: Array<String>) {
    val a = -1
    val b = 2
    try {
        val avg = average(a, b)
        println("The average of $a and $b is $avg")
    } catch (e: IllegalArgumentException) {
        println("Error: ${e.message}")
    }
}
```

In the code above, we catch the ```IllegalArgumentException``` thrown by our ```average``` function. We then print an error message to the user.

## Additional Information

- Exceptions can be caught using the ```try```/```catch``` keywords.
- Exceptions can be thrown manually using the ```throw``` keyword.
- Unchecked exceptions are those that extend the ```RuntimeException``` class.
- Checked exceptions are those that extend the ```Exception``` class.