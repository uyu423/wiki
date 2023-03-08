---
title: About first-class/higher-order functions in Kotlin lambdas
description: 
published: true
date: 2023-02-17T18:00:13.654Z
tags: kotlin, lambda, english
editor: markdown
dateCreated: 2022-12-24T19:24:06.482Z
---

- [코틀린 람다의 일급 함수 / 고차 함수에 대해***Korean** version of this document is available*](/ko/dev/Kotlin/About-first-class-and-higher-order-functions-in-Kotlin-lambdas)
{.links-list}

---

- In Kotlin, functions are first-class citizens, which means that they can be treated like any other value. This includes the ability to store them in variables, pass them as arguments to other functions, and return them as results from functions.

- Here's an example of a function in Kotlin that takes a lambda expression as an argument and returns it as a result:

```kotlin
fun makeAdder(x: Int): (Int) -> Int {
    return { y -> x + y }
}
```

- In this example, the makeAdder function takes an Int argument and returns a lambda expression that adds the argument to its own input. The returned lambda expression is a function that takes an Int argument and returns an Int result.

- Higher-order functions are functions that take other functions as arguments or return them as results. In the example above, the makeAdder function is a higher-order function because it takes a lambda expression as an argument and returns it as a result.

- Higher-order functions are a powerful feature of functional programming languages because they allow you to abstract over operations and create more flexible and reusable code. For example, you can use a higher-order function to create a generic function that can perform a variety of operations on a list of elements, depending on the function passed to it as an argument.

- In Kotlin, lambda expressions are often used with higher-order functions to create flexible and reusable code. For example, you can use the map function to apply a lambda expression to each element of a list and return a new list with the transformed elements:

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val squares = numbers.map { it * it }
```

- In this example, the map function is a higher-order function that takes a lambda expression as an argument and returns a new list with the transformed elements. The lambda expression is applied to each element of the original list and returns the square of the element. The resulting list contains the squares of the original elements.

### Appendix: Is it impossible to implement a higher-order function in Java's lambda?

- It is possible to implement a higher-order function in Java using lambda expressions. A higher-order function is a function that takes other functions as arguments or returns them as results.

- To implement a higher-order function in Java, you can use functional interfaces (interfaces with a single abstract method) to represent the functions being passed as arguments or returned as results. For example, consider the following functional interface and higher-order function in Java:

```java
@FunctionalInterface
interface Function<T, R> {
    R apply(T t);
}

@FunctionalInterface
interface HigherOrderFunction<T, R> {
    Function<T, R> makeAdder(T x);
}
```

- In this example, the Function interface represents a function that takes a single argument of type T and returns a result of type R. The HigherOrderFunction interface represents a higher-order function that takes a single argument of type T and returns a Function object that takes an argument of type T and returns a result of type R.

- You can use lambda expressions to implement these functional interfaces and create higher-order functions in Java. For example, here's how you could use a lambda expression to implement the HigherOrderFunction interface and create a higher-order function that returns a function that adds a fixed value to its input:

```java
HigherOrderFunction<Integer, Integer> makeAdder = (x) -> (y) -> x + y;
```

- In this example, the lambda expression (y) -> x + y represents a function that takes an Integer argument y and returns the result of adding x to y. The outer lambda expression (x) -> (y) -> x + y represents a higher-order function that takes an Integer argument x and returns the inner lambda expression as a Function object.

- Overall, it is possible to implement higher-order functions in Java using lambda expressions and functional interfaces. However, the syntax for creating and using higher-order functions in Java can be more verbose and cumbersome than in languages with better support for functional programming, such as Kotlin.

> ***Yowu's Notes*** 😎
> Looking back at my little Java development experience so far, it doesn't seem impossible to implement first-class and higher-order functions in Java code.
> However, based on my experience so far, I didn't have to implement first-class/higher-order functions in production code that much, and in most cases, if I tried to implement them similarly to javascript, the complexity of the code unnecessarily increased, such as the body.
> So, if you want to use lambda as a first-class/higher-order function in earnest, using Kotlin seems to be beneficial to your mental health.

![kotlin.jpeg](/kotlin.jpeg =500x){.align-center}