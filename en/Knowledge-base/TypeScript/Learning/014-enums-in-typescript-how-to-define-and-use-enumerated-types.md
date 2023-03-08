---
title: 014: Enums in TypeScript: How to Define and Use Enumerated Types
description: 
published: true
date: 2023-03-06T17:32:40.042Z
tags: 
editor: markdown
dateCreated: 2023-03-06T17:32:38.673Z
---

- [014: TypeScript의 열거형: 열거형을 정의하고 사용하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/014-enums-in-typescript-how-to-define-and-use-enumerated-types)
{.links-list}



Enums in TypeScript: How to Define and Use Enumerated Types

TypeScript is a popular programming language that provides optional static typing, classes, and interfaces. One of the language's most powerful features is Enums, which allow developers to define and use enumerated types. In this post, we'll explore what Enums are, how to define them, and how to use them in your TypeScript code.

## What are Enums?

Enums are a way to define a set of named constants in TypeScript. They provide a way to give friendly names to numeric or string values, making your code more readable and easier to understand. Enums can be used in place of magic numbers or string literals, which can make your code more maintainable and less error-prone.

## Defining Enums in TypeScript

To define an Enum in TypeScript, you use the `enum` keyword followed by the name of the Enum. The names of the Enum values are defined inside curly braces, separated by commas. Here's an example:

```typescript
enum Direction {
  Up,
  Down,
  Left,
  Right
}
```

In this example, we define an Enum called `Direction` with four values: `Up`, `Down`, `Left`, and `Right`. By default, TypeScript assigns numeric values to each of the Enum values, starting from 0. So `Up` has a value of 0, `Down` has a value of 1, and so on.

You can also explicitly assign values to Enum values, like this:

```typescript
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT"
}
```

In this example, we assign string values to each of the Enum values.

## Using Enums in TypeScript

To use an Enum in TypeScript, you simply refer to it by name. Here's an example:

```typescript
let direction: Direction = Direction.Up;
console.log(direction); // Output: 0
```

In this example, we declare a variable called `direction` of type `Direction` and assign it the value `Direction.Up`. When we log the value of `direction` to the console, we get the numeric value 0.

You can also use Enums in switch statements, like this:

```typescript
switch (direction) {
  case Direction.Up:
    console.log("Going up!");
    break;
  case Direction.Down:
    console.log("Going down!");
    break;
  case Direction.Left:
    console.log("Going left!");
    break;
  case Direction.Right:
    console.log("Going right!");
    break;
  default:
    console.log("Invalid direction.");
}
```

In this example, we use a switch statement to log a message based on the value of `direction`.

## Additional Information

- You can use Enums with both numeric and string values.
- You can also use Enums with bit flags, which allow you to combine multiple values into a single value.

## Warnings

- Be careful when assigning numeric values to Enums, as it can lead to unexpected behavior if the values are not unique.
- Be careful when using Enums with bit flags, as it can make your code more complex and harder to understand.

## Conclusion

Enums are a powerful feature of TypeScript that allow you to define and use enumerated types. They provide a way to give friendly names to numeric or string values, making your code more readable and easier to understand. By using Enums in your TypeScript code, you can make your code more maintainable and less error-prone.

## Further Reading

- [TypeScript Handbook: Enums](https://www.typescriptlang.org/docs/handbook/enums.html)
- [Enums in TypeScript: The Basics](https://blog.logrocket.com/enums-in-typescript-the-basics-9fd96b0efa8a/)
- [Understanding Enums in TypeScript](https://www.sitepoint.com/understanding-enums-in-typescript/)