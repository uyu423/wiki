---
title: Features of Kotlin
description: 
published: true
date: 2023-02-17T18:00:10.921Z
tags: kotlin
editor: markdown
dateCreated: 2022-12-24T19:07:03.704Z
---

- [코틀린 특징***Korean** version of this document is available*](/ko/dev/Kotlin/feature-of-kotlin)
{.links-list}

Kotlin and Java are both popular programming languages that are used to build a wide variety of applications. They have many similarities, but there are also some key differences between the two languages. Here's a comparison of the main features of Kotlin and Java:

### Syntax

- Kotlin has a more concise and expressive syntax than Java, which makes it easier to read and write. Kotlin has features such as type inference, simplified return syntax, and support for data classes, which reduce the amount of boilerplate code that is required.

- Kotlin does not have the `public`, `private`, and `protected` keywords for modifying the visibility of class members. Instead, it uses the `internal`, `private`, and `protected` keywords, and the default visibility is `public`.

- Kotlin does not have the `void` keyword for indicating that a function does not return a value. Instead, you can use the Unit type or omit the return type entirely if the function does not return a value.

- Kotlin does not have the `new` keyword for creating objects. Instead, you can use the object keyword or the constructor keyword to create an instance of a class.

- Kotlin has a more concise syntax for defining classes, functions, and variables. For example, you can define a class with a primary constructor and field declarations in a single line of code, like this:

```kt
class User(val name: String, val age: Int)
```

- Kotlin has a more expressive syntax for loops and control flow. For example, you can use the `when` expression as a concise alternative to the `switch` statement, and you can use the `for-loop` to iterate over ranges and collections.


```kt
val x = 10
when (x) {
    0 -> print("x is zero")
    in 1..9 -> print("x is between 1 and 9")
    else -> print("x is something else")
}
```

```kt
for (i in 1..10) {
    print(i)
}

val names = listOf("Alice", "Bob", "Charlie")
for (name in names) {
    print(name)
}
```

- Kotlin has a more concise syntax for creating anonymous inner classes. Instead of using the `new` keyword and the `implements` or `extends` keywords, you can use a lambda expression or a function reference to create an instance of an interface or a class.

### Null safety

- Kotlin has built-in support for null safety, which means it can distinguish between nullable and non-nullable types. This helps prevent null reference exceptions, which are common in Java. Here's an example of how you can declare a `nullable` variable in Kotlin:

```kt
val name: String? = null
```

- In Java, you can use the `@Nullable` and `@NotNull` annotations from the `javax.annotation` package to achieve a similar effect, but it is not built into the language.

### Data Classes

- Kotlin has a concise syntax for defining data classes, which are classes that hold data without any additional logic. In Kotlin, you can define a data class like this:

```kt
data class User(val name: String, val age: Int)
```

- In Java, you would need to write a lot more code to achieve the same effect. You would need to define the class, the fields, the `getters` and `setters`, and override the `equals()`, `hashCode()`, and `toString()` methods.

### Extension Functions

- Kotlin allows you to add new functions to existing classes without having to inherit from them or use design patterns like decorators. This is done using extension functions. Here's an example of how you can define an extension function in Kotlin:

```kt
fun String.isPalindrome(): Boolean {
    return this == this.reversed()
}
```

- In Java, you would need to either use inheritance or a utility class with static methods to achieve the same effect.

###  Type Inference

- Kotlin has improved type inference compared to Java, which means the compiler is able to infer the types of variables and expressions based on the context in which they are used. This can make your code more concise and easier to read. For example, in Kotlin you can define a variable like this:

```kt
val name = "John"
```

- The type of the `name` variable is inferred to be `String`, so you don't have to specify it explicitly. In Java, you would need to write `String name = "John";` to achieve the same effect.

### Functional programming

- Kotlin supports functional programming constructs such as higher-order functions, lambdas, and function types. This makes it easier to write code that is concise, expressive, and easy to reason about. Here's an example of how you can use a higher-order function in Kotlin:

```kt
fun processData(data: List<Int>, processor: (Int) -> Int): List<Int> {
    return data.map(processor)
}
```

- This is a function that takes a list of integers and a processor function as arguments, and applies the processor function to each element of the list. The processor function is a lambda that takes an integer and returns an integer.

### Concurrency (Coroutines)

- Kotlin has built-in support for concurrency through the `kotlinx.coroutines` library. Coroutines allow you to write asynchronous, non-blocking code in a sequential style, which can make it easier to write code that performs tasks in the background without blocking the main thread. Here's an example of how you can use coroutines in Kotlin:

```kt
suspend fun loadData(): Data {
    // perform asynchronous tasks here
}
```

- The `suspend` keyword indicates that this function is a coroutine, and the code inside the function can be suspended and resumed later. You can use the `async` function to launch a coroutine and get a `Deferred` object, which you can use to access the result of the coroutine when it is complete.

```kt
val deferredData = async { loadData() }
val data = deferredData.await()
```

- In this example, the `async` function launches a coroutine that calls the `loadData()` function, and the `await()` function waits for the coroutine to complete and returns the result.

- In Java, you would need to use a library or framework like `RxJava` or `CompletableFuture` to achieve the same effect.

### Interoperability with Java

- Kotlin is fully interoperable with Java, which means you can use Kotlin and Java code together in the same project. You can even call Kotlin code from Java and vice versa. This makes it easy to incorporate Kotlin into existing Java projects, or to gradually migrate a Java codebase to Kotlin.

> Overall, Kotlin is a modern programming language that builds on the strengths of Java, while addressing some of its weaknesses. Kotlin has a more concise and expressive syntax, better support for null safety and functional programming, and good interoperability with Java. It also has additional features for concurrency and other advanced programming scenarios.

![kotlin.jpeg](/kotlin.jpeg =500x){.align-center}
