---
title: 016: Advanced topics in recursion for functional programming in JavaScript
description: 
published: true
date: 2023-02-17T14:32:51.461Z
tags: 
editor: markdown
dateCreated: 2023-02-17T14:32:44.688Z
---

- [016: JavaScript에서 함수형 프로그래밍을 위한 재귀의 고급 주제***Korean** document is available*](/ko/Knowledge-base/Functional_JavaScript/Learning/016-advanced-topics-in-recursion-for-functional-programming-in-javascript)
{.links-list}


# Introduction to recursion for functional programming in JavaScript

Recursion is a powerful tool for functional programming, and it can be used to solve many problems more elegantly than using loops. In this post, we'll take a look at what recursion is, how it works, and how to use it effectively in JavaScript.

## What is recursion?

Recursion is a technique for solving problems by breaking them down into smaller subproblems. To do this, we define a function that calls itself recursively until it reaches a point where the subproblem it is working on can be solved directly.

For example, let's say we want to calculate the factorial of a number `n`. We can do this recursively by defining a function `factorial` that takes `n` as an argument and returns `n * (n-1) * (n-2) * ... * 1`. If we call `factorial(5)`, the function will return `5 * 4 * 3 * 2 * 1`, which is 120.

## How does recursion work?

In order to understand how recursion works, we need to understand what happens when a function is called. When a function is called, JavaScript creates a new execution context for the function. This execution context contains information about the function's arguments, local variables, and the point at which the function was called.

When a function calls itself, it creates a new execution context each time. This can be thought of as a stack of execution contexts, with the most recent context at the top. Each time the function calls itself, a new execution context is added to the top of the stack.

When the function reaches a point where it doesn't call itself anymore, the execution contexts are popped off the stack one by one, and the function returns the value it calculated.

## Base case and recursive case

In order for recursion to work, we need to define a base case and a recursive case. The base case is the point at which the function can solve the problem directly, without having to call itself. The recursive case is when the function calls itself.

For our factorial example, the base case would be when `n` is 1, because that's the point at which we can stop multiplying and just return 1. The recursive case would be when `n` is greater than 1, because that's when we need to call the function again with `n-1`.

## Tail call optimization

When a function calls itself, the current execution context is added to the stack. This can lead to a stack overflow if the function is called too many times.

Fortunately, JavaScript has a optimization called tail call optimization that helps to avoid this problem. Tail call optimization is when the return value of a function is the result of another function call. In this case, the current execution context can be reused, so the stack doesn't grow.

For example, the following function is tail recursive:

```javascript
function factorial(n) {
    if (n === 1) {
        return 1;
    } else {
        return n * factorial(n-1);
    }
}
```

But the following function is not tail recursive, because the return value is not the result of another function call:

```javascript
function factorial(n) {
    if (n === 1) {
        return 1;
    } else {
        return n * factorial(n-1) + 1;
    }
}
```

## When to use recursion

Recursion can be used to solve many problems, but it's not always the best solution. In general, recursion is best used when:

- The problem can be divided into smaller subproblems
- The problem can be solved directly when the subproblem is small enough
- The structure of the problem lends itself to a recursive solution

Recursion can also be used to create data structures such as linked lists and trees.

## When not to use recursion

Recursion is not always the best solution to a problem. In general, you should avoid recursion if:

- The problem can be more easily solved using a loop
- The problem doesn't lend itself to a recursive solution
- The problem is too computationally intensive to be solved recursively

## Examples of recursion

Let's take a look at some examples of recursion.

### Calculating the factorial of a number

As we saw earlier, we can use recursion to calculate the factorial of a number. This is a good example of a problem that can be divided into smaller subproblems, and it can be solved directly when the subproblem is small enough.

```javascript
function factorial(n) {
    if (n === 1) {
        return 1;
    } else {
        return n * factorial(n-1);
    }
}
```

### Calculating the nth Fibonacci number

Another common example of recursion is calculating the nth Fibonacci number. The Fibonacci sequence is a sequence of numbers where each number is the sum of the previous two numbers. So the sequence goes 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...

To calculate the nth Fibonacci number, we can use a recursive function that takes `n` as an argument and returns the `n-1`th Fibonacci number plus the `n-2`th Fibonacci number.

```javascript
function fibonacci(n) {
    if (n <= 1) {
        return n;
    } else {
        return fibonacci(n-1) + fibonacci(n-2);
    }
}
```

### Finding the greatest common divisor of two numbers

Another example of recursion is finding the greatest common divisor (GCD) of two numbers. The GCD of two numbers is the largest number that divides evenly into both numbers.

We can use Euclid's algorithm to find the GCD of two numbers. The algorithm is as follows:

- If `b` is 0, then the GCD is `a`
- Otherwise, the GCD is the GCD of `b` and the remainder of `a / b`

We can implement this algorithm in JavaScript as follows:

```javascript
function gcd(a, b) {
    if (b === 0) {
        return a;
    } else {
        return gcd(b, a % b);
    }
}
```

## Conclusion

In this post, we've seen what recursion is, how it works, and how to use it effectively in JavaScript. We've also seen some examples of problems that can be solved using recursion.

Recursion is a powerful tool for functional programming, but it's not always the best solution to a problem. In general, you should use recursion if the problem can be divided into smaller subproblems, the problem can be solved directly when the subproblem is small enough, and the structure of the problem lends itself to a recursive solution.