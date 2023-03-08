---
title: 036: Mapped Types in TypeScript: How to Transform Types with Mappings
description: 
published: true
date: 2023-03-03T07:32:31.711Z
tags: 
editor: markdown
dateCreated: 2023-03-03T07:32:24.543Z
---

- [036: TypeScript의 매핑된 유형: 매핑으로 유형을 변환하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/036-mapped-types-in-typescript-how-to-transform-types-with-mappings)
{.links-list}


Mapped Types in TypeScript: How to Transform Types with Mappings

TypeScript is an open-source language that is a superset of JavaScript. It provides static typing, which makes code more reliable and helps to avoid errors. One of the key features of TypeScript is mapped types. Mapped types provide a way to transform types by mapping properties of one type to another. In this post, we will explore mapped types in TypeScript and learn how to use them.

## Introduction to Mapped Types

Mapped types are a feature in TypeScript that allow you to transform types by mapping properties from one type to another. This can be useful when you need to create a new type based on an existing type but with some modifications. For example, you may want to create a new type that has all the properties of an existing type, but with some properties made optional. Mapped types can help you achieve this.

## Basic Mapped Types

The most basic mapped type is the `Partial` type. The `Partial` type transforms a type by making all of its properties optional. Here is an example:

```typescript
interface Person {
  name: string;
  age: number;
}

type PartialPerson = Partial<Person>;

const partialPerson: PartialPerson = { name: "John" };
```

In this example, we define an interface `Person` with two properties: `name` and `age`. We then define a new type `PartialPerson` using the `Partial` mapped type. This type has the same properties as `Person` but with all properties made optional. We then create a variable `partialPerson` of type `PartialPerson` and assign it an object with only the `name` property specified.

## Mapped Types with Constraints

Mapped types can also be used with constraints. Constraints allow you to limit the properties that can be mapped. For example, you may want to create a new type that has all the properties of an existing type, except for a few properties that you want to exclude. Here is an example:

```typescript
interface Person {
  name: string;
  age: number;
  address: string;
}

type ExcludeAddress<T> = {
  [P in keyof T as Exclude<P, "address">]: T[P];
};

const person: Person = { name: "John", age: 30, address: "123 Main St." };
const personWithoutAddress: ExcludeAddress<Person> = person;
```

In this example, we define an interface `Person` with three properties: `name`, `age`, and `address`. We then define a new type `ExcludeAddress` using a mapped type with a constraint. The constraint is specified using the `keyof` keyword, which returns the keys of a type as a union type. The `Exclude` utility type is then used to exclude the `address` property from the union type. The resulting type is a new type that has all the properties of `Person`, except for the `address` property.

We then create a variable `person` of type `Person` and assign it an object with all three properties specified. We then create a variable `personWithoutAddress` of type `ExcludeAddress<Person>` and assign it the `person` object. The `personWithoutAddress` object has all the properties of `person`, except for the `address` property.

## Mapped Types with Optional Properties

Mapped types can also be used to create types with optional properties. Here is an example:

```typescript
interface Person {
  name: string;
  age: number;
  address: {
    street: string;
    city: string;
    state: string;
  };
}

type PartialAddress<T> = {
  [P in keyof T]: P extends "address" ? Partial<T[P]> : T[P];
};

const person: Person = {
  name: "John",
  age: 30,
  address: { street: "123 Main St.", city: "Anytown", state: "CA" },
};

const personWithPartialAddress: PartialAddress<Person> = {
  name: "John",
  age: 30,
  address: { street: "123 Main St." },
};
```

In this example, we define an interface `Person` with three properties: `name`, `age`, and `address`. The `address` property is an object with three properties: `street`, `city`, and `state`. We then define a new type `PartialAddress` using a mapped type with optional properties. The `Partial` utility type is used to make the `address` property optional. The resulting type is a new type that has all the properties of `Person`, with the `address` property made optional.

We then create a variable `person` of type `Person` and assign it an object with all three properties specified. We then create a variable `personWithPartialAddress` of type `PartialAddress<Person>` and assign it an object with only the `name` and `age` properties specified, and the `address` property made optional.

## Conclusion

Mapped types are a powerful feature in TypeScript that allow you to transform types by mapping properties from one type to another. They can be used to create new types with optional properties, exclude properties, and more. By using mapped types, you can make your code more flexible and easier to work with.

## Additional Information

- TypeScript Handbook on Mapped Types: https://www.typescriptlang.org/docs/handbook/2/mapped-types.html

## Warnings

- When using mapped types, be careful not to create circular references. This can cause TypeScript to enter an infinite loop and crash.

## Dangers

- Mapped types can be complex and difficult to understand. It is important to read the documentation and understand the examples before using them in your code.

