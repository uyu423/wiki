---
title: 031: Non-Nullable Types in TypeScript: How to Ensure Types Are Not Null or Undefined
description: 
published: true
date: 2023-03-10T14:32:59.868Z
tags: 
editor: markdown
dateCreated: 2023-03-10T14:32:59.868Z
---

- [031: TypeScript에서 Null을 허용하지 않는 유형: 유형이 Null이거나 정의되지 않았는지 확인하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/031-non-nullable-types-in-typescript-how-to-ensure-types-are-not-null-or-undefined)
{.links-list}

Non-Nullable Types in TypeScript: How to Ensure Types Are Not Null or Undefined

TypeScript is a popular programming language that adds type annotations to JavaScript. It provides a way to catch errors at compile-time instead of run-time, which makes it easier to maintain code and catch bugs early on. One common issue that TypeScript developers face is dealing with null or undefined values. In this post, we will explore non-nullable types in TypeScript and how to ensure types are not null or undefined.

## What are Non-Nullable Types?

Non-nullable types are a new feature in TypeScript 2.0 that allow developers to indicate that a variable or parameter cannot be null or undefined. This is useful because null and undefined values can cause unexpected behavior and errors in the code.

In TypeScript, non-nullable types are denoted by appending a "!" to the end of the type. For example, "string!" indicates that the variable must be a string and cannot be null or undefined.

## Declaring Non-Nullable Types

To declare a variable as non-nullable, simply add the "!" at the end of the type declaration. For example:

```typescript
let name: string!;
name = "John"; // valid
name = null; // error: Type 'null' is not assignable to type 'string'
```

In this example, the variable "name" is declared as a non-nullable string type. It can only be assigned a string value, and not null or undefined.

Similarly, when declaring a function parameter as non-nullable, add the "!" at the end of the type. For example:

```typescript
function greet(name: string!) {
  console.log("Hello, " + name);
}

greet("John"); // valid
greet(null); // error: Argument of type 'null' is not assignable to parameter of type 'string'
```

In this example, the "name" parameter is declared as a non-nullable string type. It can only be passed a string value, and not null or undefined.

## Optional and Non-Nullable Types

In TypeScript, variables and parameters can also be optional. An optional variable or parameter can be assigned a value of its type or undefined. For example:

```typescript
let age: number;
age = 30; // valid
age = undefined; // valid

function greet(name: string, age?: number) {
  console.log("Hello, " + name);
  if (age !== undefined) {
    console.log("You are " + age + " years old.");
  }
}

greet("John"); // valid
greet("Jane", 25); // valid
greet("Jake", undefined); // valid
```

In this example, the "age" variable is declared as a number, but not as non-nullable. It can be assigned a number or undefined.

The "age" parameter in the "greet" function is declared as optional using the "?" syntax. It can be passed a number or undefined.

To make the "age" parameter non-nullable, simply add the "!" at the end of the type declaration. For example:

```typescript
function greet(name: string, age: number!) {
  console.log("Hello, " + name);
  console.log("You are " + age + " years old.");
}

greet("John", 30); // valid
greet("Jane", undefined); // error: Argument of type 'undefined' is not assignable to parameter of type 'number'
```

In this example, the "age" parameter is declared as non-nullable. It can only be passed a number value, and not undefined.

## Using Non-Nullable Types with Classes

Non-nullable types can also be used with classes in TypeScript. For example:

```typescript
class Person {
  name: string!;
  age: number!;
  
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
  
  greet() {
    console.log("Hello, my name is " + this.name + " and I am " + this.age + " years old.");
  }
}

const john = new Person("John", 30);
john.greet(); // Hello, my name is John and I am 30 years old.

const jane = new Person(null, 25); // error: Type 'null' is not assignable to type 'string'
```

In this example, the "Person" class has non-nullable "name" and "age" properties. When creating a new instance of the class, the "name" and "age" values must be provided and cannot be null or undefined.

## Additional Information

Non-nullable types are a powerful feature in TypeScript that can help catch errors early on in the development process. However, they should be used with caution as they can lead to runtime errors if not used correctly. It is important to thoroughly test code and ensure that non-nullable types are used appropriately.

## Conclusion

In this post, we have explored non-nullable types in TypeScript and how to ensure types are not null or undefined. We have learned how to declare non-nullable variables and parameters, use non-nullable types with optional variables and parameters, and use non-nullable types with classes.

TypeScript provides a way to catch errors at compile-time instead of run-time, which makes it easier to maintain code and catch bugs early on. Non-nullable types are a powerful feature that can help ensure that variables and parameters are not null or undefined, but they should be used with caution. It is important to thoroughly test code and ensure that non-nullable types are used appropriately.

## Further Reading

- [TypeScript documentation on Non-Nullable Types](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html#--strictnullchecks)
- [TypeScript Deep Dive: Non-Nullable Types](https://basarat.gitbook.io/typescript/type-system/non-nullability)