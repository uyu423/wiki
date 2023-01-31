---
title: 008: Null Safety in Kotlin: Understanding the ? Operator and Non-Null Types
description: 
published: true
date: 2023-01-31T05:14:06.918Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:14:06.918Z
---

- [008: Kotlin의 Null 안전: ? 연산자 및 Null이 아닌 유형***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/008-null-safety-in-kotlin-understanding-the--operator-and-non-null-types)
{.links-list}
- [008: Kotlin の Null 安全性: ? を理解する演算子と非 null 型***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/008-null-safety-in-kotlin-understanding-the--operator-and-non-null-types)
{.links-list}
- [008：Kotlin 中的空安全：理解 ?运算符和非空类型***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/008-null-safety-in-kotlin-understanding-the--operator-and-non-null-types)
{.links-list}


# Null safety in Kotlin: understanding the ? operator and non-null types

Kotlin's null safety is one of its key features that distinguishes it from Java. Null safety in Kotlin is designed to eliminate the risk of null pointer exceptions, which are common in Java programs.

In Kotlin, every variable must be declared as either a non-null type or a nullable type. A non-null type can never be assigned a null value, whereas a nullable type can be assigned a null value.

The ? operator is used to declare a variable as a nullable type. For example, the following variable is a nullable type:

```kotlin
var myVar: String? = "Hello"
```

If you try to assign a null value to a non-null type, you will get a compilation error:

```kotlin
var myVar: String = "Hello"
myVar = null // compilation error
```

You can use the ? operator to safely access a nullable type. The ? operator will check if the variable is null before accessing it. If the variable is not null, the ? operator will return the value; if the variable is null, the ? operator will return null.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
println(myVar?.length) // prints "Hello"

myVar = null
println(myVar?.length) // prints "null"
```

If you try to access a nullable type without using the ? operator, you will get a null pointer exception:

```kotlin
var myVar: String? = "Hello"
println(myVar.length) // NullPointerException
```

The !! operator can be used to force-access a nullable type. This will cause a null pointer exception if the variable is null:

```kotlin
var myVar: String? = "Hello"
println(myVar!!.length) // prints "Hello"

myVar = null
println(myVar!!.length) // NullPointerException
```

The ?: operator is called the null-coalescing operator. This operator can be used to provide a default value for a nullable type. For example, the following code will print "Hello" if myVar is not null, and will print "World" if myVar is null:

```kotlin
var myVar: String? = "Hello"
println(myVar ?: "World") // prints "Hello"

myVar = null
println(myVar ?: "World") // prints "World"
```

You can use the Elvis operator (?:) to safely access a nullable type. This will check if the variable is null before accessing it. If the variable is not null, the Elvis operator will return the value; if the variable is null, the Elvis operator will return the default value.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
println(myVar ?: "null") // prints "Hello"

myVar = null
println(myVar ?: "null") // prints "null"
```

The !! operator can be used to force-access a nullable type. This will cause a null pointer exception if the variable is null:

```kotlin
var myVar: String? = "Hello"
println(myVar!!) // prints "Hello"

myVar = null
println(myVar!!) // NullPointerException
```

You can use the let function to safely access a nullable type. The let function will check if the variable is null before accessing it. If the variable is not null, the let function will invoke the lambda function with the variable as the parameter; if the variable is null, the let function will do nothing.

For example, the following code will print "Hello" if myVar is not null, and will not print anything if myVar is null:

```kotlin
var myVar: String? = "Hello"
myVar?.let { println(it) } // prints "Hello"

myVar = null
myVar?.let { println(it) } // does nothing
```

You can use thealso function to safely access a nullable type. The also function will check if the variable is null before accessing it. If the variable is not null, the also function will invoke the lambda function with the variable as the parameter; if the variable is null, the also function will return null.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
myVar?.also { println(it) } // prints "Hello"

myVar = null
myVar?.also { println(it) } // prints "null"
```

You can use the let and also functions together to safely access a nullable type. The let function will check if the variable is null before accessing it. If the variable is not null, the let function will invoke the lambda function with the variable as the parameter; if the variable is null, the let function will do nothing. The also function will check if the result of the lambda function is null before returning it. If the result of the lambda function is not null, the also function will return the result; if the result of the lambda function is null, the also function will return null.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
myVar?.let { it.also { println(it) } } // prints "Hello"

myVar = null
myVar?.let { it.also { println(it) } } // prints "null"
```

You can use the takeIf function to safely access a nullable type. The takeIf function will check if the variable is null before accessing it. If the variable is not null, the takeIf function will invoke the lambda function with the variable as the parameter; if the variable is null, the takeIf function will return null.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
myVar?.takeIf { it == "Hello" }?.also { println(it) } // prints "Hello"

myVar = null
myVar?.takeIf { it == "Hello" }?.also { println(it) } // prints "null"
```

You can use the takeUnless function to safely access a nullable type. The takeUnless function will check if the variable is null before accessing it. If the variable is not null, the takeUnless function will invoke the lambda function with the variable as the parameter; if the variable is null, the takeUnless function will return the variable.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
myVar?.takeUnless { it == "Hello" }?.also { println(it) } // prints "null"

myVar = null
myVar?.takeUnless { it == "Hello" }?.also { println(it) } // prints "null"
```

You can use the run function to safely access a nullable type. The run function will check if the variable is null before accessing it. If the variable is not null, the run function will invoke the lambda function with the variable as the receiver; if the variable is null, the run function will return null.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
myVar?.run { println(this) } // prints "Hello"

myVar = null
myVar?.run { println(this) } // prints "null"
```

You can use the with function to safely access a nullable type. The with function will check if the variable is null before accessing it. If the variable is not null, the with function will invoke the lambda function with the variable as the receiver; if the variable is null, the with function will return null.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
with(myVar) { println(this) } // prints "Hello"

myVar = null
with(myVar) { println(this) } // prints "null"
```

You can use the apply function to safely access a nullable type. The apply function will check if the variable is null before accessing it. If the variable is not null, the apply function will invoke the lambda function with the variable as the receiver and return the result; if the variable is null, the apply function will return null.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
myVar?.apply { println(this) } // prints "Hello"

myVar = null
myVar?.apply { println(this) } // prints "null"
```

You can use the also function to safely access a nullable type. The also function will check if the variable is null before accessing it. If the variable is not null, the also function will invoke the lambda function with the variable as the parameter and return the variable; if the variable is null, the also function will return null.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
myVar?.also { println(it) } // prints "Hello"

myVar = null
myVar?.also { println(it) } // prints "null"
```

You can use the map function to safely access a nullable type. The map function will check if the variable is null before accessing it. If the variable is not null, the map function will invoke the lambda function with the variable as the receiver and return the result; if the variable is null, the map function will return null.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
myVar?.map { it.toUpperCase() }?.also { println(it) } // prints "HELLO"

myVar = null
myVar?.map { it.toUpperCase() }?.also { println(it) } // prints "null"
```

You can use the let function to safely access a nullable type. The let function will check if the variable is null before accessing it. If the variable is not null, the let function will invoke the lambda function with the variable as the parameter and return the result; if the variable is null, the let function will return null.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
myVar?.let { it.toUpperCase() }?.also { println(it) } // prints "HELLO"

myVar = null
myVar?.let { it.toUpperCase() }?.also { println(it) } // prints "null"
```

You can use the run function to safely access a nullable type. The run function will check if the variable is null before accessing it. If the variable is not null, the run function will invoke the lambda function with the variable as the receiver and return the result; if the variable is null, the run function will return null.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
myVar?.run { toUpperCase() }?.also { println(it) } // prints "HELLO"

myVar = null
myVar?.run { toUpperCase() }?.also { println(it) } // prints "null"
```

You can use the with function to safely access a nullable type. The with function will check if the variable is null before accessing it. If the variable is not null, the with function will invoke the lambda function with the variable as the receiver and return the result; if the variable is null, the with function will return null.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
with(myVar) { toUpperCase() }?.also { println(it) } // prints "HELLO"

myVar = null
with(myVar) { toUpperCase() }?.also { println(it) } // prints "null"
```

You can use the let function to safely access a nullable type. The let function will check if the variable is null before accessing it. If the variable is not null, the let function will invoke the lambda function with the variable as the first parameter and the receiver as the second parameter; if the variable is null, the let function will return null.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
myVar?.let { it, str -> println("$it $str") } // prints "Hello Hello"

myVar = null
myVar?.let { it, str -> println("$it $str") } // prints "null null"
```

You can use the also function to safely access a nullable type. The also function will check if the variable is null before accessing it. If the variable is not null, the also function will invoke the lambda function with the variable as the first parameter and the receiver as the second parameter; if the variable is null, the also function will return null.

For example, the following code will print "Hello" if myVar is not null, and will print "null" if myVar is null:

```kotlin
var myVar: String? = "Hello"
myVar?.also { it, str -> println("$it $str") } // prints "Hello Hello"

myVar = null
myVar?.also { it, str -> println("$it $str") } // prints "null null"
```

You can use the takeIf function to safely access a nullable type. The takeIf function will check if the variable is null before accessing it. If the variable is not null, the takeIf function will invoke the lambda function with the variable as the parameter and return the result; if the variable is null, the takeIf function will return null.

For example,