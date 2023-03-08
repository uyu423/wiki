---
title: 003: Using recursion to solve common programming problems in JavaScript
description: 
published: true
date: 2023-02-17T08:06:51.595Z
tags: 
editor: markdown
dateCreated: 2023-02-17T08:06:44.841Z
---

- [003: 재귀를 사용하여 JavaScript에서 일반적인 프로그래밍 문제 해결***Korean** document is available*](/ko/Knowledge-base/Functional_JavaScript/Learning/003-using-recursion-to-solve-common-programming-problems-in-javascript)
{.links-list}


# Using recursion to solve common programming problems in JavaScript

Recursion is a powerful tool that can be used to solve many common programming problems. In this post, we will explore how to use recursion to solve some common problems in JavaScript.

## What is recursion?

Recursion is a process in which a function calls itself. This can be used to solve problems in which the solution can be divided into smaller sub-problems.

## How to use recursion?

When using recursion, it is important to have a base case and a recursive case. The base case is the simplest form of the problem and the recursive case is the case in which the function calls itself.

## Example: Factorial

One common example of recursion is calculating the factorial of a number. The factorial of a number is the product of all the integers from 1 to that number. For example, the factorial of 5 is 5 * 4 * 3 * 2 * 1.

We can use recursion to calculate the factorial of a number as follows:

```javascript
function factorial(n) {
  // Base case
  if (n === 1) {
    return 1;
  }
  // Recursive case
  return n * factorial(n - 1);
}

console.log(factorial(5)); // 120
```

In the example above, the base case is when n equals 1. The recursive case is when the function calls itself with n-1. This will keep calling itself until it reaches the base case.

## Example: Fibonacci Sequence

Another common example of recursion is the Fibonacci sequence. The Fibonacci sequence is a series of numbers in which each number is the sum of the two preceding numbers. The first two numbers in the sequence are 0 and 1. For example, the Fibonacci sequence is 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987, 1597, 2584, 4181, 6765, 10946, 17711, 28657, 46368, 75025, 121393, 196418, 317811, 514229, 832040, 1346269, 2178309, 3524578, 5702887, 9227465, 14930352, 24157817, 39088169, 63245986, 102334155, 165580141, 267914296, 433494437, 701408733, 1134903170, 1836311903, 2971215073, 4807526976, 7778742049, 12586269025, 20365011074, 32951280099, 53316291173, 86267571272, 139583862445, 225851433717, 365435296162, 591286729879, 969323036873, 1548008755920, 2504730781961, 4052739537881, 6557470319842, 10610209857723, 17167680177565, 27777890035288, 44945570212853, 72723460248141, 11805916207174, 1930392490709135, 313528776555673
```

We can use recursion to calculate the Fibonacci sequence as follows:

```javascript
function fib(n) {
  // Base case
  if (n <= 1) {
    return n;
  }
  // Recursive case
  return fib(n - 1) + fib(n - 2);
}

console.log(fib(10)); // 55
```

In the example above, the base case is when n is less than or equal to 1. The recursive case is when the function calls itself with n-1 and n-2. This will keep calling itself until it reaches the base case.

## Example: Greatest Common Divisor

Another common example of recursion is finding the greatest common divisor (GCD) of two numbers. The GCD of two numbers is the largest number that divides both numbers evenly. For example, the GCD of 12 and 18 is 6.

We can use recursion to calculate the GCD of two numbers as follows:

```javascript
function gcd(a, b) {
  // Base case
  if (b === 0) {
    return a;
  }
  // Recursive case
  return gcd(b, a % b);
}

console.log(gcd(12, 18)); // 6
```

In the example above, the base case is when b equals 0. The recursive case is when the function calls itself with b and a mod b. This will keep calling itself until it reaches the base case.

## Example: Binary Search

Binary search is a common algorithm that is used to search for an element in a sorted array. The binary search algorithm works by dividing the array in half and comparing the element to be searched for with the element in the middle of the array. If the element to be searched for is less than the element in the middle of the array, the algorithm will search the first half of the array. If the element to be searched for is greater than the element in the middle of the array, the algorithm will search the second half of the array. This process is repeated until the element is found or the array is exhausted.

We can use recursion to implement binary search as follows:

```javascript
function binarySearch(arr, elem) {
  // Base case
  if (arr.length === 0) {
    return false;
  }
  // Recursive case
  const middle = Math.floor(arr.length / 2);
  const middleElem = arr[middle];
  if (elem === middleElem) {
    return true;
  } else if (elem < middleElem) {
    return binarySearch(arr.slice(0, middle), elem);
  } else {
    return binarySearch(arr.slice(middle + 1), elem);
  }
}

const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
console.log(binarySearch(arr, 5)); // true
console.log(binarySearch(arr, 11)); // false
```

In the example above, the base case is when the array is empty. The recursive case is when the function calls itself with the first or second half of the array, depending on whether the element to be searched for is less than or greater than the element in the middle of the array. This will keep calling itself until it reaches the base case.

## Conclusion

In this post, we have explored how to use recursion to solve some common problems in JavaScript. Recursion is a powerful tool that can be used to solve many common programming problems.