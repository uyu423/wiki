---
title: 014: Writing pure functions in JavaScript for safer code
description: 
published: true
date: 2023-02-17T13:32:42.855Z
tags: 
editor: markdown
dateCreated: 2023-02-17T13:32:36.130Z
---

- [014: 안전한 코드를 위해 JavaScript로 순수 함수 작성***Korean** document is available*](/ko/Knowledge-base/Functional_JavaScript/Learning/014-writing-pure-functions-in-javascript-for-safer-code)
{.links-list}


# Writing pure functions in JavaScript for safer code

JavaScript is a powerful programming language that allows developers to write code that is both flexible and robust. However, JavaScript's power also comes with a certain amount of complexity, which can lead to errors in code that are difficult to debug.

One way to reduce the complexity of JavaScript code and to make it more robust is to write pure functions. Pure functions are functions that always return the same result for the same input, and have no side effects. In other words, pure functions are deterministic.

Pure functions are important for two main reasons:

1. They are easier to reason about than impure functions.

2. They are easier to test than impure functions.

Let's take a look at an example of a pure function:

```javascript
function square(x) {
  return x * x;
}
```

This function takes a single input, `x`, and returns the square of that input. Because the function always returns the same result for the same input, we say that it is deterministic.

In contrast, consider the following impure function:

```javascript
function square(x) {
  console.log(x);
  return x * x;
}
```

This function takes the same input, `x`, and returns the square of that input. However, it also has a side effect: it prints the value of `x` to the console. Because this function has a side effect, we say that it is non-deterministic.

It is important to note that pure functions can only be written in programming languages that support side effects. JavaScript is one such language. In contrast, languages like Haskell and PureScript do not allow side effects, and as a result, all functions in these languages are pure.

One common misconception about pure functions is that they are boring and lack flexibility. This is simply not true. Pure functions can be just as flexible as impure functions. The only difference is that pure functions are easier to reason about and easier to test.

There are a few rules that you can follow to write pure functions in JavaScript:

1. **Don't use global variables.** Global variables are variables that are declared outside of any function. These variables can be accessed and modified by any code in your program. As a result, they are not pure.

  ```javascript
  // This is an impure function because it uses a global variable
  function impure(x) {
    return x * window.y;
  }
  ```

2. **Don't use side effects.** Side effects are any actions that take place outside of the function, such as printing to the console or modifying a global variable. These actions make the function non-deterministic.

  ```javascript
  // This is an impure function because it has a side effect
  function impure(x) {
    console.log(x);
    return x * x;
  }
  ```

3. **Don't use mutable data structures.** Mutable data structures are data structures that can be modified in place, such as arrays and objects. These data structures are not pure because they can be modified by other code in your program.

  ```javascript
  // This is an impure function because it uses a mutable data structure
  function impure(x) {
    x.push(1);
    return x;
  }
  ```

4. **Don't make network requests.** Network requests are actions that take place outside of your program, such as making an HTTP request to a server. These requests are not pure because they can take an unpredictable amount of time to complete.

  ```javascript
  // This is an impure function because it makes a network request
  function impure(x) {
    return fetch('https://example.com/api/v1/users/' + x).then(function(response) {
      return response.json();
    });
  }
  ```

5. **Don't use Date.now() or Math.random().** These functions are impure because they return a different value each time they are called.

  ```javascript
  // This is an impure function because it uses Math.random()
  function impure(x) {
    return x * Math.random();
  }
  ```

By following these rules, you can be sure that your functions are pure. Pure functions are easier to reason about and easier to test, which makes them essential for writing safe and reliable code.