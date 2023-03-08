---
title: 002: Basic Types in TypeScript: Understanding Variables and Data Types
description: 
published: true
date: 2023-03-02T08:41:18.168Z
tags: 
editor: markdown
dateCreated: 2023-03-02T08:41:16.763Z
---

- [002: TypeScript의 기본 유형: 변수 및 데이터 유형 이해***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/002-basic-types-in-typescript-understanding-variables-and-data-types)
{.links-list}


Basic Types in TypeScript: Understanding Variables and Data Types

TypeScript is a superset of JavaScript that adds optional static typing and class-based object-oriented programming features. It is designed to make large-scale web applications more manageable and easier to maintain. One of the most fundamental concepts in TypeScript is the concept of variables and data types. In this post, we will discuss basic types in TypeScript and how to use them in your code.

## Variables in TypeScript

Variables in TypeScript are declared using the `let` keyword. They can be assigned a value of any type, but once a variable is assigned a value of a particular type, it cannot be assigned a value of a different type. This is because TypeScript is a statically-typed language, which means that the type of a variable is determined at compile time rather than at runtime.

### Example

```typescript
let age: number;
age = 30;
```

In this example, we declare a variable `age` of type `number` and assign it a value of `30`. The type of the variable is inferred to be `number` because we explicitly specify its type.

### Type Inference

TypeScript has a feature called type inference, which allows the type of a variable to be inferred from its value. This means that you don't always have to specify the type of a variable explicitly.

### Example

```typescript
let name = "John";
```

In this example, we declare a variable `name` and assign it a value of `"John"`. The type of the variable is inferred to be `string` because its value is a string.

### Constants

Constants are variables that cannot be reassigned once they are initialized. They are declared using the `const` keyword.

### Example

```typescript
const pi = 3.14;
```

In this example, we declare a constant `pi` and assign it a value of `3.14`. Once a constant is assigned a value, it cannot be reassigned.

## Basic Types in TypeScript

TypeScript provides several basic types that can be used to declare variables. These include:

- `number`
- `string`
- `boolean`
- `null`
- `undefined`

### Number

The `number` type is used to represent numeric values. It includes both integer and floating-point numbers.

### Example

```typescript
let age: number = 30;
let height: number = 1.75;
```

In this example, we declare two variables `age` and `height` of type `number`.

### String

The `string` type is used to represent textual data. It includes both single-quoted and double-quoted strings.

### Example

```typescript
let name: string = "John";
let message: string = 'Hello, world!';
```

In this example, we declare two variables `name` and `message` of type `string`.

### Boolean

The `boolean` type is used to represent logical values. It includes only two possible values: `true` and `false`.

### Example

```typescript
let isDone: boolean = false;
```

In this example, we declare a variable `isDone` of type `boolean`.

### Null and Undefined

The `null` and `undefined` types are used to represent the absence of a value.

### Example

```typescript
let x: null = null;
let y: undefined = undefined;
```

In this example, we declare two variables `x` and `y` of types `null` and `undefined`, respectively.

### Type Assertion

TypeScript allows you to explicitly specify the type of a variable using a syntax called type assertion. This is useful when the type of a variable cannot be inferred automatically.

### Example

```typescript
let someValue: any = "this is a string";
let strLength: number = (<string>someValue).length;
```

In this example, we declare a variable `someValue` of type `any` and assign it a value of `"this is a string"`. We then use type assertion to specify that `someValue` is a string, and assign its length to a variable `strLength`.

## Conclusion

In this post, we discussed the basic types in TypeScript and how to use them in your code. We covered variables, type inference, constants, and type assertion. Understanding these concepts is essential for working with TypeScript, and will help you write more robust and maintainable code.

## Additional Information

- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [TypeScript Playground](https://www.typescriptlang.org/play)