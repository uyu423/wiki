---
title: Exploring Null Safety in Kotlin
description: 
published: true
date: 2023-02-17T23:06:47.756Z
tags: 
editor: markdown
dateCreated: 2023-02-17T23:06:40.940Z
---

- [Kotlin의 Null 안전 탐색***Korean** document is available*](/ko/Knowledge-base/Kotlin/exploring-null-safety-in-kotlin)
{.links-list}


# Exploring Null Safety in Kotlin

Kotlin is a statically typed programming language that runs on the Java Virtual Machine and can also be compiled to JavaScript source code. It is an open source project under the Apache 2.0 license. Kotlin is heavily inspired by Java, and it is intended to be a more concise, safer, and more expressive alternative to Java. 

One of Kotlin's most notable features is its null safety, which is designed to eliminate the risk of NullPointerException errors (often referred to as the "billion dollar mistake"). In Kotlin, all types are non-nullable by default, which means that a variable of type String can never hold null. However, nullable types can be declared by adding a question mark to the type, like this:

```kotlin
var s: String? = null
```

Now the variable s can hold either a string or null. When a variable can hold null, we say that it is nullable.

If we try to access a nullable variable without first checking if it is null, we will get a compiler error. For example, the following code will not compile:

```kotlin
var s: String? = null
println(s.length) // error: variable s can be null
```

To access a nullable variable, we first need to check if it is null. We can do this using the ? operator, like this:

```kotlin
var s: String? = null
println(s?.length) // prints null if s is null, otherwise prints s.length
```

Now the code will compile, but it will print null if the variable s is null. If we want to do something else if the variable is null, we can use the elvis operator, which is written as ?:. For example, we could print a default length if the variable is null, like this:

```kotlin
var s: String? = null
println(s?.length ?: 0) // prints 0 if s is null, otherwise prints s.length
```

If we want to access a nullable variable without first checking if it is null, we can use the !! operator, which will throw an exception if the variable is null. For example, the following code will throw an exception if the variable s is null:

```kotlin
var s: String? = null
println(s!!.length) // throws an exception if s is null
```

## Nullable Types

As we saw before, nullable types are declared by adding a question mark to the type. For example, the following variable can hold either a string or null:

```kotlin
var s: String? = null
```

We can also have nullable types for other types, like numbers, booleans, and more. For example, the following variable can hold either a number or null:

```kotlin
var n: Int? = null
```

Nullable types are useful when we want to represent the absence of a value. For example, consider a function that converts a string to a number. If the string cannot be converted to a number, we might want to return null:

```kotlin
fun parseInt(s: String): Int? {
    // ...
}
```

We can call this function like this:

```kotlin
val n = parseInt("42")
```

Now the variable n will hold the number 42 if the string can be parsed, or null if it cannot.

We can also have nullable types for collections. For example, the following variable can hold either a list of strings or null:

```kotlin
var list: List<String>? = null
```

Nullable types are useful when we want to represent the absence of a value, but they can also be dangerous. For example, consider the following code:

```kotlin
fun printLength(s: String?) {
    println(s?.length ?: 0)
}

printLength(null) // prints 0
printLength("abc") // prints 3
```

This code will compile and run without problems, but it will print the wrong result if we pass null. Instead of printing 0, it will print null. This is because the elvis operator will return the right-hand side if the left-hand side is null, and the right-hand side of the elvis operator is 0.

To fix this, we can use the let function, which will only execute the code inside the function if the variable is not null:

```kotlin
fun printLength(s: String?) {
    s?.let {
        println(it.length)
    }
}

printLength(null) // prints nothing
printLength("abc") // prints 3
```

Now the code will only print the length of the string if the string is not null.

## Non-Nullable Types

As we saw before, all types are non-nullable by default in Kotlin. This means that a variable of type String can never hold null. However, we can still have nullable types by adding a question mark to the type, like this:

```kotlin
var s: String? = null
```

Now the variable s can hold either a string or null.

Non-nullable types are useful when we want to represent the presence of a value. For example, consider a function that converts a string to a number. If the string cannot be converted to a number, we might want to return -1:

```kotlin
fun parseInt(s: String): Int {
    // ...
}
```

We can call this function like this:

```kotlin
val n = parseInt("42")
```

Now the variable n will hold the number 42 if the string can be parsed, or -1 if it cannot.

We can also have non-nullable types for collections. For example, the following variable can hold either a list of strings or an empty list:

```kotlin
var list: List<String> = emptyList()
```

Non-nullable types are useful when we want to represent the presence of a value, but they can also be dangerous. For example, consider the following code:

```kotlin
fun printLength(s: String) {
    println(s.length)
}

printLength(null) // error: variable s cannot be null
printLength("abc") // prints 3
```

This code will not compile because the variable s is declared as a non-nullable type. To fix this, we can use the let function, which will only execute the code inside the function if the variable is not null:

```kotlin
fun printLength(s: String) {
    s.let {
        println(it.length)
    }
}

printLength(null) // error: variable s cannot be null
printLength("abc") // prints 3
```

Now the code will only print the length of the string if the string is not null.

## Conclusion

Null safety is an important feature of Kotlin that can help us avoid NullPointerException errors. Nullable types are useful when we want to represent the absence of a value, and non-nullable types are useful when we want to represent the presence of a value. However, both nullable and non-nullable types can be dangerous if we're not careful.