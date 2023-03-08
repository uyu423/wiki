---
title: 018: Type Compatibility in TypeScript: How to Ensure Types Are Compatible in Your Code
description: 
published: true
date: 2023-03-02T16:32:24.788Z
tags: 
editor: markdown
dateCreated: 2023-03-02T16:32:17.566Z
---

- [018: TypeScript의 유형 호환성: 코드에서 유형이 호환되는지 확인하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/018-type-compatibility-in-typescript-how-to-ensure-types-are-compatible-in-your-code)
{.links-list}
Type Compatibility in TypeScript: How to Ensure Types Are Compatible in Your Code

TypeScript is a popular open-source programming language widely used for developing large-scale applications. TypeScript supports type annotations, which help developers to write safer and more maintainable code. However, ensuring types are compatible in TypeScript can be a challenge. This post will guide you through type compatibility in TypeScript and how to ensure types are compatible in your code.

## What is Type Compatibility in TypeScript?

Type compatibility in TypeScript refers to the ability of one type to be assigned to another type. For example, consider the following code:

```typescript
let x: boolean = true;
let y: boolean | number = x;
```

In this code, we declare a variable `x` of type `boolean` and a variable `y` of type `boolean | number`. The `|` symbol indicates a union type, which means `y` can be either a `boolean` or a `number`. We then assign the value of `x` to `y`. Since `boolean` is a subtype of `boolean | number`, the assignment is valid.

TypeScript uses structural typing, which means that two types are compatible if their internal structure is compatible. This is different from nominal typing, which compares types based on their name or declaration.

## Ensuring Type Compatibility in TypeScript

To ensure type compatibility in TypeScript, you need to understand the rules of type compatibility. TypeScript has several rules for type compatibility, which include:

### Assignability of Functions

Functions in TypeScript are compatible if their parameter lists and return types are compatible. For example, consider the following code:

```typescript
type Adder = (a: number, b: number) => number;
let add: Adder = (a, b) => a + b;

type Multiplier = (a: number, b: number) => number;
let multiply: Multiplier = (a, b) => a * b;

let operation: Adder = multiply;
```

In this code, we declare two types `Adder` and `Multiplier`, which are functions that take two parameters of type `number` and return a value of type `number`. We then declare two variables `add` and `multiply` of type `Adder` and `Multiplier`, respectively. Finally, we declare a variable `operation` of type `Adder` and assign the value of `multiply` to it. Since the parameter types and return types of `multiply` are compatible with `Adder`, the assignment is valid.

### Assignability of Objects

Objects in TypeScript are compatible if their properties are compatible. For example, consider the following code:

```typescript
interface Person {
  name: string;
  age: number;
}

let person: Person = {
  name: 'John',
  age: 30,
};

let employee = {
  name: 'John',
  age: 30,
  salary: 50000,
};

person = employee;
```

In this code, we declare an interface `Person` with two properties `name` of type `string` and `age` of type `number`. We then declare a variable `person` of type `Person` and assign an object with `name` and `age` properties to it. We then declare a variable `employee` with `name`, `age`, and `salary` properties. Finally, we assign the value of `employee` to `person`. Since `employee` has all the properties of `Person`, the assignment is valid.

### Assignability of Generics

Generics in TypeScript are compatible if their types are compatible. For example, consider the following code:

```typescript
interface Box<T> {
  value: T;
}

let stringBox: Box<string> = { value: 'hello' };
let anyBox: Box<any> = stringBox;
```

In this code, we declare an interface `Box` with a generic type `T` and a property `value` of type `T`. We then declare a variable `stringBox` of type `Box<string>` and assign an object with a `value` property of type `string` to it. We then declare a variable `anyBox` of type `Box<any>` and assign the value of `stringBox` to it. Since `string` is a subtype of `any`, the assignment is valid.

## Additional Information

TypeScript also has rules for type incompatibility, which include:

- Assignability of functions with optional parameters and rest parameters
- Assignability of functions with different arity
- Assignability of objects with excess properties
- Assignability of objects with missing properties

To learn more about these rules, check out the TypeScript documentation.

## Warnings

TypeScript provides warnings for type incompatibility. If you try to assign a value of an incompatible type, TypeScript will show a warning. For example, consider the following code:

```typescript
let x: string = 'hello';
let y: number = x;
```

In this code, we declare a variable `x` of type `string` and assign the value `'hello'` to it. We then declare a variable `y` of type `number` and assign the value of `x` to it. Since `string` is not compatible with `number`, TypeScript will show a warning.

## Dangers

TypeScript cannot catch all type errors. It is possible to write code that compiles without errors but produces unexpected results at runtime. Therefore, it is important to write tests and use good coding practices to ensure your code is correct.

## Conclusion

Type compatibility in TypeScript is an important concept that helps developers write safer and more maintainable code. To ensure type compatibility in TypeScript, you need to understand the rules of type compatibility and use good coding practices. TypeScript provides warnings for type incompatibility, but it is important to write tests to ensure your code is correct.

## Further Reading

- [TypeScript documentation on type compatibility](https://www.typescriptlang.org/docs/handbook/type-compatibility.html)
- [TypeScript documentation on structural typing](https://www.typescriptlang.org/docs/handbook/type-compatibility.html#structural-typing)
- [TypeScript documentation on nominal typing](https://www.typescriptlang.org/docs/handbook/type-compatibility.html#nominal-typing)