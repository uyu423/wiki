---
title: 003: Functions in TypeScript: How to Declare and Use Functions in Your Code
description: 
published: true
date: 2023-03-06T10:32:45.316Z
tags: 
editor: markdown
dateCreated: 2023-03-06T10:32:45.316Z
---

- [003: TypeScript의 함수: 코드에서 함수를 선언하고 사용하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/003-functions-in-typescript-how-to-declare-and-use-functions-in-your-code)
{.links-list}



Functions in TypeScript: How to Declare and Use Functions in Your Code

In TypeScript, functions are an essential part of the language. They are used to encapsulate reusable pieces of code and make your code more modular. In this article, we will explore how to declare and use functions in TypeScript.

## What are Functions in TypeScript?

A function is a block of code that performs a specific task. In TypeScript, functions can be declared in multiple ways, and they can have parameters and return values.

Functions in TypeScript can be categorized into two types:

1. Named Functions: These are functions that have a name associated with them. They can be declared using the `function` keyword.

2. Anonymous Functions: These are functions that do not have a name associated with them. They can be assigned to a variable or passed as an argument to another function.

## Declaring Functions in TypeScript

To declare a function in TypeScript, you need to specify the function name, parameters (if any), and return type (if any). Here is an example of a named function:

```typescript
function addNumbers(num1: number, num2: number): number {
  return num1 + num2;
}
```

In the above example, we have declared a function named `addNumbers` that takes two parameters of type `number` and returns a value of type `number`.

Here is an example of an anonymous function:

```typescript
let multiplyNumbers = function(num1: number, num2: number): number {
  return num1 * num2;
}
```

In the above example, we have assigned an anonymous function to a variable named `multiplyNumbers`.

## Using Functions in TypeScript

Once you have declared a function in TypeScript, you can use it in your code. Here is an example of how to use the `addNumbers` function we declared earlier:

```typescript
let result = addNumbers(10, 20);
console.log(result); // Output: 30
```

In the above example, we have called the `addNumbers` function with two arguments, `10` and `20`, and assigned the result to a variable named `result`. We then logged the value of `result` to the console, which should output `30`.

Here is an example of how to use the `multiplyNumbers` function we declared earlier:

```typescript
let result = multiplyNumbers(10, 20);
console.log(result); // Output: 200
```

In the above example, we have called the `multiplyNumbers` function with two arguments, `10` and `20`, and assigned the result to a variable named `result`. We then logged the value of `result` to the console, which should output `200`.

## Optional Parameters and Default Parameters

In TypeScript, you can declare optional parameters and default parameters in a function. Optional parameters are parameters that do not need to be passed to the function, while default parameters are parameters that have a default value if no argument is passed.

Here is an example of a function with an optional parameter:

```typescript
function greet(name?: string): void {
  if (name) {
    console.log(`Hello, ${name}!`);
  } else {
    console.log("Hello!");
  }
}
```

In the above example, we have declared a function named `greet` that takes an optional parameter named `name` of type `string`. If the `name` parameter is passed, the function will log a greeting with the name included. If the `name` parameter is not passed, the function will log a generic greeting.

Here is an example of a function with a default parameter:

```typescript
function greet(name: string = "World"): void {
  console.log(`Hello, ${name}!`);
}
```

In the above example, we have declared a function named `greet` that takes a default parameter named `name` of type `string`. If the `name` parameter is not passed, the function will use the default value of `"World"`.

## Rest Parameters

In TypeScript, you can declare rest parameters in a function. Rest parameters are used to pass a variable number of arguments to a function.

Here is an example of a function with rest parameters:

```typescript
function multiplyNumbers(...nums: number[]): number {
  return nums.reduce((total, num) => total * num);
}
```

In the above example, we have declared a function named `multiplyNumbers` that takes rest parameters named `nums` of type `number[]`. The function uses the `reduce` method to multiply all the numbers passed as arguments.

## Conclusion

In this article, we have explored how to declare and use functions in TypeScript. We have covered named functions, anonymous functions, optional parameters, default parameters, and rest parameters.

Functions are an essential part of any programming language, and TypeScript is no exception. By using functions, you can make your code more modular and reusable. Hopefully, this article has given you a good understanding of how to declare and use functions in TypeScript.

## Further Reading

- [TypeScript Handbook: Functions](https://www.typescriptlang.org/docs/handbook/functions.html)
- [MDN Web Docs: Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)