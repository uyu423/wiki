---
title: 075: Dynamic Programming in Kotlin: Optimizing Recursive Solutions with Memoization
description: 
published: true
date: 2023-01-31T18:04:36.388Z
tags: 
editor: markdown
dateCreated: 2023-01-31T18:04:32.800Z
---

- [075: Kotlin의 동적 프로그래밍: 메모이제이션으로 재귀 솔루션 최적화***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/075-dynamic-programming-in-kotlin-optimizing-recursive-solutions-with-memoization)
{.links-list}
- [075: Kotlin での動的プログラミング: メモ化による再帰的ソリューションの最適化***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/075-dynamic-programming-in-kotlin-optimizing-recursive-solutions-with-memoization)
{.links-list}
- [075：Kotlin 中的动态编程：使用记忆优化递归解决方案***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/075-dynamic-programming-in-kotlin-optimizing-recursive-solutions-with-memoization)
{.links-list}



# 075: Dynamic Programming in Kotlin: Optimizing Recursive Solutions with Memoization

Dynamic programming is a powerful technique for solving complex problems by breaking them down into smaller, simpler subproblems. It can be used to optimize recursive solutions by storing the results of subproblems so that they can be reused instead of recalculated.

In this article, we'll learn how to use dynamic programming to optimize recursive solutions in Kotlin. We'll start with a simple example to illustrate the technique, then we'll apply it to a more complex problem.

## A Simple Example

Suppose we want to calculate the nth Fibonacci number. We can do this recursively using the following code:

```kotlin
fun fib(n: Int): Int {
    if (n <= 1) return n
    return fib(n - 1) + fib(n - 2)
}
```

However, this code is very inefficient because it recalculates the results of subproblems. For example, when we calculate `fib(5)`, we calculate `fib(4)` and `fib(3)` twice:

![Fibonacci calculation](fibonacci.png)

We can use dynamic programming to optimize this code by storing the results of subproblems so that they can be reused. We can do this by using an array to keep track of the Fibonacci numbers that have already been calculated:

```kotlin
fun fib(n: Int): Int {
    if (n <= 1) return n
    val fibs = IntArray(n + 1)
    fibs[0] = 0
    fibs[1] = 1
    for (i in 2..n) {
        fibs[i] = fibs[i - 1] + fibs[i - 2]
    }
    return fibs[n]
}
```

Now, when we calculate `fib(5)`, we can reuse the results of `fib(4)` and `fib(3)`:

![Fibonacci calculation with memoization](fibonacci-memoized.png)

This code is much more efficient because we don't have to recalculate the results of subproblems.

## A More Complex Example

Now let's apply dynamic programming to a more complex problem: the knapsack problem. In the knapsack problem, we are given a set of items, each with a weight and a value. Our goal is to choose a subset of items that maximizes the total value while staying under a given weight limit.

For example, suppose we have the following items:

| Item | Weight | Value |
| --- | --- | --- |
| A | 2 | 6 |
| B | 2 | 10 |
| C | 3 | 12 |

And we want to find a subset of items that has a total weight of 5 or less and maximizes the total value. In this case, the optimal solution is to choose items A and C, which have a total weight of 5 and a total value of 18.

We can solve the knapsack problem using dynamic programming. We'll use an array to keep track of the maximum value that can be achieved for each weight up to the weight limit:

```kotlin
fun knapsack(items: Array<Item>, weightLimit: Int): Int {
    val values = IntArray(weightLimit + 1)
    for (i in items.indices) {
        val item = items[i]
        for (w in weightLimit downTo item.weight) {
            values[w] = max(values[w], values[w - item.weight] + item.value)
        }
    }
    return values[weightLimit]
}
```

In this code, `values[w]` represents the maximum value that can be achieved with a weight of `w` or less. We calculate this value by considering each item in turn and seeing if it's worth adding to the knapsack. If it is, we update `values[w]` accordingly.

For example, suppose we're considering item A with weight 2 and value 6. We update `values[2]` to 6 (the value of item A) and `values[3]` to 8 (the value of item A plus the best value we can get with a weight of 1).

![Knapsack calculation](knapsack.png)

We continue this process until we've considered all of the items. At the end, `values[weightLimit]` contains the maximum value that can be achieved with a weight of `weightLimit` or less.

## Conclusion

In this article, we've learned how to use dynamic programming to optimize recursive solutions in Kotlin. We've seen how to use memoization to store the results of subproblems so that they can be reused, and we've applied this technique to the knapsack problem.