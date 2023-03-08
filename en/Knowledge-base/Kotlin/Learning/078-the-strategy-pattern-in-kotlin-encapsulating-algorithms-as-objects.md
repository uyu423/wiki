---
title: 078: The Strategy Pattern in Kotlin: Encapsulating Algorithms as Objects
description: 
published: true
date: 2023-02-14T17:55:34.418Z
tags: 
editor: markdown
dateCreated: 2023-02-14T17:55:27.002Z
---

- [078: El patrón de estrategia en Kotlin: algoritmos encapsulados como objetos***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/078-the-strategy-pattern-in-kotlin-encapsulating-algorithms-as-objects)
{.links-list}
- [078：Kotlin 中的策略模式：将算法封装为对象***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/078-the-strategy-pattern-in-kotlin-encapsulating-algorithms-as-objects)
{.links-list}
- [078: Kotlin의 전략 패턴: 알고리즘을 객체로 캡슐화***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/078-the-strategy-pattern-in-kotlin-encapsulating-algorithms-as-objects)
{.links-list}


# 078: The Strategy Pattern in Kotlin: Encapsulating Algorithms as Objects

## Introduction

The strategy pattern is a behavioural software design pattern that enables an algorithm's behaviour to be selected at runtime. This is useful when an application needs to use different algorithms, and the choice of algorithm can be made at runtime according to the user's input or the application's current state.

The strategy pattern is also known as the policy pattern.

## The Problem

Suppose we have a simple application that sorts a list of integers. We might start by writing a simple `sort` function like this:

```kotlin
fun sort(list: List<Int>): List<Int> {
    // implement sorting algorithm here
}
```

This `sort` function takes a list of integers as input and returns a new list of integers that is sorted in ascending order.

Now suppose we want to add another sorting algorithm to our application. We could write another `sort` function, but then we would have two functions with the same name but different behaviours. This would be confusing for users of our application.

Instead, we can use the strategy pattern to encapsulate each sorting algorithm in its own object. We can then write a `sort` function that takes a list of integers and a strategy object as input, and uses the strategy object to sort the list.

## The Solution

Here is how we can use the strategy pattern to sort a list of integers:

```kotlin
// define a sorting strategy interface
interface SortingStrategy {
    fun sort(list: List<Int>): List<Int>
}

// implement a sorting strategy for ascending order
class AscendingSortingStrategy : SortingStrategy {
    override fun sort(list: List<Int>): List<Int> {
        // implement sorting algorithm here
    }
}

// implement a sorting strategy for descending order
class DescendingSortingStrategy : SortingStrategy {
    override fun sort(list: List<Int>): List<Int> {
        // implement sorting algorithm here
    }
}

// use the strategy pattern to sort a list of integers
fun sort(list: List<Int>, strategy: SortingStrategy): List<Int> {
    return strategy.sort(list)
}
```

In the code above, we have defined a `SortingStrategy` interface that represents a sorting strategy. We have also implemented two sorting strategies: `AscendingSortingStrategy` and `DescendingSortingStrategy`.

Finally, we have written a `sort` function that takes a list of integers and a sorting strategy as input, and uses the sorting strategy to sort the list.

We can now use our `sort` function like this:

```kotlin
// sort a list of integers in ascending order
val ascendingList = sort(list, AscendingSortingStrategy())

// sort a list of integers in descending order
val descendingList = sort(list, DescendingSortingStrategy())
```

## The Benefits

The strategy pattern has several benefits:

- It enables an algorithm's behaviour to be selected at runtime.

- It makes it easy to add new algorithms to an application.

- It makes it easy to test algorithms.

- It makes code more readable and maintainable.

## The Pitfalls

There are a few potential pitfalls when using the strategy pattern:

- It can make code more complex.

- It can make code harder to read and understand.

- It can make it harder to change or add new algorithms.