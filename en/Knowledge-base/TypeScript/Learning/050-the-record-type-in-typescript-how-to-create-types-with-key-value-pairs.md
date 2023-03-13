---
title: 050: The Record Type in TypeScript: How to Create Types with Key-Value Pairs
description: 
published: true
date: 2023-03-13T03:32:39.494Z
tags: 
editor: markdown
dateCreated: 2023-03-13T03:32:39.494Z
---

- [050: TypeScript의 레코드 유형: 키-값 쌍으로 유형을 생성하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/050-the-record-type-in-typescript-how-to-create-types-with-key-value-pairs)
{.links-list}



The Record Type in TypeScript: How to Create Types with Key-Value Pairs

TypeScript is a popular programming language that is widely used in web development. It is an extension of JavaScript that adds static typing and other features to the language. One of the features that make TypeScript stand out is its support for advanced types, such as the Record type.

In this post, we will explore the Record type in TypeScript and learn how to create types with key-value pairs.

## What is the Record Type?

The Record type is a built-in type in TypeScript that allows you to create an object type with key-value pairs. It is similar to the object type, but with a specific set of keys and values.

The syntax for defining a Record type is as follows:

```typescript
type RecordType = Record<Keys, Type>;
```

Here, the `Keys` parameter is a union of string literal types that represent the keys of the object, and the `Type` parameter is the type of the values associated with each key.

For example, suppose we want to create a type that represents a user object with a name, age, and email. We can define a Record type as follows:

```typescript
type User = Record<'name' | 'age' | 'email', string>;
```

This creates a type called `User` that represents an object with three keys (`name`, `age`, and `email`) and string values.

## Creating Record Types

To create a Record type, you can use the `Record` utility type provided by TypeScript. The `Record` type takes two parameters: the keys and the values.

Here's an example of how to create a Record type:

```typescript
type MyRecord = Record<'key1' | 'key2', number>;
```

This creates a type called `MyRecord` that represents an object with two keys (`key1` and `key2`) and number values.

You can also use a type alias to define a Record type:

```typescript
type MyRecord = {
  key1: number;
  key2: number;
};
```

This creates a type called `MyRecord` that represents an object with two keys (`key1` and `key2`) and number values.

## Accessing Record Type Values

To access the values of a Record type, you can use the dot notation or bracket notation:

```typescript
type MyRecord = Record<'key1' | 'key2', number>;

const record: MyRecord = {
  key1: 10,
  key2: 20,
};

console.log(record.key1); // 10
console.log(record['key2']); // 20
```

Here, we create a `MyRecord` object with two keys (`key1` and `key2`) and assign values to them. We can then access the values using the dot notation (`record.key1`) or bracket notation (`record['key2']`).

## Additional Information

- The Record type is useful when you need to define an object with a specific set of keys and values.
- The keys of a Record type can be any string literal type, including union types.
- The values of a Record type can be any type, including primitive types, object types, and function types.

## Conclusion

The Record type is a powerful feature of TypeScript that allows you to create types with key-value pairs. It is useful when you need to define an object with a specific set of keys and values. In this post, we learned how to create Record types and access their values. We hope this post helps you in your TypeScript development journey!

## Further Reading

- [TypeScript Handbook: Record Type](https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkeystype)
- [TypeScript Deep Dive: Record Type](https://basarat.gitbook.io/typescript/type-system/utility-types#record)