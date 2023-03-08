---
title: 008: Generics in TypeScript: How to Write Reusable Code with Type Parameters
description: 
published: true
date: 2023-03-07T20:32:45.647Z
tags: 
editor: markdown
dateCreated: 2023-03-07T20:32:38.025Z
---

- [008: TypeScript의 제네릭: 유형 매개변수로 재사용 가능한 코드를 작성하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/008-generics-in-typescript-how-to-write-reusable-code-with-type-parameters)
{.links-list}



Generics in TypeScript: How to Write Reusable Code with Type Parameters

Have you ever found yourself writing the same code over and over again for different types? Or maybe you've encountered a situation where you need to write a function that can work with different types of data? This is where generics in TypeScript come in handy.

In this post, we'll explore what generics are and how to use them in TypeScript to write reusable code with type parameters.

## What are Generics?

Generics are a way to write code that can work with multiple types. They allow you to define a type or function with placeholders for the type of data it will work with. This makes it possible to write code that is highly reusable and flexible.

Generics in TypeScript are similar to those in other programming languages like Java and C#. They allow you to write code that doesn't depend on a specific type, but instead works with any type that meets certain requirements.

## Why Use Generics?

Generics are useful in situations where you need to write code that can work with different types of data. They help you avoid writing duplicate code for similar types and make your code more flexible and reusable.

For example, let's say you have a function that takes an array of strings and returns the first element:

```typescript
function getFirstElement(arr: string[]): string {
  return arr[0];
}
```

If you need to get the first element of an array of numbers, you would have to write a separate function:

```typescript
function getFirstNumber(arr: number[]): number {
  return arr[0];
}
```

With generics, you can write a single function that can work with any type of array:

```typescript
function getFirstElement<T>(arr: T[]): T {
  return arr[0];
}
```

The `<T>` after the function name declares a type parameter that can be any type. The rest of the function uses `T` as a placeholder for the actual type.

## How to Use Generics in TypeScript

To use generics in TypeScript, you need to declare a type parameter with the `<` and `>` symbols after the name of the function or class. You can use any name for the type parameter, but by convention, `T` is used for a single type parameter and `K` and `V` are used for key and value types in maps and dictionaries.

Here's an example of a generic function that takes two arguments of the same type and returns an array of those values:

```typescript
function createArray<T>(a: T, b: T): T[] {
  return [a, b];
}
```

The function takes two arguments of type `T`, which can be any type. The function returns an array of `T`, which is the same type as the arguments.

You can also use multiple type parameters in a single function. Here's an example of a function that takes two arguments of different types and returns an object with those values:

```typescript
function createObject<K, V>(key: K, value: V): { [key: string]: V } {
  const obj = {};
  obj[key.toString()] = value;
  return obj;
}
```

The function takes two arguments of different types `K` and `V`. The function returns an object with a key of type `string` and a value of type `V`. The key is converted to a string using the `toString()` method.

## Additional Information

Generics can be used with classes, interfaces, and functions. They allow you to write highly reusable code that can work with multiple types.

When using generics, it's important to understand the constraints of the type parameter. You can use the `extends` keyword to specify that the type parameter must be a subtype of a certain type.

For example, if you have a function that only works with objects that have a `name` property, you can specify that the type parameter must extend an interface with a `name` property:

```typescript
interface Named {
  name: string;
}

function getName<T extends Named>(obj: T): string {
  return obj.name;
}
```

The `<T extends Named>` declares that `T` must be a subtype of `Named`, which has a `name` property.

## Warnings and Dangers

Using generics can make your code more complex and harder to read. It's important to use them only when necessary and to keep the code as simple as possible.

When using generics, be careful not to create too many type parameters or constraints. This can make the code harder to understand and maintain.

## Conclusion

Generics are a powerful feature of TypeScript that allow you to write highly reusable code with type parameters. They can make your code more flexible and reduce duplication.

In this post, we've covered the basics of generics in TypeScript, including what they are, why you should use them, and how to use them in your code. With this knowledge, you can start writing more flexible and reusable code in TypeScript.

## Further Reading

- [TypeScript Generics](https://www.typescriptlang.org/docs/handbook/generics.html)
- [TypeScript Generics Tutorial](https://www.tutorialsteacher.com/typescript/typescript-generics)