---
title: Closures in Functional Programming with Kotlin Lambda Expressions
description: 
published: true
date: 2023-02-17T18:00:12.240Z
tags: kotlin, closure, lambda, english
editor: markdown
dateCreated: 2022-12-24T19:15:11.615Z
---


- [코틀린 람다 표현식으로 살펴보는 함수형 프로그래밍의 클로져(Closure)***Korean** version of this document is available*](/ko/dev/Kotlin/Kotlin-labmda-functional-programming-closures)
{.links-list}

---

- In functional programming, a closure is a function that refers to free variables (variables that are not bound in the current scope) in its body. A closure is a function that retains the ability to access and modify the variables that were in its lexical scope, even when the function is executed outside of that lexical scope.


- In Kotlin, a lambda is an anonymous function that can be created and passed around like any other object. A lambda can capture variables from the surrounding scope, and these variables are known as the closure's free variables.


- Here's an example of a Kotlin lambda that captures a free variable:

```kotlin
val greeting = "Hello"
val sayHello = { name: String ->
    println("$greeting, $name!")
}

sayHello("John")  // prints "Hello, John!"
```

- In this example, the lambda sayHello captures the free variable greeting. The lambda can access and modify the value of greeting even though it is defined outside the lambda's lexical scope.

- Closures are useful in functional programming because they allow functions to be created and passed around as values, just like any other object. This enables a wide range of programming patterns, such as higher-order functions (functions that take other functions as arguments) and partial application (creating a new function by fixing some of the arguments to a function).

- For example, consider the following higher-order function in Kotlin:

```kotlin
fun repeat(times: Int, action: (Int) -> Unit) {
    for (i in 1..times) {
        action(i)
    }
}
```

- This function takes an integer times and a function action as arguments, and it calls the function times number of times, passing the current iteration number as an argument. The function action can be any function that takes an integer as an argument and returns nothing.

- Here's an example of how this higher-order function can be used with a lambda:

```kotlin
repeat(5) { i ->
    println("Iteration $i")
}
```

This code will print the following output:

```text
Iteration 1
Iteration 2
Iteration 3
Iteration 4
Iteration 5
```

- In this example, the lambda { i -> println("Iteration $i") } captures no free variables, so it is a pure function. However, if the lambda captured a free variable, it would become a closure, and the value of the free variable could be accessed and modified within the lambda.

### Summary

- In functional programming, a closure is a function that refers to free variables in its body. A free variable is a variable that is not bound in the current scope, but is instead defined in an enclosing scope.
- In Kotlin, a lambda is an anonymous function that can capture variables from the surrounding scope and use them as free variables.
- Closures are useful in functional programming because they allow functions to be created and passed around as values, enabling programming patterns such as higher-order functions and partial application.
- A higher-order function is a function that takes other functions as arguments and returns a function as a result. Partial application is the process of creating a new function by fixing some of the arguments to a function.
- In functional programming, partial application is the process of creating a new function by fixing some of the arguments to a function. This allows you to create specialized versions of a function with some of the arguments already set, without having to specify all of the arguments every time the function is called.
- Closures can be pure functions (functions that do not capture any free variables) or functions that capture free variables and can access and modify their values.

> **Appendix: Partial Application vs Currying**
> 
> both partial application and currying involve creating new functions by fixing some of the arguments to a function. However, partial application involves creating a new function by fixing some of the arguments to a function without specifying all of the arguments, while currying involves breaking down a function into a chain of functions that each take a single argument.
> 
> *Example of partial application:*
> ```kt
> fun add(x: Int, y: Int): Int {
>     return x + y
> }
> 
> val addFive = { x: Int -> add(5, x) }
> 
> println(addFive(3))  // prints 8
> println(addFive(10))  // prints 15
> ```
> In this example, the function add takes two integer arguments and returns their sum. The lambda addFive is a partially applied function that fixes the first argument to 5 and takes the second argument as a parameter. When addFive is called with an argument x, it calls the function add with 5 as the first argument and x as the second argument, and returns the result.
> 
> *Example of currying:*
> ```kt
> fun add(x: Int): (Int) -> (Int) -> Int {
>    return { y: Int -> { z: Int -> x + y + z } }
> }
>
> val addThreeNumbers = add(1)(2)(3)  // addThreeNumbers is 6
> ```
> In this example, the function add takes a single integer argument x and returns a new function that takes a single integer argument y. This new function returns yet another function that takes a single integer argument z. When the innermost function is called with an argument z, it adds x, y, and z and returns the result.
> 
> The lambda addThreeNumbers is a partially applied function that fixes the first argument to 1, the second argument to 2, and the third argument to 3. When addThreeNumbers is called, it returns the result of adding 1, 2, and 3, which is 6. It can also be seen as a continuous 'Partial Application' where one parameter is fixed each time.

![kotlin.jpeg](/kotlin.jpeg =500x){.align-center}