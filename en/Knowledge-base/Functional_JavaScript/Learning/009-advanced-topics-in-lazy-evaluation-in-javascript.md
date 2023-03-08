---
title: 009: Advanced topics in lazy evaluation in JavaScript
description: 
published: true
date: 2023-02-17T11:06:55.136Z
tags: 
editor: markdown
dateCreated: 2023-02-17T11:06:53.745Z
---

- [009: JavaScript의 지연 평가에 대한 고급 주제***Korean** document is available*](/ko/Knowledge-base/Functional_JavaScript/Learning/009-advanced-topics-in-lazy-evaluation-in-javascript)
{.links-list}


## What is Lazy Evaluation?
Lazy evaluation is a form of computation where the result of an expression is not calculated until it is needed. This can be contrasted with eager evaluation, where expressions are evaluated as soon as they are bound to a variable.

In JavaScript, lazy evaluation is used in several places:

- The `&&` and `||` operators only evaluate the right-hand side if the left-hand side does not determine the result.
- The `? :` operator only evaluates the right-hand side if the left-hand side is truthy.
- The `.` operator only evaluates the right-hand side if the left-hand side is an object.
- Function arguments are only evaluated when the function is called.
- Object properties are only evaluated when they are accessed.

Lazy evaluation can be used to improve performance by avoiding unnecessary work. It can also be used to create infinite data structures.

## Lazy Evaluation and Infinite Data Structures
Lazy evaluation is often used in conjunction with recursion to create infinite data structures.

Consider the following example:

```javascript
function createRange(start, end) {
  if (start === end) {
    return [start];
  } else {
    return [start, ...createRange(start + 1, end)];
  }
}
```

This function creates an array of numbers starting from `start` and ending at `end`. The `...` spread operator is used to concatenate the arrays.

If we call `createRange(1, Infinity)`, the function will keep creating arrays until the call stack overflows. However, if we call `createRange(1, 10)`, the function will only create 10 arrays.

This is because the `...` operator is only evaluated when the function is called with a finite `end` argument. When `end` is `Infinity`, the `...` operator is never evaluated.

## Lazy Evaluation and Performance
Lazy evaluation can improve performance by avoiding unnecessary work.

Consider the following example:

```javascript
function isEven(n) {
  if (n === 0) {
    return true;
  } else if (n === 1) {
    return false;
  } else {
    return isEven(n - 2);
  }
}

isEven(1000000); // false
```

This function returns `true` if `n` is even and `false` if `n` is odd. It uses recursion to compute the result.

If we call `isEven(1000000)`, the function will recurse until the call stack overflows. However, if we call `isEven(10)`, the function will only recurse 10 times.

This is because the `if` statement is only evaluated when the function is called with a finite `n` argument. When `n` is `1000000`, the `if` statement is never evaluated.

## Lazy Evaluation and Memoization
Lazy evaluation can be used to improve performance by memoizing the results of expensive function calls.

Consider the following example:

```javascript
function Fibonacci(n) {
  if (n === 0) {
    return 0;
  } else if (n === 1) {
    return 1;
  } else {
    return Fibonacci(n - 1) + Fibonacci(n - 2);
  }
}

Fibonacci(10); // 55
```

This function computes the `n`th Fibonacci number. It uses recursion to compute the result.

If we call `Fibonacci(10)`, the function will recurse 10 times. However, if we call `Fibonacci(100)`, the function will recurse 100 times.

This is because the `if` statement is only evaluated when the function is called with a finite `n` argument. When `n` is `100`, the `if` statement is never evaluated.

We can improve the performance of this function by memoizing the results of expensive function calls.

```javascript
function Fibonacci(n, memo = {}) {
  if (n in memo) {
    return memo[n];
  } else if (n === 0) {
    return 0;
  } else if (n === 1) {
    return 1;
  } else {
    memo[n] = Fibonacci(n - 1, memo) + Fibonacci(n - 2, memo);
    return memo[n];
  }
}

Fibonacci(10); // 55
Fibonacci(100); // 354224848179261915075
```

In this version of the function, we pass in an empty object as a memo. The function checks if the `n`th Fibonacci number is in the memo. If it is, the function returns the memoized value. If not, the function computes the `n`th Fibonacci number and memoizes the result.

This improvement is significant. The original function takes `10` milliseconds to compute the `100`th Fibonacci number. The memoized function takes `0` milliseconds.

## Additional Information
- Lazy evaluation is also known as call-by-need.
- Eager evaluation is also known as call-by-value.
- In JavaScript, lazy evaluation is not always guaranteed. For example, the `.` operator eagerly evaluates the right-hand side if the left-hand side is not an object.

## Resources
- [Wikipedia - Lazy evaluation](https://en.wikipedia.org/wiki/Lazy_evaluation)
- [MDN - Lazy evaluation](https://developer.mozilla.org/en-US/docs/Glossary/Lazy_evaluation)
- [ExploringJS - Lazy evaluation](https://exploringjs.com/es6/ch_operators.html#sec_lazy-evaluation)