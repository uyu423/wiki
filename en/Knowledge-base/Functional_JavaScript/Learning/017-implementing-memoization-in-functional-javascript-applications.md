---
title: 017: Implementing memoization in functional JavaScript applications
description: 
published: true
date: 2023-02-17T15:06:58.856Z
tags: 
editor: markdown
dateCreated: 2023-02-17T15:06:52.054Z
---

- [017: 기능적 JavaScript 애플리케이션에서 메모이제이션 구현***Korean** document is available*](/ko/Knowledge-base/Functional_JavaScript/Learning/017-implementing-memoization-in-functional-javascript-applications)
{.links-list}


# Implementing memoization in functional JavaScript applications

Functional programming is a programming paradigm that emphasizes the evaluation of functions. It is a declarative programming style that is often used to write more concise and maintainable code.

One of the key concepts in functional programming is memoization. Memoization is a technique for caching the results of function calls and reusing the cached results when the same function is called again with the same arguments.

This can be a powerful optimization technique, especially in JavaScript applications where function calls are often made with the same arguments. In this post, we will take a look at how to implement memoization in JavaScript.

## What is memoization?

Memoization is a technique for caching the results of function calls and reusing the cached results when the same function is called again with the same arguments.

This can be a powerful optimization technique, especially in JavaScript applications where function calls are often made with the same arguments.

For example, consider a function that calculates the factorial of a number. This function can be implemented using recursion:

```javascript
function factorial(n) {
    if (n === 1) {
        return 1;
    }
    return n * factorial(n - 1);
}
```

If we call this function with the same argument multiple times, it will recalculate the factorial each time. This can be inefficient, especially for large numbers.

We can use memoization to cache the results of the function so that we don't have to recalculate the factorial each time:

```javascript
function factorial(n) {
    if (n === 1) {
        return 1;
    }
    return n * factorial(n - 1);
}

let memo = {};

function memoizedFactorial(n) {
    if (memo[n]) {
        return memo[n];
    }
    let result = factorial(n);
    memo[n] = result;
    return result;
}
```

In this example, we create a memo object to store the cached results. When we call the memoizedFactorial function, we first check to see if the result is already cached. If it is, we return the cached result. If it isn't, we calculate the result and cache it before returning it.

This can be a powerful optimization technique, especially in JavaScript applications where function calls are often made with the same arguments.

## Implementing memoization

There are a few different ways to implement memoization in JavaScript. In this section, we will take a look at two different approaches.

### Approach 1: Using a closure

One way to implement memoization is to use a closure. A closure is a function that has access to the variables in the outer scope.

For example, consider the following code:

```javascript
function outer() {
    let x = 10;
    
    function inner() {
        console.log(x);
    }
    
    inner();
}

outer(); // 10
```

In this code, the inner function has access to the x variable in the outer function. This is because the inner function is defined within the outer function.

We can use this concept to implement memoization:

```javascript
function memoize(fn) {
    let memo = {};
    
    return function(...args) {
        if (memo[args]) {
            return memo[args];
        }
        
        let result = fn(...args);
        memo[args] = result;
        return result;
    }
}

function factorial(n) {
    if (n === 1) {
        return 1;
    }
    return n * factorial(n - 1);
}

let memoizedFactorial = memoize(factorial);

memoizedFactorial(5); // 120
memoizedFactorial(5); // 120 (cached)
```

In this code, we create a memoize function that takes a function as an argument. This function returns a new function that has access to the memo variable in the outer scope.

When we call the new function, it first checks to see if the result is already cached. If it is, it returns the cached result. If it isn't, it calculates the result and caches it before returning it.

We can use this memoize function to memoize any function.

### Approach 2: Using a higher-order function

Another way to implement memoization is to use a higher-order function. A higher-order function is a function that takes one or more functions as arguments.

For example, consider the following code:

```javascript
function higherOrder(fn, x) {
    return fn(x);
}

function foo(x) {
    return x + 1;
}

higherOrder(foo, 10); // 11
```

In this code, we have a higher-order function that takes a function and an argument. It calls the function with the argument and returns the result.

We can use this concept to implement memoization:

```javascript
function memoize(fn) {
    let memo = {};
    
    return function(...args) {
        if (memo[args]) {
            return memo[args];
        }
        
        let result = fn(...args);
        memo[args] = result;
        return result;
    }
}

function factorial(n) {
    if (n === 1) {
        return 1;
    }
    return n * factorial(n - 1);
}

let memoizedFactorial = memoize(factorial);

memoizedFactorial(5); // 120
memoizedFactorial(5); // 120 (cached)
```

In this code, we create a memoize function that takes a function as an argument. This function returns a new function that calls the memoize function with the function and the arguments.

When we call the new function, it first checks to see if the result is already cached. If it is, it returns the cached result. If it isn't, it calculates the result and caches it before returning it.

We can use this memoize function to memoize any function.

## When to use memoization

Memoization can be a powerful optimization technique, but it is not always the best choice. In this section, we will take a look at some of the pros and cons of using memoization.

### Pros

- Memoization can be used to cache the results of expensive function calls. This can improve the performance of your application by avoiding unnecessary recalculation.

- Memoization can make your code more concise by avoiding duplicate function calls.

- Memoization can make your code more readable by making the intention of the code more clear.

### Cons

- Memoization can use up more memory than non-memoized code. This is because the memoized code will store the results of function calls in memory.

- Memoization can make your code more difficult to debug. This is because the cached results can make it difficult to trace the execution of the code.

- Memoization can make your code more difficult to understand. This is because the code can become more complex when memoization is used.

## Conclusion

In this post, we have taken a look at memoization and how to implement it in JavaScript. Memoization can be a powerful optimization technique, but it is not always the best choice. You should weigh the pros and cons of using memoization before deciding whether or not to use it in your application.