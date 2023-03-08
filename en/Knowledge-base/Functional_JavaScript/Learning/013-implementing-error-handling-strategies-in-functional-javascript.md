---
title: 013: Implementing error handling strategies in functional JavaScript
description: 
published: true
date: 2023-02-17T13:06:29.544Z
tags: 
editor: markdown
dateCreated: 2023-02-17T13:06:28.163Z
---

- [013: 기능적 JavaScript에서 오류 처리 전략 구현***Korean** document is available*](/ko/Knowledge-base/Functional_JavaScript/Learning/013-implementing-error-handling-strategies-in-functional-javascript)
{.links-list}


## Implementing error handling strategies in functional JavaScript

Functional programming is a programming paradigm that emphasizes the evaluation of functions. It is a declarative programming style that is often used to write more concise and maintainable code.

One of the benefits of functional programming is that it can help you to write code that is easier to reason about and debug. In this post, we will explore some strategies for implementing error handling in functional JavaScript.

### Try/catch

The first strategy we will look at is using the `try/catch` statement. The `try/catch` statement allows you to catch errors that occur in your code.

For example, let's say we have a function that divides two numbers. If we pass in `0` as the divisor, we will get an error.

We can use the `try/catch` statement to catch this error and handle it gracefully.

```javascript
function divide(x, y) {
    try {
        return x / y;
    } catch (e) {
        console.log("Error: Cannot divide by zero.");
    }
}
```

In the above code, we are using the `try/catch` statement to catch any errors that occur when we try to divide `x` by `y`. If an error does occur, we print a message to the console.

### Returning early

Another strategy for handling errors is to return early from a function when an error occurs. This can be done using the `throw` keyword.

For example, let's say we have a function that checks if a given number is positive. If the number is not positive, we want to `throw` an error.

```javascript
function checkPositive(x) {
    if (x <= 0) {
        throw "Error: x must be positive.";
    }
    // ...
}
```

In the above code, we are using the `throw` keyword to throw an error if `x` is not positive.

### Using optional chaining

Another strategy for handling errors is to use optional chaining. Optional chaining is a feature of JavaScript that allows you to access properties of an object without having to check if the object exists first.

For example, let's say we have an object that contains information about a user.

```javascript
const user = {
    id: 1,
    name: "John"
};
```

If we try to access the `age` property of the `user` object, we will get an error because the `age` property does not exist.

```javascript
console.log(user.age); // Error: age does not exist
```

We can use optional chaining to safely access the `age` property.

```javascript
console.log(user?.age); // undefined
```

In the above code, we are using optional chaining to access the `age` property. If the `age` property does not exist, we will get `undefined` instead of an error.

### Conclusion

In this post, we have explored some strategies for implementing error handling in functional JavaScript. We have seen how to use the `try/catch` statement, how to return early from a function when an error occurs, and how to use optional chaining.

Which strategy you use will depend on your specific needs. However, all of these strategies can be used to write more robust and maintainable code.