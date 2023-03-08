---
title: 005: Building reusable code with higher-order functions in JavaScript
description: 
published: true
date: 2023-02-17T09:07:23.887Z
tags: 
editor: markdown
dateCreated: 2023-02-17T09:07:17.039Z
---

- [005: JavaScript에서 고차 함수로 재사용 가능한 코드 작성***Korean** document is available*](/ko/Knowledge-base/Functional_JavaScript/Learning/005-building-reusable-code-with-higher-order-functions-in-javascript)
{.links-list}


# Building reusable code with higher-order functions in JavaScript

JavaScript is a powerful programming language that enables developers to build complex applications. A key feature of JavaScript is its support for higher-order functions.

Higher-order functions are functions that take other functions as arguments or return a function as a result. This enables developers to write code that is more modular and easier to reuse.

In this article, we will explore how to use higher-order functions to build reusable code in JavaScript.

## What are higher-order functions?

A higher-order function is a function that takes one or more functions as arguments or returns a function as a result.

In JavaScript, all functions are first-class citizens. This means that they can be passed as arguments to other functions and returned as results from functions.

Consider the following example:

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

function operate(operator, x, y) {
  return operator(x, y);
}

const result1 = operate(add, 1, 2);
// returns 3

const result2 = operate(subtract, 1, 2);
// returns -1

const result3 = operate(multiply, 1, 2);
// returns 2

const result4 = operate(divide, 1, 2);
// returns 0.5
```

In the example above, we have defined a function named `operate` that takes an `operator` function and two `x` and `y` arguments. The `operate` function then calls the `operator` function with the `x` and `y` arguments and returns the result.

We have also defined four other functions: `add`, `subtract`, `multiply`, and `divide`. These functions perform simple arithmetic operations.

Finally, we have invoked the `operate` function four times, passing in each of the arithmetic functions as the `operator` argument.

The `operate` function is an example of a higher-order function. It takes a function (the `operator` argument) and returns a result based on that function.

## Writing higher-order functions

Let's now write our own higher-order functions.

Consider the following example:

```javascript
function greeting(name) {
  return `Hello, ${name}!`;
}

function farewell(name) {
  return `Goodbye, ${name}!`;
}

function greetingFarewell(greeting, farewell, name) {
  return `${greeting(name)} ${farewell(name)}`;
}

const result = greetingFarewell(greeting, farewell, 'John');
// returns 'Hello, John! Goodbye, John!'
```

In the example above, we have defined a `greeting` function that takes a `name` argument and returns a greeting string. We have also defined a `farewell` function that takes a `name` argument and returns a farewell string.

Finally, we have defined a `greetingFarewell` function that takes a `greeting` function, a `farewell` function, and a `name` argument. The `greetingFarewell` function calls the `greeting` and `farewell` functions with the `name` argument and returns the concatenated results.

We have then invoked the `greetingFarewell` function, passing in the `greeting` and `farewell` functions as arguments.

The `greetingFarewell` function is an example of a higher-order function. It takes two functions (the `greeting` and `farewell` arguments) and returns a result based on those functions.

## Benefits of higher-order functions

Higher-order functions offer a number of benefits over traditional functions.

### Modularity

Higher-order functions enable developers to write code that is more modular.

Modular code is easier to understand, maintain, and reuse.

Consider the following example:

```javascript
function validate(value, validators) {
  for (const validator of validators) {
    const error = validator(value);
    if (error) {
      return error;
    }
  }
}

function required(value) {
  if (value === undefined || value === null || value === '') {
    return 'Required';
  }
}

function minLength(length) {
  return function(value) {
    if (value.length < length) {
      return `Must be at least ${length} characters`;
    }
  }
}

function maxLength(length) {
  return function(value) {
    if (value.length > length) {
      return `Must be at most ${length} characters`;
    }
  }
}

function email(value) {
  // email regex
}

const result = validate('john@example.com', [
  required,
  minLength(5),
  maxLength(10),
  email,
]);
// returns undefined
```

In the example above, we have defined a `validate` function that takes a `value` and an array of `validators`. The `validate` function then loops through the `validators` and calls each one with the `value`. If any of the `validators` return an error, the `validate` function returns that error. Otherwise, it returns `undefined`.

We have also defined four other functions: `required`, `minLength`, `maxLength`, and `email`. These functions are used to validate a value. The `required` function checks if a value is `undefined`, `null`, or an empty string. The `minLength` and `maxLength` functions check if a value is above or below a certain length, respectively. The `email` function checks if a value is a valid email address.

Finally, we have invoked the `validate` function, passing in a string and an array of validators. The `validate` function will loop through the validators and return the first error that it encounters.

The `validate` function is an example of a higher-order function. It takes an array of functions (the `validators` argument) and returns a result based on those functions.

### Composability

Higher-order functions enable developers to write code that is more composable.

Composable code is code that can be combined to create more complex functionality.

Consider the following example:

```javascript
function map(array, transform) {
  const mapped = [];
  for (const element of array) {
    mapped.push(transform(element));
  }
  return mapped;
}

function filter(array, predicate) {
  const filtered = [];
  for (const element of array) {
    if (predicate(element)) {
      filtered.push(element);
    }
  }
  return filtered;
}

function reduce(array, reducer, accumulator) {
  for (const element of array) {
    accumulator = reducer(accumulator, element);
  }
  return accumulator;
}

const result = reduce(
  map(filter([1, 2, 3, 4, 5], x => x % 2 === 0), x => x * x),
  (acc, cur) => acc + cur,
  0,
);
// returns 20
```

In the example above, we have defined three higher-order functions: `map`, `filter`, and `reduce`.

The `map` function takes an array and a `transform` function. The `map` function then calls the `transform` function on each element in the array and returns a new array with the transformed elements.

The `filter` function takes an array and a `predicate` function. The `filter` function then calls the `predicate` function on each element in the array and returns a new array with only the elements for which the `predicate` function returned `true`.

The `reduce` function takes an array, a `reducer` function, and an `accumulator`. The `reduce` function then calls the `reducer` function on the `accumulator` and each element in the array. The `reducer` function is responsible for updating the `accumulator` with the result of the operation. The `reduce` function returns the `accumulator` when it has finished looping through the array.

We have then invoked the `reduce` function, passing in the `map` function, the `filter` function, and an array. The `reduce` function will first call the `map` function, which will call the `filter` function. The `filter` function will return an array of only the even numbers. The `map` function will then return an array of the squares of the even numbers. The `reduce` function will then sum the elements in the array and return the result.

The `reduce` function is an example of a higher-order function. It takes two functions (the `map` and `filter` functions) and returns a result based on those functions.

## Conclusion

In this article, we have explored how to use higher-order functions to build reusable code in JavaScript.

Higher-order functions offer a number of benefits over traditional functions, including modularity and composability.

When writing higher-order functions, it is important to consider the trade-offs between readability and reuse. Higher-order functions can make code more difficult to understand, but they can also make code easier to reuse.

## Resources

- [Functions as first-class citizens](https://en.wikipedia.org/wiki/First-class_function)
- [Higher-order function](https://en.wikipedia.org/wiki/Higher-order_function)
- [JavaScript: The Good Parts](https://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742)