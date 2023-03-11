---
title: 029: Type Predicates in TypeScript: How to Write Custom Type Guards
description: 
published: true
date: 2023-03-11T14:33:11.182Z
tags: 
editor: markdown
dateCreated: 2023-03-11T14:33:11.182Z
---

- [029: TypeScript의 유형 술어: 사용자 정의 유형 가드를 작성하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/029-type-predicates-in-typescript-how-to-write-custom-type-guards)
{.links-list}



Type Predicates in TypeScript: How to Write Custom Type Guards

TypeScript is a superset of JavaScript that provides static typing and other features to help developers write more robust and maintainable code. One of the most powerful features of TypeScript is its type system, which allows developers to define custom types and interfaces that can be used to enforce type safety across their codebase.

One of the key tools for working with TypeScript's type system is type predicates. Type predicates allow developers to write custom type guards that can be used to narrow down the type of a variable at runtime. In this post, we'll explore how to write custom type guards in TypeScript using type predicates.

## What are Type Predicates?

In TypeScript, a type predicate is a function that returns a boolean value and is used to narrow down the type of a variable. Type predicates are typically used in conjunction with the `typeof` and `instanceof` operators to determine the type of a variable at runtime.

For example, let's say we have a function that takes an argument of type `unknown` and we want to determine whether that argument is a string. We could write a custom type guard using a type predicate like this:

```typescript
function isString(value: unknown): value is string {
  return typeof value === 'string';
}
```

In this example, we define a function called `isString` that takes an argument of type `unknown` and returns a boolean value. The `value is string` syntax is a type assertion that tells TypeScript that if the `isString` function returns `true`, then the type of `value` should be narrowed down to `string`.

We can then use this type guard to determine whether a variable is a string at runtime:

```typescript
function processValue(value: unknown) {
  if (isString(value)) {
    // value is now of type string
    console.log(value.toUpperCase());
  } else {
    console.log('Value is not a string');
  }
}
```

In this example, the `processValue` function takes an argument of type `unknown` and uses the `isString` type guard to determine whether the argument is a string. If the argument is a string, the function converts it to uppercase and logs it to the console. If the argument is not a string, the function logs a message indicating that the value is not a string.

## How to Write Custom Type Guards

To write a custom type guard in TypeScript, you need to define a function that returns a boolean value and uses a type assertion to narrow down the type of a variable. The syntax for defining a custom type guard is:

```typescript
function isType(value: unknown): value is Type {
  // return true if value is of type Type, false otherwise
}
```

In this syntax, `value` is the variable whose type you want to narrow down, and `Type` is the type you want to narrow it down to. The `is` keyword is used to indicate that the function is a type predicate.

Let's look at a few examples of how to write custom type guards using type predicates.

### Checking for Primitive Types

To check if a variable is a primitive type, you can use the `typeof` operator in conjunction with a type assertion. For example, to check if a variable is a string, you can write:

```typescript
function isString(value: unknown): value is string {
  return typeof value === 'string';
}
```

In this example, the `isString` function returns `true` if the `typeof` operator on `value` is equal to `'string'`. The `value is string` syntax is a type assertion that tells TypeScript to narrow down the type of `value` to `string` if the function returns `true`.

You can use similar techniques to check for other primitive types like `number`, `boolean`, and `symbol`.

### Checking for Object Types

To check if a variable is an object, you can use the `typeof` operator in conjunction with a type assertion. For example, to check if a variable is an array, you can write:

```typescript
function isArray(value: unknown): value is any[] {
  return typeof value === 'object' && Array.isArray(value);
}
```

In this example, the `isArray` function returns `true` if the `typeof` operator on `value` is equal to `'object'` and `value` is an array. The `value is any[]` syntax is a type assertion that tells TypeScript to narrow down the type of `value` to `any[]` if the function returns `true`.

You can use similar techniques to check for other object types like `Map`, `Set`, and `Date`.

### Checking for Custom Types

To check if a variable is a custom type or interface, you can use the `instanceof` operator in conjunction with a type assertion. For example, let's say we have a custom interface called `Person`:

```typescript
interface Person {
  name: string;
  age: number;
}
```

We can write a type guard to check if a variable is of type `Person` like this:

```typescript
function isPerson(value: unknown): value is Person {
  return typeof value === 'object' && value !== null && 'name' in value && 'age' in value;
}
```

In this example, the `isPerson` function returns `true` if `value` is an object that has a `name` property of type `string` and an `age` property of type `number`. The `value is Person` syntax is a type assertion that tells TypeScript to narrow down the type of `value` to `Person` if the function returns `true`.

## Additional Information

Type predicates are a powerful tool for working with TypeScript's type system, but they can also be tricky to use correctly. Here are a few additional tips to keep in mind when working with type predicates:

- Type predicates only work with `unknown` and `any` types. If you want to use a type predicate with a specific type, you need to use a union type that includes `unknown` or `any`.
- Type predicates must return a boolean value. If your type predicate returns anything other than `true` or `false`, TypeScript will throw an error.
- Type predicates can be used with `null` and `undefined` values, but you need to use a type assertion to allow for these values. For example, to check if a variable is a string or `null`, you can write:

```typescript
function isStringOrNull(value: unknown): value is string | null {
  return value === null || typeof value === 'string';
}
```

## Conclusion

Type predicates are a powerful tool for working with TypeScript's type system. By defining custom type guards, you can ensure that your code is type-safe and maintainable. Whether you're checking for primitive types, object types, or custom types, type predicates provide a flexible and robust way to narrow down the type of a variable at runtime.

## Further Reading

- [TypeScript Handbook: Type Guards and Differentiating Types](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-guards-and-differentiating-types)
- [TypeScript Deep Dive: Type Guards and Type Assertions](https://basarat.gitbook.io/typescript/type-system/typeguard#user-defined-type-guards)
- [TypeScript Official Website](https://www.typescriptlang.org/)