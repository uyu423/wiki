---
title: [C Language] 001: Asymptotic Analysis
description: 
published: true
date: 2023-02-12T13:32:28.274Z
tags: 
editor: markdown
dateCreated: 2023-02-12T13:32:21.622Z
---

- [[Lenguaje C] 001: Análisis asintótico***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-001-asymptotic-analysis)
{.links-list}
- [【C语言】001：渐近分析***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-001-asymptotic-analysis)
{.links-list}
- [[C언어] 001: 점근적 해석***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-001-asymptotic-analysis)
{.links-list}


#[C Language] 001: Asymptotic Analysis

Asymptotic analysis is a mathematical tool used to understand the behavior of a function as the input grows large. It allows us to make statements about the runtime of an algorithm without having to actually run the algorithm on large inputs.

There are two main types of asymptotic analysis: worst-case analysis and average-case analysis.

##Worst-case analysis

Worst-case analysis is the simplest form of asymptotic analysis. It simply looks at the worst possible input to an algorithm and analyzes the runtime in that case.

For example, let's say we have an algorithm that sorts an array of n numbers. The worst case input for this algorithm is an array that is already sorted in reverse order. In this case, the runtime of the algorithm would be O(n^2).

##Average-case analysis

Average-case analysis is a bit more complicated than worst-case analysis. It looks at all possible inputs to an algorithm and calculates the average runtime.

For our sorting algorithm example, the average case runtime would be O(n log n). This is because there are n! possible inputs to the algorithm, and the runtime for each input is different. To calculate the average runtime, we simply take the sum of all the runtimes and divide by n!.

##Asymptotic notation

Asymptotic notation is a mathematical notation used to describe the runtime of an algorithm. The three most common notations are O(n), Ω(n), and Θ(n).

O(n) notation is used to describe the worst-case runtime of an algorithm. For our sorting algorithm example, the worst case runtime is O(n^2).

Ω(n) notation is used to describe the best-case runtime of an algorithm. For our sorting algorithm example, the best case runtime is Ω(n log n).

Θ(n) notation is used to describe the average-case runtime of an algorithm. For our sorting algorithm example, the average case runtime is Θ(n log n).

##Exercises

1. Given the following code, what is the asymptotic runtime?

```C
int sum(int n) {
    int i;
    int s = 0;
    for (i = 1; i <= n; i++) {
        s = s + i;
    }
    return s;
}
```

The asymptotic runtime of this code is O(n).

2. Given the following code, what is the asymptotic runtime?

```C
int sum(int n) {
    int i;
    int s = 0;
    for (i = 1; i <= n; i++) {
        s = s + i;
        if (s > 100) {
            break;
        }
    }
    return s;
}
```

The asymptotic runtime of this code is O(n).