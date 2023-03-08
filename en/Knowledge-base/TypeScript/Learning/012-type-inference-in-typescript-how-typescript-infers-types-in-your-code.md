---
title: 012: Type Inference in TypeScript: How TypeScript Infers Types in Your Code
description: 
published: true
date: 2023-03-04T06:32:37.085Z
tags: 
editor: markdown
dateCreated: 2023-03-04T06:32:29.703Z
---

- [012: TypeScript에서 유형 추론: TypeScript가 코드에서 유형을 추론하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/012-type-inference-in-typescript-how-typescript-infers-types-in-your-code)
{.links-list}


Type inference is a powerful feature of TypeScript that allows the compiler to automatically infer the types of variables and expressions in your code. This feature makes it easier to write and maintain code, as you don't have to manually specify types for every variable or function parameter.

In this post, we'll take a closer look at how type inference works in TypeScript and how you can take advantage of it in your own code.

## What is Type Inference?

Type inference is the process of determining the type of a variable or expression based on its usage in your code. In other words, TypeScript can look at how you're using a variable or expression and automatically determine its type.

For example, let's say you have a variable `name` that is initialized with a string:

```typescript
let name = "John";
```

TypeScript can infer that the type of `name` is `string`, based on the fact that it's being initialized with a string value.

Similarly, if you have a function that takes a parameter `age` and returns a boolean based on whether the age is greater than 18:

```typescript
function isAdult(age: number) {
  return age > 18;
}
```

TypeScript can infer that the type of `age` is `number`, based on the fact that it's being used in a comparison operation.

## How Does Type Inference Work?

TypeScript uses a process called "contextual typing" to infer types in your code. This means that the type of a variable or expression is inferred based on the context in which it's used.

For example, let's say you have a function that takes a parameter `person` and returns their name:

```typescript
function getName(person: { name: string }) {
  return person.name;
}
```

In this case, TypeScript can infer that the type of `person` is an object with a property `name` of type `string`. This is because the function is expecting an object with a `name` property, and it's using the `name` property in the return statement.

## Type Inference with Generics

Type inference also works with generics in TypeScript. Generics allow you to write code that can work with a variety of types, without knowing the exact type in advance.

For example, let's say you have a function that takes an array of values and returns the first value:

```typescript
function getFirst<T>(arr: T[]): T {
  return arr[0];
}
```

In this case, the `T` in the function signature represents a generic type that can be any type. TypeScript can infer the type of `T` based on the type of the array that's passed in.

For example, if you call the function with an array of strings:

```typescript
const first = getFirst(["hello", "world"]);
```

TypeScript can infer that the type of `first` is `string`, based on the fact that the array passed to `getFirst` is an array of strings.

## Limitations of Type Inference

While type inference can be very helpful in reducing the amount of code you need to write, it's important to note that it's not always possible for TypeScript to infer types correctly.

In some cases, the type of a variable or expression may be ambiguous, or there may be multiple possible types that could be inferred. In these cases, you may need to manually specify the type using a type annotation.

For example, let's say you have a variable `age` that is initialized with a numeric string:

```typescript
let age = "20";
```

In this case, TypeScript may infer the type of `age` as `string`, even though you intended it to be a number. To fix this, you can manually specify the type using a type annotation:

```typescript
let age: number = parseInt("20");
```

## Conclusion

Type inference is a powerful feature of TypeScript that allows the compiler to automatically infer the types of variables and expressions in your code. By understanding how type inference works, you can write more concise and maintainable code.

While type inference is not always perfect, it can save you a lot of time and effort in writing and maintaining your code. As you become more familiar with TypeScript, you'll start to develop a better sense of when to rely on type inference and when to use type annotations.

## Additional Information

- TypeScript Handbook: [Type Inference](https://www.typescriptlang.org/docs/handbook/type-inference.html)
- TypeScript Deep Dive: [Type Inference](https://basarat.gitbook.io/typescript/type-system/type-inference)
- TypeScript Official Documentation: [Type Inference](https://www.typescriptlang.org/docs/handbook/type-inference.html)

## Warnings

- Be careful when relying solely on type inference, as it's not always 100% accurate.
- If you're unsure about the type of a variable or expression, it's always better to specify the type using a type annotation.

## Dangers

- Using type inference incorrectly can lead to bugs and unexpected behavior in your code. Always test your code thoroughly to ensure that it's working as expected.