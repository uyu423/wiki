---
title: 053: The Required Type in TypeScript: How to Create Types with Required Properties
description: 
published: true
date: 2023-03-04T08:32:30.882Z
tags: 
editor: markdown
dateCreated: 2023-03-04T08:32:29.501Z
---

- [053: TypeScript의 필수 유형: 필수 속성으로 유형을 만드는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/053-the-required-type-in-typescript-how-to-create-types-with-required-properties)
{.links-list}


The Required Type in TypeScript: How to Create Types with Required Properties

TypeScript is a powerful language that provides developers with the ability to write clean and maintainable code. One of the features that TypeScript provides is the ability to define types with required properties. In this post, we will explore what the required type is and how to create types with required properties.

## Understanding the Required Type

The required type is a built-in type in TypeScript that allows developers to define a type with required properties. When a property is defined as required, it means that the property must be present in the object and cannot be undefined or null. 

For example, let's say we have an object called `Person` with two properties, `name` and `age`. To make the `name` property required, we can define the `Person` type as follows:

```typescript
type Person = {
  name: string;
  age?: number;
}
```

In this example, the `age` property is optional, but the `name` property is required. If we try to create a `Person` object without the `name` property, TypeScript will throw an error.

```typescript
const person = {
  age: 30
} // Error: Property 'name' is missing in type '{ age: number; }' but required in type 'Person'.
```

## Creating Types with Required Properties

To create a type with required properties, we can use the `Required` utility type. The `Required` type takes an object type as an argument and returns a new type with all properties set to required.

```typescript
type RequiredPerson = Required<Person>;
```

In this example, the `RequiredPerson` type is created by applying the `Required` utility type to the `Person` type. The resulting type will have all properties set to required, including the `name` property.

```typescript
const requiredPerson: RequiredPerson = {
  name: 'John',
  age: 30
} // OK

const missingName: RequiredPerson = {
  age: 30
} // Error: Property 'name' is missing in type '{ age: number; }' but required in type 'RequiredPerson'.
```

## Working with Deeply Nested Objects

The `Required` type can also be used to create types with required properties in deeply nested objects. Let's say we have an object called `Address` with two properties, `street` and `city`. We can create a new type called `RequiredAddress` with all properties set to required, including the `street` and `city` properties.

```typescript
type Address = {
  street?: string;
  city?: string;
}

type Person = {
  name: string;
  age?: number;
  address?: Address;
}

type RequiredPerson = Required<Person>;
```

In this example, we define the `Person` type with an optional `address` property that is an object of type `Address`. We then apply the `Required` utility type to the `Person` type to create the `RequiredPerson` type with all properties set to required.

```typescript
const requiredPerson: RequiredPerson = {
  name: 'John',
  age: 30,
  address: {
    street: '123 Main St',
    city: 'New York'
  }
} // OK

const missingAddress: RequiredPerson = {
  name: 'John',
  age: 30
} // Error: Property 'address' is missing in type '{ name: string; age: number; }' but required in type 'RequiredPerson'.
```

## Additional Information

When defining types with required properties, it is important to consider the use case and ensure that the properties that are set to required are necessary for the object to function correctly. Overuse of required properties can lead to unnecessary errors and make the code difficult to maintain.

## Conclusion

In this post, we explored the required type in TypeScript and how to create types with required properties. We learned how to use the `Required` utility type to create new types with all properties set to required, and how to work with deeply nested objects. By using the required type, we can ensure that our objects have the necessary properties to function correctly and write clean and maintainable code.

## Further Reading

- [TypeScript Handbook: Required Properties](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-8.html#optional-props-become-readonly-when-used-in-interfaces-and-type-literals)
- [TypeScript Handbook: Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html#required)