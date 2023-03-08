---
title: 008: Null Safety in Kotlin: Understanding the ? Operator and Non-Null Types
description: 
published: true
date: 2023-01-31T05:24:40.639Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:24:37.191Z
---

- [008: Kotlin의 Null 안전: ? 연산자 및 Null이 아닌 유형***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/008-null-safety-in-kotlin-understanding-the--operator-and-non-null-types)
{.links-list}
- [008: Kotlin の Null 安全性: ? を理解する演算子と非 null 型***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/008-null-safety-in-kotlin-understanding-the--operator-and-non-null-types)
{.links-list}
- [008：Kotlin 中的空安全：理解 ?运算符和非空类型***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/008-null-safety-in-kotlin-understanding-the--operator-and-non-null-types)
{.links-list}




# Null Safety in Kotlin: Understanding the ? Operator and Non-Null Types

Kotlin is a statically typed programming language that runs on the JVM. It is fully interoperable with Java and is often used as an alternative to Java for Android development. Null safety is one of the key features of Kotlin. It eliminates the risk of null pointer exceptions, which can be a major source of errors in Java programs.

In Kotlin, every variable must be declared as either nullable or non-null. A nullable variable can hold a null value, whereas a non-null variable cannot. This is enforced at compile time, so it is not possible to assign a null value to a non-null variable.

The key to understanding null safety in Kotlin is the ? operator. This operator is used to mark a variable as nullable. For example, the following variable can hold either a null or non-null value:

```kotlin
var str: String? = "Hello, world!"
```

The type of a nullable variable is denoted by adding a ? after the type name. In the example above, the type of the variable is String?.

If you try to access a nullable variable without first checking if it is null, you will get a compile time error. For example, the following code will not compile:

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str.length)
}
```

The compiler knows that str could be null, so it will not allow you to call the length property on it. To fix this, you need to check if str is null before accessing it:

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    if (str != null) {
        println(str.length)
    }
}
```

Alternatively, you can use the ? operator to safely access a nullable variable. This will check if the variable is null before accessing it. If it is null, the whole expression will evaluate to null. For example:

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str?.length)
}
```

In the above code, the expression str?.length will evaluate to null if str is null. Otherwise, it will evaluate to the length of the string.

It is also possible to use the ? operator to specify a default value to use if the variable is null. For example:

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str?.length ?: 0)
}
```

In the above code, if str is null, the expression will evaluate to 0. Otherwise, it will evaluate to the length of the string.

It is often useful to create a non-null type from a nullable type. This can be done using the !! operator. This operator will convert a nullable type to a non-null type. However, if the nullable type is actually null, it will throw an exception. For example:

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str!!.length)
}
```

In the above code, if str is null, an exception will be thrown. Otherwise, the length of the string will be printed.

It is also possible to use the ? operator with the !! operator. This will first check if the nullable variable is null. If it is null, it will return null. Otherwise, it will convert the nullable variable to a non-null type and return it. For example:

```kotlin
fun main(args: Array<String>) {
    var str: String? = "Hello, world!"
    println(str?.length ?: 0)
}
```

In the above code, if str is null, the expression will evaluate to null. Otherwise, it will evaluate to the length of the string.

Null safety is an important feature of Kotlin that can help you to avoid null pointer exceptions. By carefully using the ? operator, you can make your code more robust and avoid these types of errors.