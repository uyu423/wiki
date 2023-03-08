---
title: 031: Ranges in Kotlin: Representing and Iterating Over Ranges of Values
description: 
published: true
date: 2023-02-10T17:55:20.790Z
tags: 
editor: markdown
dateCreated: 2023-02-10T17:55:14.346Z
---

- [031: Rangos en Kotlin: representación e iteración sobre rangos de valores***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/031-ranges-in-kotlin-representing-and-iterating-over-ranges-of-values)
{.links-list}
- [031：Kotlin 中的范围：表示和迭代值的范围***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/031-ranges-in-kotlin-representing-and-iterating-over-ranges-of-values)
{.links-list}
- [031: Kotlin의 범위: 값 범위를 표현하고 반복하기***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/031-ranges-in-kotlin-representing-and-iterating-over-ranges-of-values)
{.links-list}


# Ranges in Kotlin: Representing and Iterating Over Ranges of Values

Ranges are a fundamental concept in Kotlin that allow you to represent a sequence of values. In this post, we'll take a look at how to create and iterate over ranges in Kotlin.

## Creating Ranges

There are two ways to create ranges in Kotlin: using the `..` operator, or using the `rangeTo()` function.

The `..` operator is used to create ranges that include both their start and end values. For example, the following code creates a range from 1 to 5:

```kotlin
val range1 = 1..5
```

The `rangeTo()` function, on the other hand, is used to create ranges that exclude their end values. For example, the following code creates a range from 1 to 5:

```kotlin
val range2 = 1.rangeTo(5)
```

Both of these ranges are *inclusive*, meaning that they include their start and end values. You can also create *exclusive* ranges by using the `until` keyword instead of `..` or `.rangeTo()`. For example, the following code creates a range from 1 to 5:

```kotlin
val range3 = 1 until 5
```

## Iterating Over Ranges

Now that we know how to create ranges, let's take a look at how to iterate over them. We can do this using a for loop:

```kotlin
for (i in 1..5) {
    println(i)
}
```

This code will print the numbers 1 through 5 to the console. We can also iterate over ranges in reverse by using the `downTo` keyword:

```kotlin
for (i in 5 downTo 1) {
    println(i)
}
```

This code will print the numbers 5 through 1 to the console.

## Conclusion

In this post, we've taken a look at how to create and iterate over ranges in Kotlin. Ranges are a powerful tool that can be used in a variety of situations. I hope you find them as useful as I do!