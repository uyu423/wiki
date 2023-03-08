---
title: 048: The Elvis Operator in Kotlin: Dealing with Null Values in a Compact Way
description: 
published: true
date: 2023-02-02T09:57:30.884Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:57:26.500Z
---

- [048: El operador de Elvis en Kotlin: tratar con valores nulos de forma compacta***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/048-the-elvis-operator-in-kotlin-dealing-with-null-values-in-a-compact-way)
{.links-list}
- [048：Kotlin 中的猫王运算符：以紧凑的方式处理空值***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/048-the-elvis-operator-in-kotlin-dealing-with-null-values-in-a-compact-way)
{.links-list}
- [048: Kotlin의 Elvis 연산자: 간결한 방식으로 Null 값 처리***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/048-the-elvis-operator-in-kotlin-dealing-with-null-values-in-a-compact-way)
{.links-list}


# The Elvis Operator in Kotlin: Dealing with Null Values in a Compact Way

Null values can be a pain to deal with in any programming language. In Kotlin, the Elvis operator provides a concise and safe way to handle null values.

## What is the Elvis Operator?

The Elvis operator is a null-safe operator that returns the non-null value of its operand or a default value if the operand is null. The Elvis operator is written as follows:

```kotlin
val result = operand ?: defaultValue
```

If the operand is not null, the Elvis operator returns it. If the operand is null, the Elvis operator returns the default value.

## How does the Elvis Operator work?

The Elvis operator is made up of two parts: the null-safe operator (`?.`) and the Elvis operator (`?:`).

The null-safe operator (`?.`) is used to safely access a member of a nullable object. If the object is null, the null-safe operator returns null instead of throwing a NullPointerException.

The Elvis operator (`?:`) is used to provide a default value if the operand is null.

## When to use the Elvis Operator

The Elvis operator is most commonly used to handle null values in a concise and safe way.

For example, consider the following code:

```kotlin
val list: List<String>? = null

val firstItem = list?.get(0) ?: "Default Value"
```

In this code, the `list` variable is nullable. If `list` is null, the `firstItem` variable will be set to the default value ("Default Value"). If `list` is not null, the `firstItem` variable will be set to the first item in the list.

## Additional Information

Here are some additional resources for learning more about the Elvis operator:

- [Kotlin docs - The Elvis operator](https://kotlinlang.org/docs/reference/null-safety.html#the-elvis-operator)
- [Kotlin Academy - Null safety and the Elvis operator](https://kotlinacademy.com/kotlin-null-safety-elvis-operator/)
- [Android Developers - Dealing with nulls in Kotlin](https://developer.android.com/kotlin/null-safety)