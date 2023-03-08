---
title: 057: Exception Handling in Kotlin: Dealing with Errors and Exceptions
description: 
published: true
date: 2023-02-01T16:23:26.881Z
tags: 
editor: markdown
dateCreated: 2023-02-01T16:23:22.982Z
---

- [057: Manejo de excepciones en Kotlin: manejo de errores y excepciones***Spanish** version of this document is available*](/es/Knowledge-base/Kotlin/Learning/057-exception-handling-in-kotlin-dealing-with-errors-and-exceptions)
{.links-list}
- [057: Kotlin의 예외 처리: 오류 및 예외 처리***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/057-exception-handling-in-kotlin-dealing-with-errors-and-exceptions)
{.links-list}
- [057：Kotlin 中的异常处理：处理错误和异常***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/057-exception-handling-in-kotlin-dealing-with-errors-and-exceptions)
{.links-list}


# Kotlin Exception Handling

Exceptions are events that occur during the execution of a program that disrupt the normal flow of instructions. Kotlin provides a powerful mechanism to deal with exceptions. In this article, we'll take a look at how to handle exceptions in Kotlin.

## What are Exceptions?

An exception is an event that occurs during the execution of a program that disrupts the normal flow of instructions. When an exception occurs, the program terminates abruptly.

There are two types of exceptions: checked and unchecked. Checked exceptions are those that occur at compile time, such as when a file is not found. Unchecked exceptions are those that occur at runtime, such as when a divide-by-zero error occurs.

## Handling Exceptions

Kotlin provides a powerful mechanism to deal with exceptions. The try/catch block is used to handle exceptions. The try block contains the code that may throw an exception. The catch block contains the code that handles the exception.

```kotlin
try {
   // code that may throw an exception
} catch (e: Exception) {
   // code that handles the exception
}
```

If an exception occurs in the try block, the catch block is executed. If no exception occurs, the catch block is skipped.

It is also possible to have multiple catch blocks to handle different types of exceptions.

```kotlin
try {
   // code that may throw an exception
} catch (e: FileNotFoundException) {
   // code that handles the FileNotFoundException
} catch (e: IOException) {
   // code that handles the IOException
}
```

## Finally Block

The finally block is optional. It is executed whether or not an exception occurs.

```kotlin
try {
   // code that may throw an exception
} catch (e: Exception) {
   // code that handles the exception
} finally {
   // code that is always executed
}
```

## Throwing Exceptions

Exceptions can be thrown explicitly using the throw keyword.

```kotlin
throw FileNotFoundException()
```

## Creating Custom Exceptions

It is possible to create custom exceptions by extending the Exception class.

```kotlin
class MyException: Exception() {
}
```

## Resources

- [Kotlin docs - Exception Handling](https://kotlinlang.org/docs/reference/exceptions.html)
- [JavaWorld - Exception Handling in Kotlin](https://www.javaworld.com/article/3240006/learn-java/exception-handling-in-kotlin.html)
- [Stack Overflow - How do I create a custom exception in Kotlin?](https://stackoverflow.com/questions/44487193/how-do-i-create-a-custom-exception-in-kotlin)