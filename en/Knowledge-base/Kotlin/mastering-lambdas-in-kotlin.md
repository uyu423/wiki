---
title: Mastering Lambdas in Kotlin
description: 
published: true
date: 2023-02-17T23:32:41.352Z
tags: 
editor: markdown
dateCreated: 2023-02-17T23:32:39.971Z
---

- [Kotlin에서 람다 마스터하기***Korean** document is available*](/ko/Knowledge-base/Kotlin/mastering-lambdas-in-kotlin)
{.links-list}


# Mastering Lambdas in Kotlin

Lambdas are a powerful tool in Kotlin that can help you write concise and effective code. In this article, we'll take a look at what lambdas are, how they work, and how to use them effectively in your Kotlin code.

## What are Lambdas?

Lambdas are a way to create anonymous functions. They are often used as a way to passed a function as an argument to another function. For example, consider the following code:

```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5)
    val doubledNumbers = numbers.map { it * 2 }
}
```

In the code above, we have a list of numbers and we want to create a new list that contains the double of each number in the original list. We could do this by creating a function that takes a number and returns the double of that number:

```kotlin
fun double(x: Int): Int {
    return x * 2
}
```

And then we could use that function in the `map` function:

```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5)
    val doubledNumbers = numbers.map(::double)
}
```

However, this is a bit verbose. We can achieve the same result using a lambda:

```kotlin
fun main() {
    val numbers = listOf(1, 2, 3, 4, 5)
    val doubledNumbers = numbers.map { it * 2 }
}
```

In the code above, we've created a lambda that takes an `Int` and returns the double of that `Int`. We've then passed that lambda to the `map` function. The `map` function will call our lambda for each element in the `numbers` list and return a new list with the results.

As you can see, lambdas can be a concise and effective way to write code.

## How do Lambdas Work?

Lambdas areAnonymous Functions. That is, they are functions that don't have a name.

Lambdas are often used to create a function that will be passed as an argument to another function. In the previous section, we saw an example of this when we passed a lambda to the `map` function.

Lambdas can be created in two ways:

* With a function body
* With an expression

### Lambdas with a Function Body

Lambdas with a function body are defined using the `{}` syntax. For example, the following is a lambda that takes an `Int` and returns the double of that `Int`:

```kotlin
val lambda = { x: Int ->
    x * 2
}
```

In the code above, we've defined a lambda that takes an `Int` and returns the double of that `Int`. We can then call that lambda like this:

```kotlin
val result = lambda(2)
```

In the code above, we've called the lambda with the `Int` `2` and stored the result in the `result` variable.

### Lambdas with an Expression

Lambdas with an expression are defined using the `=` syntax. For example, the following is a lambda that takes an `Int` and returns the double of that `Int`:

```kotlin
val lambda = { x: Int ->
    x * 2
}
```

In the code above, we've defined a lambda that takes an `Int` and returns the double of that `Int`. We can then call that lambda like this:

```kotlin
val result = lambda(2)
```

In the code above, we've called the lambda with the `Int` `2` and stored the result in the `result` variable.

## How to Use Lambdas

Now that we've seen what lambdas are and how they work, let's take a look at how to use them effectively in your code.

### Lambdas with Single Parameters

Lambdas with a single parameter can be defined using the `it` keyword. For example, the following is a lambda that takes a `String` and returns the length of that `String`:

```kotlin
val lambda = { it: String ->
    it.length
}
```

In the code above, we've defined a lambda that takes a `String` and returns the length of that `String`. We can then call that lambda like this:

```kotlin
val result = lambda("Hello, world!")
```

In the code above, we've called the lambda with the `String` `"Hello, world!"` and stored the result in the `result` variable.

### Lambdas with Multiple Parameters

Lambdas with multiple parameters are defined using the parameter names. For example, the following is a lambda that takes two `Int`s and returns the sum of those `Int`s:

```kotlin
val lambda = { x: Int, y: Int ->
    x + y
}
```

In the code above, we've defined a lambda that takes two `Int`s and returns the sum of those `Int`s. We can then call that lambda like this:

```kotlin
val result = lambda(1, 2)
```

In the code above, we've called the lambda with the `Int`s `1` and `2` and stored the result in the `result` variable.

### Lambdas with No Parameters

Lambdas with no parameters are defined using the `()` syntax. For example, the following is a lambda that returns the string `"Hello, world!"`:

```kotlin
val lambda = {
    "Hello, world!"
}
```

In the code above, we've defined a lambda that returns the string `"Hello, world!"`. We can then call that lambda like this:

```kotlin
val result = lambda()
```

In the code above, we've called the lambda and stored the result in the `result` variable.

## Conclusion

Lambdas are a powerful tool in Kotlin that can help you write concise and effective code. In this article, we've seen what lambdas are, how they work, and how to use them effectively in your code.