---
title: 052: Nullability and Null Safety in Kotlin: Managing Null Values in Your Code
description: 
published: true
date: 2023-02-14T03:17:36.796Z
tags: 
editor: markdown
dateCreated: 2023-02-14T03:17:29.685Z
---

- [052: Nullability y Null Safety en Kotlin: Gestión de valores nulos en su código***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/052-nullability-and-null-safety-in-kotlin-managing-null-values-in-your-code)
{.links-list}
- [052：Kotlin 中的可空性和空安全性：管理代码中的空值***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/052-nullability-and-null-safety-in-kotlin-managing-null-values-in-your-code)
{.links-list}
- [052: Kotlin의 Null 허용 및 Null 안전성: 코드에서 Null 값 관리***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/052-nullability-and-null-safety-in-kotlin-managing-null-values-in-your-code)
{.links-list}


## Introduction

Kotlin is a statically typed programming language that runs on the Java Virtual Machine. It is a JVM language that is interoperable with Java and can be used to develop Android apps.

One of the key features of Kotlin is null safety. Null safety is the ability to avoid NullPointerException. Kotlin achieves null safety by using nullable and non-null types.

Nullable types can hold a null value, while non-null types cannot. This means that if you try to assign a null value to a non-null type, you will get a compile-time error.

## Nullable and Non-Null Types

Kotlin has two types of nullable and non-null types:

* **Nullable type**: A type that can hold a null value. Kotlin uses the ? (question mark) to denote a nullable type.

* **Non-null type**: A type that cannot hold a null value. Kotlin uses the !! (double exclamation mark) to denote a non-null type.

Here is an example of how to declare a nullable and a non-null type:

```kotlin
// Nullable type
var name: String? = "John"

// Non-null type
var age: Int = 20
```

As you can see, the nullable type is declared with a ? after the type name, while the non-null type is declared without a ?.

## Assigning Null Values

You can assign a null value to a nullable type, but you cannot assign a null value to a non-null type.

If you try to assign a null value to a non-null type, you will get a compile-time error.

Here is an example of how to assign a null value to a nullable type:

```kotlin
var name: String? = "John"

name = null
```

As you can see, we have declared a nullable type and assigned a null value to it. This is allowed because the type is nullable.

However, if we try to do the same with a non-null type, we will get a compile-time error:

```kotlin
var age: Int = 20

age = null // This will give a compile-time error
```

## Checking for Null Values

You should always check for null values before using them. Kotlin provides the ?. (safe call operator) and the !! (not-null assertion operator) to help you check for null values.

The ?. operator checks if the value is null before accessing it. If the value is null, it will return null. Otherwise, it will return the value.

Here is an example of how to use the ?. operator:

```kotlin
var name: String? = "John"

// This will print "John"
println(name?.length)

name = null

// This will print "null"
println(name?.length)
```

As you can see, we have checked if the name variable is null before accessing its length property. If the name variable is null, the ?. operator will return null. Otherwise, it will return the value.

The !! operator is used to force-unwrap a value. This means that it will return the value even if it is null.

This can be dangerous because it can lead to a NullPointerException if the value is actually null.

Here is an example of how to use the !! operator:

```kotlin
var name: String? = "John"

// This will print "John"
println(name!!.length)

name = null

// This will give a NullPointerException
println(name!!.length)
```

As you can see, we have used the !! operator to force-unwrap the name variable. Even though the name variable is null, the !! operator will still return the value.

However, if we try to access the length property of the name variable, we will get a NullPointerException because the name variable is actually null.

## Conclusion

In this post, we have learned about null safety in Kotlin. We have learned about nullable and non-null types and how to assign null values to them. We have also learned about the ?. and !! operators and how to use them to check for null values.