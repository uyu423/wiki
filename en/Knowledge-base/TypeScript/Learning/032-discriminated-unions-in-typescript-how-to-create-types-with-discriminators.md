---
title: 032: Discriminated Unions in TypeScript: How to Create Types with Discriminators
description: 
published: true
date: 2023-03-07T07:33:06.543Z
tags: 
editor: markdown
dateCreated: 2023-03-07T07:32:59.302Z
---

- [032: TypeScript의 구별된 공용체: 판별자를 사용하여 유형을 만드는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/032-discriminated-unions-in-typescript-how-to-create-types-with-discriminators)
{.links-list}



Discriminated Unions in TypeScript: How to Create Types with Discriminators

TypeScript is a popular programming language that adds type annotations to JavaScript. It provides a lot of features that help developers write better code, including interfaces, classes, and enums. One of the most powerful features of TypeScript is Discriminated Unions. In this post, we will explore what Discriminated Unions are, how they work, and how to create them in TypeScript.

## What are Discriminated Unions?

Discriminated Unions are a pattern in TypeScript that allows you to create types that have a common property, called a discriminator. The discriminator is a property that has a specific value for each type in the union. By using the discriminator, TypeScript can determine which type a variable is at runtime.

For example, let's say we have two types: `Square` and `Rectangle`. Both types have a `type` property, but the value of the `type` property is different for each type.

```typescript
interface Square {
  type: 'square';
  size: number;
}

interface Rectangle {
  type: 'rectangle';
  width: number;
  height: number;
}
```

In this example, the discriminator is the `type` property. The value of the `type` property is `'square'` for the `Square` type and `'rectangle'` for the `Rectangle` type. This means that TypeScript can determine the type of a variable based on the value of its `type` property.

## How do Discriminated Unions work?

When we create a Discriminated Union, we define a type that is a union of several other types. Each type in the union must have a common property that acts as the discriminator. When we create a variable of the union type, we must set the value of the discriminator property to a specific value.

For example, let's create a variable of the `Square | Rectangle` type:

```typescript
let shape: Square | Rectangle;
```

To set the value of the discriminator property, we can use a type assertion or a type guard. A type assertion is a way to tell TypeScript the type of a variable, even if TypeScript can't determine the type on its own. A type guard is a function that checks if a variable is of a certain type.

Here's an example of setting the value of the discriminator property using a type assertion:

```typescript
shape = {
  type: 'square',
  size: 10
} as Square;
```

In this example, we're setting the value of the discriminator property to `'square'` by using a type assertion to tell TypeScript that the object is of type `Square`.

Here's an example of setting the value of the discriminator property using a type guard:

```typescript
function isSquare(shape: Square | Rectangle): shape is Square {
  return shape.type === 'square';
}

if (isSquare(shape)) {
  console.log(shape.size);
} else {
  console.log(shape.width, shape.height);
}
```

In this example, we're using the `isSquare` function as a type guard to determine if the variable is of type `Square`. If the variable is of type `Square`, we can access the `size` property. If the variable is of type `Rectangle`, we can access the `width` and `height` properties.

## How to Create Types with Discriminators

To create a type with a discriminator, we need to define an interface that has a discriminator property. We can then create other interfaces that extend the base interface and add additional properties.

Here's an example of creating a Discriminated Union for different shapes:

```typescript
interface Shape {
  kind: 'circle' | 'square' | 'rectangle';
}

interface Circle extends Shape {
  kind: 'circle';
  radius: number;
}

interface Square extends Shape {
  kind: 'square';
  size: number;
}

interface Rectangle extends Shape {
  kind: 'rectangle';
  width: number;
  height: number;
}
```

In this example, we're defining a base interface `Shape` that has a discriminator property `kind`. We're then creating three interfaces `Circle`, `Square`, and `Rectangle` that extend the `Shape` interface and add additional properties.

We can then create a variable of the `Circle | Square | Rectangle` type and set the value of the discriminator property:

```typescript
let shape: Circle | Square | Rectangle;

shape = {
  kind: 'circle',
  radius: 10
};

shape = {
  kind: 'square',
  size: 10
};

shape = {
  kind: 'rectangle',
  width: 10,
  height: 20
};
```

## Additional Information

Discriminated Unions are a powerful feature of TypeScript that can help you write more type-safe code. By using Discriminated Unions, you can create types that have a common property and use that property to determine the type of a variable at runtime.

## External Resources

- [TypeScript Handbook: Discriminated Unions](https://www.typescriptlang.org/docs/handbook/advanced-types.html#discriminated-unions)
- [TypeScript Deep Dive: Discriminated Unions](https://basarat.gitbook.io/typescript/type-system/discriminated-unions)