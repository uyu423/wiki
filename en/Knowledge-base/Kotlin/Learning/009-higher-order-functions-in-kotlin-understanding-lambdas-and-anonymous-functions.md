---
title: 009: Higher-Order Functions in Kotlin: Understanding Lambdas and Anonymous Functions
description: 
published: true
date: 2023-01-31T05:36:04.908Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:36:02.755Z
---

- [009: Kotlin의 고차 함수: 람다 및 익명 함수 이해***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/009-higher-order-functions-in-kotlin-understanding-lambdas-and-anonymous-functions)
{.links-list}
- [009: Kotlin の高階関数: ラムダと匿名関数を理解する***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/009-higher-order-functions-in-kotlin-understanding-lambdas-and-anonymous-functions)
{.links-list}
- [009：Kotlin 中的高阶函数：了解 Lambda 和匿名函数***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/009-higher-order-functions-in-kotlin-understanding-lambdas-and-anonymous-functions)
{.links-list}


# 009: Higher Order Functions in Kotlin: Understanding Lambdas and Anonymous Functions

In computer programming, a higher-order function is a function that takes one or more functions as arguments (i.e. procedural parameters), and returns a new function as its result.

In Kotlin, higher-order functions are very common, due to the language's rich set of built-in functions and the fact that functions are first-class citizens, which means they can be stored in variables and passed as arguments to other functions.

One of the most commonly used higher-order functions in Kotlin is the `apply` function, which is used to execute a given block of code on an object, and then return the object itself. For example, consider the following code:

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

In the code above, the `apply` function is used to execute the given block of code (i.e. the code between the curly braces) on the `list` object, and then return the `list` object itself. The `also` function is then used to perform some additional actions on the `list` object (in this case, printing it to the console).

One of the key things to understand about higher-order functions is that they can be used to abstract away repeated code patterns. For example, consider the following code:

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

In the code above, the `apply` function is used to add a new element to the `list`, and then return the `list`. This particular code pattern is so common that Kotlin provides a built-in `+=` operator that can be used instead:

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list += 5
    list += listOf(6, 7, 8)

    println(list)
}
```

The `+=` operator is just an shorthand for the `apply` function, which means it's equivalent to the following code:

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }

    println(list)
}
```

As you can see, the `+=` operator can be used to abstract away the common code pattern of adding an element to a list (or any other mutable collection).

Another common higher-order function is the `let` function, which is used to execute a given block of code on an object, and then return the result of the code. For example, consider the following code:

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list.let {
        it.add(5)
        it.addAll(listOf(6, 7, 8))
        it
    }

    println(newList)
}
```

In the code above, the `let` function is used to execute the given block of code on the `list` object, and then return the `list` object itself. The `it` variable is used to refer to the `list` object inside the block of code.

Similarly to the `apply` function, the `let` function can be used to abstract away repeated code patterns. For example, consider the following code:

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list.let {
        it.add(5)
        it.addAll(listOf(6, 7, 8))
        it
    }

    println(newList)
}
```

In the code above, the `let` function is used to add a new element to the `list`, and then return the `list`. This particular code pattern is so common that Kotlin provides a built-in `+=` operator that can be used instead:

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list += 5
    val newList = list += listOf(6, 7, 8)

    println(newList)
}
```

The `+=` operator is just an shorthand for the `let` function, which means it's equivalent to the following code:

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    val newList = list.let {
        it.add(5)
        it.addAll(listOf(6, 7, 8))
        it
    }

    println(newList)
}
```

As you can see, the `+=` operator can be used to abstract away the common code pattern of adding an element to a list (or any other mutable collection).

Finally, it's worth mentioning that higher-order functions are often used in conjunction with lambdas, which are anonymous functions that don't have a name. Lambdas are often used to pass a block of code to a higher-order function as an argument. For example, consider the following code:

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        this.add(5)
        this.addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

In the code above, the `apply` function is used to execute the given lambda on the `list` object, and then return the `list` object itself. The `also` function is then used to perform some additional actions on the `list` object (in this case, printing it to the console).

As you can see, lambdas can be used to abstract away repeated code patterns. For example, consider the following code:

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }.also {
        println(it)
    }
}
```

In the code above, the `apply` function is used to add a new element to the `list`, and then return the `list`. This particular code pattern is so common that Kotlin provides a built-in `+=` operator that can be used instead:

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list += 5
    list += listOf(6, 7, 8)

    println(list)
}
```

The `+=` operator is just an shorthand for the `apply` function, which means it's equivalent to the following code:

```kotlin
fun main(args: Array<String>) {
    val list = mutableListOf(1, 2, 3, 4)

    list.apply {
        add(5)
        addAll(listOf(6, 7, 8))
    }

    println(list)
}
```

As you can see, the `+=` operator can be used to abstract away the common code pattern of adding an element to a list (or any other mutable collection).

Key points:
- Higher-order functions are functions that take one or more functions as arguments and return a new function as its result.
- In Kotlin, higher-order functions are very common, due to the language's rich set of built-in functions and the fact that functions are first-class citizens.
- One of the most commonly used higher-order functions in Kotlin is the `apply` function, which is used to execute a given block of code on an object, and then return the object itself. 
- Another common higher-order function is the `let` function, which is used to execute a given block of code on an object, and then return the result of the code.
- Higher-order functions are often used in conjunction with lambdas, which are anonymous functions that don't have a name.