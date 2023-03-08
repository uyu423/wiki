---
title: 006: Introduction to functional design patterns in JavaScript
description: 
published: true
date: 2023-02-17T09:32:43.869Z
tags: 
editor: markdown
dateCreated: 2023-02-17T09:32:42.514Z
---

- [006: JavaScript의 기능적 디자인 패턴 소개***Korean** document is available*](/ko/Knowledge-base/Functional_JavaScript/Learning/006-introduction-to-functional-design-patterns-in-javascript)
{.links-list}


# Introduction to functional design patterns in JavaScript

Functional programming is a programming paradigm that emphasizes the evaluation of expressions rather than the execution of commands. It is a declarative programming style that is often used to write more concise and readable code.

In JavaScript, there are several design patterns that can be used to write more functional code. These patterns include the use of higher-order functions, closures, and currying.

## Higher-order functions

A higher-order function is a function that takes one or more functions as arguments, or returns a function as a result.

In JavaScript, higher-order functions are often used to create new functions from existing ones. For example, the Array.prototype.map() method is a higher-order function that takes a function as an argument and returns a new array with the results of calling the function on each element in the original array.

 Higher-order functions can also be used to avoid repeating code. For example, the following code defines a function that calculates the average of two numbers:

```javascript
function average(a, b) {
  return (a + b) / 2;
}
```

If we want to calculate the average of three numbers, we can write a new function that calls the average function twice:

```javascript
function average3(a, b, c) {
  return average(average(a, b), c);
}
```

Alternatively, we can use a higher-order function to create a new averaging function:

```javascript
function average(a, b) {
  return (a + b) / 2;
}

function average3(a, b, c) {
  return average(a, average(b, c));
}
```

The higher-order function approach is more concise and easier to read. It is also more extensible - if we want to calculate the average of four numbers, we can just call the average3 function twice.

## Closures

A closure is a function that has access to the variables in the scope in which it was defined.

In JavaScript, closures are often used to create private variables. For example, the following code defines a function that creates a counter object with two methods:

```javascript
function createCounter() {
  let count = 0;

  return {
    increment() {
      count++;
    },
    getCount() {
      return count;
    }
  };
}
```

The createCounter function defines a count variable and returns an object with two methods: increment, which increments the value of count, and getCount, which returns the current value of count.

Since the count variable is defined within the createCounter function, it is not accessible from outside the function. However, the increment and getCount methods have access to the count variable because they are defined within the same scope.

This allows us to create a private variable that can only be modified by the methods that have access to it.

## Currying

Currying is a technique for creating new functions from existing ones by partial application of arguments.

In JavaScript, currying is often used to create new functions with a fixed number of arguments. For example, the following code defines a function that calculates the product of two numbers:

```javascript
function product(a, b) {
  return a * b;
}
```

If we want to create a new function that calculates the product of three numbers, we can use currying to create a new function that takes the third number as an argument:

```javascript
function product3(a, b) {
  return function(c) {
    return a * b * c;
  }
}

const productOf3 = product3(3, 4);
console.log(productOf3(5)); // 60
```

In the code above, we use currying to create a new function, product3, that takes two numbers as arguments and returns a new function that takes the third number as an argument. We then call the product3 function with the values 3 and 4, and store the resulting function in a variable called productOf3.

Finally, we call the productOf3 function with the value 5 and print the result to the console.

 Currying can be used to create functions with any number of arguments. For example, the following code defines a function that calculates the sum of three numbers:

```javascript
function sum3(a) {
  return function(b) {
    return function(c) {
      return a + b + c;
    }
  }
}

const sumOf3 = sum3(1);
console.log(sumOf3(2)(3)); // 6
```

In the code above, we use currying to create a new function, sum3, that takes a single number as an argument and returns a new function that takes two numbers as arguments. We then call the sum3 function with the value 1, and store the resulting function in a variable called sumOf3.

Finally, we call the sumOf3 function with the values 2 and 3, and print the result to the console.

## Conclusion

Functional programming is a programming paradigm that emphasizes the evaluation of expressions rather than the execution of commands. In JavaScript, there are several design patterns that can be used to write more functional code. These patterns include the use of higher-order functions, closures, and currying.