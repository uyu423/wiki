---
title: 034: Function Overloading in TypeScript: How to Create Functions with Multiple Signatures
description: 
published: true
date: 2023-03-09T21:32:31.941Z
tags: 
editor: markdown
dateCreated: 2023-03-09T21:32:31.941Z
---

- [034: TypeScript의 함수 오버로딩: 여러 서명으로 함수를 만드는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/034-function-overloading-in-typescript-how-to-create-functions-with-multiple-signatures)
{.links-list}



Function Overloading in TypeScript: How to Create Functions with Multiple Signatures

Function overloading is a powerful feature in TypeScript that allows developers to create functions with multiple signatures. This feature enables functions to accept different parameter types and return different types based on the context in which they are called.

In this post, we will explore function overloading in TypeScript and learn how to create functions with multiple signatures.

## What is Function Overloading?

Function overloading refers to the ability to define multiple functions with the same name but different parameter types and return types. In other words, function overloading allows developers to define a function with multiple signatures.

When a function is overloaded, TypeScript uses the function signature to determine which implementation to use at runtime. This feature is particularly useful when creating functions that can accept different types of parameters or return different types of values depending on the context in which they are called.

## How to Create Function Overloading in TypeScript

To create function overloading in TypeScript, we need to define multiple function signatures for the same function. Each signature should have a unique set of parameters and return types.

Here's an example:

```typescript
function add(a: number, b: number): number;
function add(a: string, b: string): string;
function add(a: any, b: any): any {
  return a + b;
}
```

In this example, we have defined three function signatures for the `add` function. The first signature accepts two `number` parameters and returns a `number`. The second signature accepts two `string` parameters and returns a `string`. The third signature is a catch-all signature that accepts any type of parameters and returns any type.

When we call the `add` function, TypeScript will use the function signature to determine which implementation to use at runtime. For example:

```typescript
const result1 = add(1, 2); // returns 3
const result2 = add('hello', 'world'); // returns 'helloworld'
const result3 = add(true, false); // returns truefalse
```

In this example, the first call to `add` uses the first signature, which accepts two `number` parameters and returns a `number`. The second call to `add` uses the second signature, which accepts two `string` parameters and returns a `string`. The third call to `add` uses the catch-all signature, which accepts any type of parameters and returns any type.

## Additional Information

When defining function overloading in TypeScript, it's important to remember that the catch-all signature should always be the last signature in the list. This ensures that TypeScript will use the more specific signatures before falling back to the catch-all signature.

## Conclusion

Function overloading is a powerful feature in TypeScript that allows developers to create functions with multiple signatures. This feature enables functions to accept different parameter types and return different types based on the context in which they are called.

In this post, we have learned how to create function overloading in TypeScript and explored some best practices for defining multiple signatures. By using function overloading, we can create more flexible and robust functions that can handle different types of inputs and outputs.

## Further Reading

- [TypeScript Handbook: Function Overloads](https://www.typescriptlang.org/docs/handbook/2/functions.html#overloads)
- [TypeScript Deep Dive: Function Overloading](https://basarat.gitbook.io/typescript/type-system/functions#function-overloading)