---
title: 034: vararg Functions in Kotlin: Creating Functions that Accept a Variable Number of Arguments
description: 
published: true
date: 2023-02-13T18:55:47.369Z
tags: 
editor: markdown
dateCreated: 2023-02-13T18:55:40.247Z
---

- [034: funciones vararg en Kotlin: creación de funciones que aceptan un número variable de argumentos***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/034-vararg-functions-in-kotlin-creating-functions-that-accept-a-variable-number-of-arguments)
{.links-list}
- [034：Kotlin 中的可变参数函数：创建接受可变数量参数的函数***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/034-vararg-functions-in-kotlin-creating-functions-that-accept-a-variable-number-of-arguments)
{.links-list}
- [034: Kotlin의 vararg 함수: 가변 개수의 인수를 허용하는 함수 만들기***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/034-vararg-functions-in-kotlin-creating-functions-that-accept-a-variable-number-of-arguments)
{.links-list}


# vararg Functions in Kotlin: Creating Functions that Accept a Variable Number of Arguments

Kotlin's vararg keyword allows us to create functions that accept a variable number of arguments. This can be useful when we want to write a function that can take any number of arguments, without having to explicitly specify the number of arguments in the function definition.

In this post, we'll learn how to create vararg functions in Kotlin, and how to use them in our code. We'll also look at some examples of how vararg functions can be used to simplify our code.

## Creating a Vararg Function

To create a vararg function in Kotlin, we use the vararg keyword before the parameter name in the function definition. For example, let's say we want to create a function that takes a variable number of strings and prints them out. We could do this with the following function definition:

```kotlin
fun printStrings(vararg strings: String) {
    for (string in strings) {
        println(string)
    }
}
```

Notice that we've placed the vararg keyword before the strings parameter. This tells Kotlin that the function can take any number of string arguments.

We can call this function with any number of string arguments, and they will all be printed out:

```kotlin
printStrings("Hello", "World") // Prints "Hello" and "World"
printStrings("Kotlin", "is", "awesome") // Prints "Kotlin", "is", and "awesome"
```

We can also call the function with no arguments, in which case nothing will be printed:

```kotlin
printStrings() // Prints nothing
```

## Accessing Vararg Parameters

When we create a vararg function, we can access the vararg parameters in the function body just like any other parameter. In the printStrings() function above, we accessed the strings parameter in a for loop to print out all of the strings.

We can also access the vararg parameters outside of the function body. To do this, we use the * operator before the parameter name when we call the function. For example, let's say we have a vararg function that takes a variable number of integers and prints them out:

```kotlin
fun printInts(vararg ints: Int) {
    for (int in ints) {
        println(int)
    }
}
```

We can call this function with any number of integer arguments, and they will all be printed out:

```kotlin
printInts(1, 2, 3) // Prints 1, 2, and 3
printInts(4, 5, 6, 7, 8) // Prints 4, 5, 6, 7, and 8
```

We can also call the function with no arguments, in which case nothing will be printed:

```kotlin
printInts() // Prints nothing
```

Now let's say we have an array of integers and we want to print them all out using the printInts() function. We can do this by using the * operator to "unpack" the array into individual arguments:

```kotlin
val intArray = intArrayOf(1, 2, 3)
printInts(*intArray) // Prints 1, 2, and 3
```

## Vararg and Non-Vararg Parameters

We can also create vararg functions that have both vararg and non-vararg parameters. For example, let's say we want to create a function that takes a variable number of strings and an integer, and prints out the strings a number of times equal to the integer:

```kotlin
fun printStringsNTimes(n: Int, vararg strings: String) {
    for (i in 1..n) {
        for (string in strings) {
            println(string)
        }
    }
}
```

In this function, we have a non-vararg parameter (n) and a vararg parameter (strings). We can call this function with any number of string arguments, and they will all be printed out n times:

```kotlin
printStringsNTimes(3, "Hello", "World") // Prints "Hello" and "World" three times
printStringsNTimes(5, "Kotlin", "is", "awesome") // Prints "Kotlin", "is", and "awesome" five times
```

We can also call the function with no string arguments, in which case nothing will be printed:

```kotlin
printStringsNTimes(3) // Prints nothing
```

## Conclusion

In this post, we learned how to create vararg functions in Kotlin, and how to use them in our code. We also looked at some examples of how vararg functions can be used to simplify our code.

If you want to learn more about Kotlin, check out the Kotlin documentation.