---
title: 056: The When Expression in Kotlin: A Comprehensive Guide
description: 
published: true
date: 2023-02-16T19:17:38.255Z
tags: 
editor: markdown
dateCreated: 2023-02-16T19:17:30.013Z
---

- [056: La expresión When en Kotlin: una guía completa***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/056-the-when-expression-in-kotlin-a-comprehensive-guide)
{.links-list}
- [056：Kotlin 中的 When 表达式：综合指南***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/056-the-when-expression-in-kotlin-a-comprehensive-guide)
{.links-list}
- [056: Kotlin의 When 표현식: 종합 안내서***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/056-the-when-expression-in-kotlin-a-comprehensive-guide)
{.links-list}


## Introduction

Kotlin's when expression is a powerful tool that can be used to match on a variety of different types of data. In this guide, we'll take a look at how to use the when expression in Kotlin and explore some of its more advanced features.

## Basic Usage

The when expression is Kotlin's equivalent of the switch statement in other languages. It allows you to match on a value and execute a block of code based on that value. 

Here's a simple example:

```kotlin
when (x) {
    1 -> println("x is 1")
    2 -> println("x is 2")
    else -> println("x is neither 1 nor 2")
}
```

In this example, we're matching on the value of the variable `x`. If `x` is equal to `1`, the code block associated with that case will be executed. Similarly, if `x` is equal to `2`, the code block associated with that case will be executed. If `x` is neither `1` nor `2`, the code block associated with the `else` case will be executed.

It's important to note that the `else` case is not required. If you omit the `else` case, the when expression will not match any values that are not explicitly listed in the other cases:

```kotlin
when (x) {
    1 -> println("x is 1")
    2 -> println("x is 2")
}
```

In this example, if `x` is neither `1` nor `2`, the code block associated with the `else` case will not be executed.

## Matching on Types

In addition to matching on values, the when expression can also be used to match on types. This is particularly useful when working with nullable types. 

Consider the following example:

```kotlin
fun process(value: Any) {
    when (value) {
        is String -> println(value.length)
        is Int -> println(value * 2)
        else -> println("I don't know what this is")
    }
}
```

In this example, we have a function that takes an `Any` type and processes it in some way. We use the when expression to match on the type of the `value` parameter. 

If `value` is a `String`, we print out its length. If `value` is an `Int`, we print out its value multiplied by 2. If `value` is neither a `String` nor an `Int`, we print out a message saying that we don't know what it is.

You can also use the when expression to match on nullable types. This is useful for avoiding the dreaded `NullPointerException`. 

Consider the following example:

```kotlin
fun process(value: Any?) {
    when (value) {
        is String -> println(value.length)
        is Int -> println(value * 2)
        null -> println("value is null")
        else -> println("I don't know what this is")
    }
}
```

In this example, we've changed the type of the `value` parameter from `Any` to `Any?`. This makes the parameter nullable, which means it can now take the value `null`. 

We've added a case to the when expression to handle the `null` value. If `value` is `null`, we print out a message saying so. 

It's important to note that the `null` case must come before the `else` case. This is because the `else` case will match any value, including `null`. 

If the `null` case were after the `else` case, it would never be executed.

## Conclusion

In this guide, we've taken a look at how to use the when expression in Kotlin. We've seen how to match on values and types, and we've also seen how to handle nullable types.