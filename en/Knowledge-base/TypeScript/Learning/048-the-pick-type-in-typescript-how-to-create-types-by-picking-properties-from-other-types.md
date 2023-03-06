---
title: 048: The Pick Type in TypeScript: How to Create Types by Picking Properties from Other Types
description: 
published: true
date: 2023-03-06T21:32:39.041Z
tags: 
editor: markdown
dateCreated: 2023-03-06T21:32:39.041Z
---

- [048: TypeScript에서 유형 선택: 다른 유형에서 속성을 선택하여 유형을 만드는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/048-the-pick-type-in-typescript-how-to-create-types-by-picking-properties-from-other-types)
{.links-list}



The Pick Type in TypeScript: How to Create Types by Picking Properties from Other Types

TypeScript is a popular language for building scalable and maintainable applications. One of the key features of TypeScript is its ability to define and use types. In this post, we will explore the Pick type in TypeScript, which allows us to create new types by picking properties from other types.

## What is the Pick Type?

The Pick type is a built-in utility type in TypeScript that allows us to create new types by picking properties from an existing type. It takes two type arguments: the first argument is the source type, and the second argument is a string literal or union of string literals representing the names of the properties to pick.

Here's an example of how to use the Pick type:

```typescript
type Person = {
  name: string;
  age: number;
  address: {
    street: string;
    city: string;
    country: string;
  };
};

type PersonName = Pick<Person, 'name'>;
```

In this example, we have defined a Person type with three properties: name, age, and address. We then create a new type called PersonName by using the Pick type and specifying the Person type as the source type and the string literal 'name' as the property to pick. The resulting type is a new type with only the name property from the Person type.

## Using Pick to Create Subtypes

The Pick type is particularly useful when we want to create subtypes of an existing type. For example, suppose we have a User type with many properties, but we only need a subset of those properties for a particular use case. We can use the Pick type to create a new type that only includes the necessary properties.

Here's an example:

```typescript
type User = {
  id: number;
  name: string;
  email: string;
  createdAt: Date;
  updatedAt: Date;
};

type UserSummary = Pick<User, 'id' | 'name'>;
```

In this example, we define a User type with five properties, including an id, name, email, createdAt, and updatedAt. We then create a new type called UserSummary by using the Pick type and specifying the User type as the source type and a union of string literals ('id' and 'name') as the properties to pick. The resulting type is a new type that only includes the id and name properties from the User type.

## Additional Information

It's important to note that the Pick type creates a new type that only includes the specified properties. Any other properties from the source type are not included in the new type. This can be useful when we want to create subtypes, but it can also lead to unexpected behavior if we're not careful.

## Using Pick with Nested Properties

The Pick type can also be used with nested properties. For example, suppose we have a Person type with an address property that contains nested properties for street, city, and country. We can use the Pick type to create a new type that only includes the street and city properties.

Here's an example:

```typescript
type Person = {
  name: string;
  age: number;
  address: {
    street: string;
    city: string;
    country: string;
  };
};

type PersonAddress = Pick<Person['address'], 'street' | 'city'>;
```

In this example, we create a new type called PersonAddress by using the Pick type and specifying the address property of the Person type as the source type and a union of string literals ('street' and 'city') as the properties to pick. The resulting type is a new type that only includes the street and city properties from the address property of the Person type.

## Warnings

When using the Pick type with nested properties, it's important to remember that the resulting type only includes the specified properties and not the entire nested object. If we need to use the entire nested object, we should use the original type instead of the picked type.

## Conclusion

The Pick type in TypeScript is a powerful tool for creating new types by picking properties from existing types. It can be particularly useful when creating subtypes or when working with nested properties. However, it's important to use the Pick type carefully and to remember that it only includes the specified properties in the resulting type.

## Further Reading

- TypeScript Handbook: [Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktypekeys)
- TypeScript Deep Dive: [Type Utility Functions](https://basarat.gitbook.io/typescript/type-system/typeutilityfunctions)