---
title: 049: The Omit Type in TypeScript: How to Create Types by Removing Properties from Other Types
description: 
published: true
date: 2023-03-11T12:32:40.677Z
tags: 
editor: markdown
dateCreated: 2023-03-11T12:32:40.677Z
---

- [049: TypeScript의 생략 유형: 다른 유형에서 속성을 제거하여 유형을 만드는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/049-the-omit-type-in-typescript-how-to-create-types-by-removing-properties-from-other-types)
{.links-list}



Creating new types in TypeScript is a common task for developers. In many cases, we need to create a new type based on an existing one, but with some properties removed. TypeScript provides a convenient way to do this with the Omit type.

In this post, we'll explore how to use the Omit type in TypeScript to create new types by removing properties from existing types.

## What is the Omit Type in TypeScript?

The Omit type is a built-in utility type in TypeScript that allows us to create a new type by removing properties from another type. It takes two type parameters: the original type and the names of the properties to be removed.

Here's the syntax for using the Omit type:

```typescript
type NewType = Omit<OriginalType, 'Property1' | 'Property2'>;
```

In this example, we're creating a new type called `NewType` by removing the properties 'Property1' and 'Property2' from the `OriginalType`.

## Using the Omit Type in Practice

Let's see how the Omit type works in practice by creating some examples.

### Example 1: Removing a Single Property

Suppose we have an interface called `Person` that has three properties: `name`, `age`, and `email`.

```typescript
interface Person {
  name: string;
  age: number;
  email: string;
}
```

Now, we want to create a new type called `PersonWithoutEmail` that has the same properties as `Person`, except for the `email` property.

We can use the Omit type to achieve this:

```typescript
type PersonWithoutEmail = Omit<Person, 'email'>;
```

The resulting type will be:

```typescript
interface PersonWithoutEmail {
  name: string;
  age: number;
}
```

### Example 2: Removing Multiple Properties

Suppose we have an interface called `Car` that has four properties: `make`, `model`, `year`, and `color`.

```typescript
interface Car {
  make: string;
  model: string;
  year: number;
  color: string;
}
```

Now, we want to create a new type called `CarSummary` that has the same properties as `Car`, except for the `year` and `color` properties.

We can use the Omit type to achieve this:

```typescript
type CarSummary = Omit<Car, 'year' | 'color'>;
```

The resulting type will be:

```typescript
interface CarSummary {
  make: string;
  model: string;
}
```

### Example 3: Removing Properties Dynamically

In some cases, we may need to remove properties from a type dynamically, based on some condition. For example, suppose we have an interface called `Product` that has three properties: `name`, `price`, and `description`.

```typescript
interface Product {
  name: string;
  price: number;
  description: string;
}
```

Now, we want to create a new type called `ProductWithoutDescription` that has the same properties as `Product`, except for the `description` property, but only if the `description` property exists on the `Product` type.

We can use a conditional type to achieve this:

```typescript
type ProductWithoutDescription = 'description' extends keyof Product
  ? Omit<Product, 'description'>
  : Product;
```

In this example, we're using a conditional type to check if the `description` property exists on the `Product` type. If it does, we use the Omit type to create a new type without the `description` property. Otherwise, we just use the original `Product` type.

## Additional Information

- The Omit type is available in TypeScript 3.5 and later.

## Conclusion

The Omit type is a powerful utility type in TypeScript that allows us to easily create new types by removing properties from existing types. By using the Omit type, we can write more concise and maintainable code.