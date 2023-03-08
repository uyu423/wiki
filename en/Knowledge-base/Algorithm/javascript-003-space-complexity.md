---
title: [JavaScript] 003: Space Complexity
description: 
published: true
date: 2023-02-09T05:32:27.825Z
tags: 
editor: markdown
dateCreated: 2023-02-09T05:32:26.179Z
---

- [[JavaScript] 003: Complejidad espacial***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-003-space-complexity)
{.links-list}
- [[JavaScript] 003：空间复杂度***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-003-space-complexity)
{.links-list}
- [[JavaScript] 003: 공간 복잡성***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-003-space-complexity)
{.links-list}


# JavaScript 003: Space Complexity

In computer science, space complexity is the amount of memory required by an algorithm to run as a function of the length of the input. Space complexity is often expressed by asymptotic notation such as O(log n), O(n), O(n log n), O(n^2), or O(2^n).

## How to calculate Space Complexity

The space complexity of an algorithm is the amount of memory required to run the algorithm as a function of the length of the input. Space complexity is often expressed in terms of asymptotic notation such as O(log n), O(n), O(n log n), O(n^2), or O(2^n).

To calculate the space complexity of an algorithm, we need to take into account both the static space and the dynamic space used by the algorithm.

Static space is the amount of space required by the algorithm regardless of the size of the input. This includes the space required for the program code and for any static data structures used by the algorithm.

Dynamic space is the amount of space required by the algorithm as the size of the input increases. This includes the space required for any dynamic data structures used by the algorithm, such as stacks, queues, and trees.

The total space complexity of an algorithm is the sum of the static space and the dynamic space.

## Space Complexity Examples

Here are some examples of space complexity calculations.

### O(1) Space Complexity

An algorithm is said to have constant space complexity if the amount of space required to run the algorithm is independent of the size of the input.

A good example of an algorithm with constant space complexity is the addition of two numbers. The amount of space required to store the two numbers is independent of the size of the numbers.

### O(log n) Space Complexity

An algorithm is said to have logarithmic space complexity if the amount of space required to run the algorithm is logarithmic in the size of the input.

A good example of an algorithm with logarithmic space complexity is a binary search. To perform a binary search, we need to store the input array in memory. However, the amount of space required to store the array is logarithmic in the size of the input.

### O(n) Space Complexity

An algorithm is said to have linear space complexity if the amount of space required to run the algorithm is proportional to the size of the input.

A good example of an algorithm with linear space complexity is a linear search. To perform a linear search, we need to store the input array in memory. The amount of space required to store the array is proportional to the size of the input.

### O(n log n) Space Complexity

An algorithm is said to have n log n space complexity if the amount of space required to run the algorithm is n log n in the size of the input.

A good example of an algorithm with n log n space complexity is a merge sort. To perform a merge sort, we need to store the input array in memory. The amount of space required to store the array is n log n in the size of the input.

### O(n^2) Space Complexity

An algorithm is said to have quadratic space complexity if the amount of space required to run the algorithm is quadratic in the size of the input.

A good example of an algorithm with quadratic space complexity is a bubble sort. To perform a bubble sort, we need to store the input array in memory. The amount of space required to store the array is quadratic in the size of the input.

### O(2^n) Space Complexity

An algorithm is said to have exponential space complexity if the amount of space required to run the algorithm is exponential in the size of the input.

A good example of an algorithm with exponential space complexity is a brute force search. To perform a brute force search, we need to store the input array in memory. The amount of space required to store the array is exponential in the size of the input.