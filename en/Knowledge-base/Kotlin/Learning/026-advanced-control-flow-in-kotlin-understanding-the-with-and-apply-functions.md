---
title: 026: Advanced Control Flow in Kotlin: Understanding the with and apply Functions
description: 
published: true
date: 2023-02-14T06:55:50.143Z
tags: 
editor: markdown
dateCreated: 2023-02-14T06:55:48.277Z
---

- [026: Flujo de control avanzado en Kotlin: comprensión de las funciones with y apply***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/026-advanced-control-flow-in-kotlin-understanding-the-with-and-apply-functions)
{.links-list}
- [026：Kotlin 中的高级控制流：了解 with 和 apply 函数***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/026-advanced-control-flow-in-kotlin-understanding-the-with-and-apply-functions)
{.links-list}
- [026: Kotlin의 고급 제어 흐름: with 및 apply 함수 이해***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/026-advanced-control-flow-in-kotlin-understanding-the-with-and-apply-functions)
{.links-list}


#026: Advanced Control Flow in Kotlin: Understanding the with and apply Functions

As a Kotlin programmer, it's important to understand the different ways to control the flow of your program. In this post, we'll take a look at two functions that are often used together: with and apply. We'll learn when and how to use them, and we'll see some examples of how they can be used to improve our code.

##What are the with and apply Functions?

The with and apply functions are both functions that take a receiver as an argument. The receiver is the object on which the function is called. The with function returns the receiver, while the apply function returns the result of the lambda that is passed to it.

##When Should I Use with and apply?

You can use the with and apply functions whenever you want to perform multiple operations on the same object. They are often used together because they allow you to concisely write code that would be more verbose if you used regular function calls.

For example, let's say we have a class called User with several properties:

```kotlin
class User(
    val name: String,
    val age: Int,
    val address: String
)
```

And we have an instance of this class:

```kotlin
val user = User("John", 30, "123 Main Street")
```

We can use the with function to perform multiple operations on the user object:

```kotlin
with(user) {
    // do something with the user object
}
```

We can also use the apply function to perform multiple operations on the user object:

```kotlin
user.apply {
    // do something with the user object
}
```

##Examples of Using with and apply

Let's take a look at some examples of how we can use with and apply to improve our code.

###1. Creating and Initializing an Object

One common use case for with and apply is creating and initializing an object. Let's say we have a class called Car with several properties:

```kotlin
class Car(
    val make: String,
    val model: String,
    val year: Int,
    val color: String
)
```

We can use with to create a new instance of this class and initialize its properties:

```kotlin
val car = with(Car("Toyota", "Camry", 2020, "red")) {
    // do something with the car object
}
```

We can also use apply to create a new instance of this class and initialize its properties:

```kotlin
val car = Car("Toyota", "Camry", 2020, "red").apply {
    // do something with the car object
}
```

###2. Accessing and Modifying Properties

Another common use case for with and apply is accessing and modifying the properties of an object. Let's say we have a class called Person with several properties:

```kotlin
class Person(
    var name: String,
    var age: Int,
    var address: String
)
```

And we have an instance of this class:

```kotlin
val person = Person("John", 30, "123 Main Street")
```

We can use with to access and modify the properties of the person object:

```kotlin
with(person) {
    name = "Jane"
    age = 31
    address = "456 Main Street"
}
```

We can also use apply to access and modify the properties of the person object:

```kotlin
person.apply {
    name = "Jane"
    age = 31
    address = "456 Main Street"
}
```

###3. Calling Multiple Methods on an Object

Another common use case for with and apply is calling multiple methods on the same object. Let's say we have a class called Employee with several methods:

```kotlin
class Employee(
    val name: String,
    val age: Int,
    val address: String
) {
    fun work() {
        // do some work
    }

    fun takeBreak() {
        // take a break
    }

    fun goHome() {
        // go home
    }
}
```

And we have an instance of this class:

```kotlin
val employee = Employee("John", 30, "123 Main Street")
```

We can use with to call multiple methods on the employee object:

```kotlin
with(employee) {
    work()
    takeBreak()
    goHome()
}
```

We can also use apply to call multiple methods on the employee object:

```kotlin
employee.apply {
    work()
    takeBreak()
    goHome()
}
```

##Additional Information

Here are some additional resources for learning more about the with and apply functions:

- The with function is a higher-order function that is declared in the Kotlin standard library [here](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-with/index.html).
- The apply function is a member function of the Any class that is declared [here](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-any/apply.html).
- The with and apply functions are described in the Kotlin documentation [here](https://kotlinlang.org/docs/reference/lambdas.html#with-and-apply).

##Conclusion

In this post, we've learned about the with and apply functions. We've seen when and how to use them, and we've seen some examples of how they can be used to improve our code.