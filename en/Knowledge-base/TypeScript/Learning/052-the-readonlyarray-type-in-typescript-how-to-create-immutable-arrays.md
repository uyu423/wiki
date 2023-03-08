---
title: 052: The ReadonlyArray Type in TypeScript: How to Create Immutable Arrays
description: 
published: true
date: 2023-03-07T14:32:46.041Z
tags: 
editor: markdown
dateCreated: 2023-03-07T14:32:38.540Z
---

- [052: TypeScript의 ReadonlyArray 유형: 불변 배열을 만드는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/052-the-readonlyarray-type-in-typescript-how-to-create-immutable-arrays)
{.links-list}



The ReadonlyArray Type in TypeScript: How to Create Immutable Arrays

Arrays are one of the most commonly used data structures in programming, and TypeScript provides a lot of features to work with them. However, sometimes we need to create immutable arrays that cannot be modified once created. In this post, we will explore how to create immutable arrays in TypeScript using the ReadonlyArray type.

## What is the ReadonlyArray Type?

The ReadonlyArray type is a built-in type in TypeScript that represents an array whose elements cannot be modified once created. It is similar to the Array type but with one key difference: the ReadonlyArray type provides read-only access to the elements of the array.

Here is an example of how to create a ReadonlyArray in TypeScript:

```typescript
const myArray: ReadonlyArray<string> = ["foo", "bar", "baz"];
```

In this example, we create a ReadonlyArray of strings with three elements. Once created, we cannot modify the elements of the array.

## Creating ReadonlyArrays from Arrays

One way to create a ReadonlyArray is to convert an existing Array to a ReadonlyArray. TypeScript provides a convenient method for doing this: the `as const` assertion.

Here is an example:

```typescript
const myArray = ["foo", "bar", "baz"] as const;
```

In this example, we create an Array of strings and then convert it to a ReadonlyArray using the `as const` assertion. Once created, we cannot modify the elements of the array.

## ReadonlyArrays and Mutability

It's important to note that the ReadonlyArray type only provides read-only access to the elements of the array. It does not prevent the array from being modified in other ways. For example, we can still add or remove elements from a ReadonlyArray:

```typescript
const myArray: ReadonlyArray<string> = ["foo", "bar", "baz"];

// This will throw a TypeError:
myArray[0] = "qux";

// This is allowed:
myArray.push("qux");
```

In this example, we attempt to modify the first element of the ReadonlyArray, which throws a TypeError. However, we can still add elements to the array using the `push` method.

## ReadonlyArrays and Type Inference

TypeScript has excellent type inference capabilities, and this extends to ReadonlyArrays. When we create a ReadonlyArray using the `as const` assertion, TypeScript infers the correct types for the elements of the array.

Here is an example:

```typescript
const myArray = ["foo", "bar", "baz"] as const;

// TypeScript infers that myArray is a ReadonlyArray<string>.
```

In this example, TypeScript infers that `myArray` is a ReadonlyArray of strings.

## Working with ReadonlyArrays

Working with ReadonlyArrays is similar to working with regular Arrays. We can access elements using bracket notation and iterate over the elements using a for loop or the `forEach` method.

Here is an example:

```typescript
const myArray: ReadonlyArray<string> = ["foo", "bar", "baz"];

// Accessing elements:
const firstElement = myArray[0]; // "foo"

// Iterating over elements:
myArray.forEach((element) => {
  console.log(element);
});
```

In this example, we access the first element of the ReadonlyArray using bracket notation and iterate over the elements using the `forEach` method.

## Additional Information

- The ReadonlyArray type is only available in TypeScript 3.4 and above.
- The ReadonlyArray type is a deep readonly type, which means that any nested objects or arrays are also read-only.

## Conclusion

In this post, we explored how to create immutable arrays in TypeScript using the ReadonlyArray type. We learned how to create ReadonlyArrays from Arrays, how ReadonlyArrays work with mutability, and how to work with ReadonlyArrays. With this knowledge, you can create more robust and predictable code in your TypeScript projects.

## Further Reading

- [TypeScript Handbook: ReadonlyArray](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#readonlyarrayt)
- [TypeScript Deep Readonly](https://devblogs.microsoft.com/typescript/announcing-typescript-3-4-rc/#deep-readonly)