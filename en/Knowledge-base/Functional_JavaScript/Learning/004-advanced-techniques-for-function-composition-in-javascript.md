---
title: 004: Advanced techniques for function composition in JavaScript
description: 
published: true
date: 2023-02-17T08:32:47.332Z
tags: 
editor: markdown
dateCreated: 2023-02-17T08:32:45.979Z
---

- [004: JavaScript에서 함수 구성을 위한 고급 기술***Korean** document is available*](/ko/Knowledge-base/Functional_JavaScript/Learning/004-advanced-techniques-for-function-composition-in-javascript)
{.links-list}


#Advanced techniques for function composition in JavaScript

Function composition is a powerful technique for structuring programs that can lead to more readable and maintainable code. In JavaScript, there are a number of ways to achieve function composition, each with its own trade-offs.

In this post, we'll explore four different techniques for function composition in JavaScript:

1. Function chaining
2. Function pipelines
3. Function trees
4. Function builders

##Function chaining

Function chaining is a technique for composing functions by making each function return the next function in the chain. This can be accomplished in JavaScript using the `.` (dot) operator:

```javascript
function add(x, y) {
  return x + y;
}

function subtract(x, y) {
  return x - y;
}

function multiply(x, y) {
  return x * y;
}

function divide(x, y) {
  return x / y;
}

// Function chaining
const result1 = add(1, 2)
  .subtract(3)
  .multiply(4)
  .divide(5);

console.log(result1); // -> 0.6
```

In the example above, we have a chain of four functions: `add`, `subtract`, `multiply`, and `divide`. Each function in the chain takes the output of the previous function as its input.

Function chaining can be a convenient way to structure code, but it can also lead to code that is difficult to read and maintain. In particular, it can be hard to tell what order the functions will be executed in, and it can be easy to introduce bugs by forgetting to chain a function.

##Function pipelines

Function pipelines are similar to function chains, but instead of each function returning the next function in the pipeline, each function returns the result of calling the next function in the pipeline with its own arguments.

In JavaScript, function pipelines can be implemented using the `.` (dot) operator and the `Function.prototype.bind` method:

```javascript
function add(x, y) {
  return x + y;
}

function subtract(x, y) {
  return x - y;
}

function multiply(x, y) {
  return x * y;
}

function divide(x, y) {
  return x / y;
}

// Function pipelines
const result2 = add.bind(null, 1, 2)
  .subtract.bind(null, 3)
  .multiply.bind(null, 4)
  .divide.bind(null, 5);

console.log(result2); // -> 0.6
```

In the example above, we have a pipeline of four functions: `add`, `subtract`, `multiply`, and `divide`. Each function in the pipeline returns the result of calling the next function in the pipeline with its own arguments.

Function pipelines can be more difficult to read and understand than function chains, but they have the advantage of being easier to compose and reuse. In particular, it is easy to add new functions to a pipeline without having to change the existing code.

##Function trees

Function trees are a technique for composing functions by creating a tree-like structure of functions. In JavaScript, function trees can be implemented using the `.` (dot) operator:

```javascript
function add(x, y) {
  return x + y;
}

function subtract(x, y) {
  return x - y;
}

function multiply(x, y) {
  return x * y;
}

function divide(x, y) {
  return x / y;
}

// Function trees
const tree = {
  add,
  subtract,
  multiply,
  divide
};

const result3 = tree.add(1, 2)
  .subtract(3)
  .multiply(4)
  .divide(5);

console.log(result3); // -> 0.6
```

In the example above, we have a tree of four functions: `add`, `subtract`, `multiply`, and `divide`. Each function in the tree can be accessed using the dot operator.

Function trees can be easier to read and understand than function chains or pipelines, but they can be more difficult to compose and reuse. In particular, it can be hard to add new functions to a tree without changing the existing code.

##Function builders

Function builders are a technique for composing functions by creating a builder function that takes a set of functions as arguments and returns a new function that calls the given functions in order.

In JavaScript, function builders can be implemented using the `.` (dot) operator and the `Function.prototype.bind` method:

```javascript
function add(x, y) {
  return x + y;
}

function subtract(x, y) {
  return x - y;
}

function multiply(x, y) {
  return x * y;
}

function divide(x, y) {
  return x / y;
}

// Function builder
function builder(...funcs) {
  return function (x) {
    return funcs.reduce((acc, func) => func(acc), x);
  };
}

const result4 = builder(
  add.bind(null, 1, 2),
  subtract.bind(null, 3),
  multiply.bind(null, 4),
  divide.bind(null, 5)
)();

console.log(result4); // -> 0.6
```

In the example above, we have a function builder that takes an arbitrary number of functions as arguments and returns a new function that calls the given functions in order.

Function builders can be more difficult to read and understand than function chains or pipelines, but they have the advantage of being easier to compose and reuse. In particular, it is easy to add new functions to a builder without having to change the existing code.

##Additional Information

Function composition is a powerful technique for structuring programs, but it is not without its trade-offs. In particular, function composition can make code more difficult to read and understand.

When deciding whether or not to use function composition in your code, it is important to weigh the benefits and drawbacks. In general, function composition can be a useful tool for creating more modular and reusable code, but it should be used with caution.