---
title: 019: Declaration Merging in TypeScript: How to Merge Multiple Declarations of the Same Entity
description: 
published: true
date: 2023-03-04T15:32:39.299Z
tags: 
editor: markdown
dateCreated: 2023-03-04T15:32:32.183Z
---

- [019: TypeScript에서 선언 병합: 동일한 엔티티의 여러 선언을 병합하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/019-declaration-merging-in-typescript-how-to-merge-multiple-declarations-of-the-same-entity)
{.links-list}


## Introduction

When you are developing software in TypeScript, you may come across scenarios where you need to declare the same entity multiple times. This can happen when you are working with external libraries or when you want to extend an existing type. In such cases, TypeScript provides a feature called "Declaration Merging" that allows you to merge multiple declarations of the same entity into a single definition.

In this post, we will explore the concept of Declaration Merging in TypeScript and learn how to use it effectively.

## What is Declaration Merging?

Declaration Merging is a feature in TypeScript that allows you to combine multiple declarations of the same entity into a single definition. This feature is useful when you are working with external libraries that have their own type definitions or when you want to extend an existing type.

Declaration Merging works by aggregating the declarations of the same entity and creating a single definition that includes all the properties and methods from each declaration. This can be done for interfaces, classes, functions, and namespaces.

## How to Use Declaration Merging

To use Declaration Merging in TypeScript, you need to follow a few rules:

1. All declarations must have the same name and be in the same scope.
2. The declarations must have compatible types.
3. The declarations must not have private or protected members.

Let's look at some examples to understand how to use Declaration Merging.

### Merging Interfaces

Suppose you have two interfaces with the same name:

```typescript
interface Person {
  name: string;
}

interface Person {
  age: number;
}
```

In this case, TypeScript will automatically merge the two interfaces into a single definition:

```typescript
interface Person {
  name: string;
  age: number;
}
```

Now, you can use the `Person` interface with both `name` and `age` properties.

### Merging Functions

Suppose you have two functions with the same name:

```typescript
function greet(name: string): void {
  console.log(`Hello, ${name}!`);
}

function greet(message: number): void {
  console.log(`Your message has ${message} characters.`);
}
```

In this case, TypeScript will automatically merge the two functions into a single definition:

```typescript
function greet(name: string): void;
function greet(message: number): void;
function greet(nameOrMessage: string | number): void {
  if (typeof nameOrMessage === 'string') {
    console.log(`Hello, ${nameOrMessage}!`);
  } else {
    console.log(`Your message has ${nameOrMessage} characters.`);
  }
}
```

Now, you can call the `greet` function with either a string or a number argument.

### Merging Namespaces

Suppose you have two namespaces with the same name:

```typescript
namespace MyNamespace {
  export const name = 'John';
}

namespace MyNamespace {
  export const age = 30;
}
```

In this case, TypeScript will automatically merge the two namespaces into a single definition:

```typescript
namespace MyNamespace {
  export const name = 'John';
  export const age = 30;
}
```

Now, you can access both `name` and `age` properties of the `MyNamespace` namespace.

## Additional Information

Here are some additional things to keep in mind when working with Declaration Merging:

- You can use the `declare` keyword to tell TypeScript that a declaration is external and will be provided at runtime. This is useful when working with libraries that have their own type definitions.
- You can use the `namespace` keyword to group related declarations together. This is useful when you have a large number of declarations and want to organize them into logical groups.
- You can use Declaration Merging to add new properties or methods to an existing type. This is useful when you want to extend an existing type without modifying its original definition.

## Conclusion

Declaration Merging is a powerful feature in TypeScript that allows you to combine multiple declarations of the same entity into a single definition. This feature is useful when you are working with external libraries or when you want to extend an existing type.

By following the rules and guidelines outlined in this post, you can use Declaration Merging effectively and improve the quality of your TypeScript code.

## Further Reading

- [TypeScript Handbook: Declaration Merging](https://www.typescriptlang.org/docs/handbook/declaration-merging.html)
- [TypeScript Deep Dive: Declaration Merging](https://basarat.gitbook.io/typescript/type-system/declaration-merging)