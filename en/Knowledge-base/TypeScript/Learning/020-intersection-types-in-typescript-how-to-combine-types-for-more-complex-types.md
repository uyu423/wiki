---
title: 020: Intersection Types in TypeScript: How to Combine Types for More Complex Types
description: 
published: true
date: 2023-03-07T05:32:41.551Z
tags: 
editor: markdown
dateCreated: 2023-03-07T05:32:34.314Z
---

- [020: TypeScript의 교차 유형: 더 복잡한 유형을 위해 유형을 결합하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/020-intersection-types-in-typescript-how-to-combine-types-for-more-complex-types)
{.links-list}



Intersection Types in TypeScript: How to Combine Types for More Complex Types

TypeScript is a superset of JavaScript. It adds static typing to the language, making it easier to catch errors at compile time. TypeScript has many features that help developers write better code, including intersection types. Intersection types allow developers to combine multiple types into a single type. This can be useful when working with complex data structures or APIs.

In this post, we will explore intersection types in TypeScript and learn how to use them to create more complex types.

## What are Intersection Types?

Intersection types allow developers to combine multiple types into a single type. This means that a variable can have all the properties and methods of multiple types. For example, if we have two types `A` and `B`, we can create a new type `C` that has all the properties and methods of both `A` and `B`.

```typescript
type A = {
  foo: string;
};

type B = {
  bar: number;
};

type C = A & B;

const c: C = {
  foo: "Hello",
  bar: 42,
};
```

In the example above, we have two types `A` and `B`. We then create a new type `C` that combines the properties of both `A` and `B` using the `&` operator. Finally, we create a variable `c` of type `C` that has all the properties of both `A` and `B`.

## Using Intersection Types in Functions

Intersection types can also be used in functions. This can be useful when working with APIs that return complex data structures. For example, let's say we have an API that returns a user object with the following properties:

```typescript
type User = {
  id: number;
  name: string;
  email: string;
};
```

We also have a function that takes a user object and logs the user's name and email:

```typescript
function logUser(user: User) {
  console.log(`Name: ${user.name}, Email: ${user.email}`);
}
```

Now let's say we have another API that returns a user object with additional properties:

```typescript
type AdminUser = {
  id: number;
  name: string;
  email: string;
  isAdmin: boolean;
};
```

We want to use the `logUser` function to log the name and email of an `AdminUser` object. We can do this by using an intersection type:

```typescript
type LogAdminUser = AdminUser & {
  isAdmin: never;
};

function logAdminUser(user: LogAdminUser) {
  logUser(user);
}
```

In the example above, we create a new type `LogAdminUser` that combines the properties of `AdminUser` and an object with the `never` type, which means it has no properties. We then create a new function `logAdminUser` that takes a `LogAdminUser` object and calls the `logUser` function with that object. This allows us to use the `logUser` function with both `User` and `AdminUser` objects.

## Additional Information

When using intersection types, it's important to remember that the resulting type will have all the properties and methods of both types. This can lead to conflicts if the two types have properties or methods with the same name. In that case, TypeScript will generate an error.

## Conclusion

Intersection types are a powerful feature of TypeScript that allow developers to combine multiple types into a single type. This can be useful when working with complex data structures or APIs. In this post, we learned how to use intersection types to create more complex types and how to use them in functions. We also learned about potential conflicts when using intersection types.

If you want to learn more about TypeScript, check out the following resources:

- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/)
- [TypeScript in 5 minutes](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html)