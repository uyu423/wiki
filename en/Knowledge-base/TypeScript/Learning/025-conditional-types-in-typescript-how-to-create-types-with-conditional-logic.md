---
title: 025: Conditional Types in TypeScript: How to Create Types with Conditional Logic
description: 
published: true
date: 2023-03-08T08:32:30.197Z
tags: 
editor: markdown
dateCreated: 2023-03-08T08:32:30.197Z
---

- [025: TypeScript의 조건부 유형: 조건부 논리로 유형을 만드는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/025-conditional-types-in-typescript-how-to-create-types-with-conditional-logic)
{.links-list}



Conditional types in TypeScript: How to Create Types with Conditional Logic

TypeScript is a popular programming language that aims to make JavaScript development more productive and efficient. One of the many features that make TypeScript powerful is its support for conditional types, which allow developers to create types based on conditional logic. In this post, we'll explore how to use conditional types in TypeScript to create more flexible and reusable code.

## What are conditional types?

Conditional types are a powerful feature of TypeScript that allow you to define types based on conditions. This means that you can create types that change based on the values of other types. With conditional types, you can create more flexible and reusable code that adapts to different situations.

## Basic syntax

The basic syntax for a conditional type in TypeScript is as follows:

```typescript
type TypeName<T> =
  T extends string ? "string" :
  T extends number ? "number" :
  T extends boolean ? "boolean" :
  T extends undefined ? "undefined" :
  "object";
```

In this example, we define a type called `TypeName` that takes a generic type parameter `T`. We then use the `extends` keyword to create a series of conditional statements that check if `T` extends certain types. If `T` extends a string, number, boolean, or undefined, we return a string literal type that corresponds to that type. Otherwise, we return the string literal type "object".

## Using conditional types

Conditional types are most useful when you need to create types that depend on other types. For example, you might have a function that takes an object with a certain shape, but you want to allow for optional properties. You can use a conditional type to create a new type that includes the optional properties.

```typescript
interface Person {
  name: string;
  age: number;
  address?: string;
}

type OptionalPerson = {
  [K in keyof Person]?: Person[K];
}
```

In this example, we define an interface called `Person` with three properties: `name`, `age`, and `address`. We then define a type called `OptionalPerson` that uses a conditional type to create a new type with all the properties of `Person`, but with the `address` property made optional.

## Advanced conditional types

Conditional types can be used in more complex scenarios as well. For example, you might want to create a type that only includes certain properties from another type.

```typescript
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
}

interface Person {
  name: string;
  age: number;
  address: string;
}

type NameAndAge = Pick<Person, "name" | "age">;
```

In this example, we define a `Pick` type that takes two type parameters: `T` and `K`. The `T` parameter is the type we want to pick properties from, and the `K` parameter is a union of keys from `T` that we want to include in the new type. We use a conditional type to create a new type with only the selected properties.

## Conclusion

Conditional types are a powerful feature of TypeScript that allow you to create more flexible and reusable code. By defining types based on conditions, you can create types that adapt to different situations and make your code more robust. With the examples we've covered in this post, you should be well-equipped to start using conditional types in your own TypeScript projects.

## Additional Resources

- [TypeScript Handbook: Conditional Types](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html)
- [TypeScript Deep Dive: Conditional Types](https://basarat.gitbook.io/typescript/type-system/conditional-types)