---
title: 017: Tuples in TypeScript: How to Work with Fixed-Length Arrays with Typed Elements
description: 
published: true
date: 2023-03-13T14:33:11.030Z
tags: 
editor: markdown
dateCreated: 2023-03-13T14:33:11.030Z
---

- [017: TypeScript의 튜플: 유형 요소가 있는 고정 길이 배열로 작업하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/017-tuples-in-typescript-how-to-work-with-fixed-length-arrays-with-typed-elements)
{.links-list}



Tuples in TypeScript: How to Work with Fixed-Length Arrays with Typed Elements

In TypeScript, a tuple is a fixed-length array that contains elements of different types. It is a useful data structure when you want to represent a collection of values with a specific order and type.

In this article, we will explore how to work with tuples in TypeScript. We will cover the following topics:

1. Creating a tuple
2. Accessing tuple elements
3. Modifying tuple elements
4. Combining tuples
5. Destructuring tuples
6. Additional information

## 1. Creating a tuple

To create a tuple in TypeScript, you use the following syntax:

```typescript
let myTuple: [string, number] = ["hello", 42];
```

In this example, we create a tuple that contains a string and a number. The variable `myTuple` is declared with the type `[string, number]`. The square brackets indicate that this is a tuple type, and the types inside the brackets specify the types of the elements in the tuple.

You can also use type aliases to define tuple types:

```typescript
type MyTuple = [string, number];
let myTuple: MyTuple = ["hello", 42];
```

This defines a type alias `MyTuple` that represents a tuple of a string and a number. The variable `myTuple` is declared with this type alias.

## 2. Accessing tuple elements

You can access tuple elements using array indexing:

```typescript
let myTuple: [string, number] = ["hello", 42];
let myString: string = myTuple[0];
let myNumber: number = myTuple[1];
```

In this example, we access the first element of the tuple with `myTuple[0]` and assign it to the variable `myString`. We access the second element with `myTuple[1]` and assign it to the variable `myNumber`.

TypeScript also supports destructuring of tuples:

```typescript
let myTuple: [string, number] = ["hello", 42];
let [myString, myNumber] = myTuple;
```

In this example, we use destructuring to assign the elements of the tuple to variables `myString` and `myNumber`. This is equivalent to the previous example.

## 3. Modifying tuple elements

Tuples are immutable, which means you cannot modify their elements. If you try to do so, TypeScript will give you an error:

```typescript
let myTuple: [string, number] = ["hello", 42];
myTuple[0] = "world"; // Error: Tuple type '[string, number]' is immutable.
```

This error occurs because tuples are designed to represent fixed-length arrays with typed elements. If you need to modify the elements of a collection, you should use an array instead.

## 4. Combining tuples

You can combine tuples using the spread operator:

```typescript
let myTuple1: [string, number] = ["hello", 42];
let myTuple2: [boolean, string] = [true, "world"];
let myCombinedTuple: [string, number, boolean, string] = [...myTuple1, ...myTuple2];
```

In this example, we use the spread operator to combine `myTuple1` and `myTuple2` into a new tuple `myCombinedTuple`. The resulting tuple has four elements: a string, a number, a boolean, and a string.

## 5. Destructuring tuples

You can also use destructuring to extract parts of a tuple:

```typescript
let myTuple: [string, number, boolean] = ["hello", 42, true];
let [myString, , myBoolean] = myTuple;
```

In this example, we use destructuring to extract the first and third elements of the tuple, and ignore the second element.

## 6. Additional information

- Tuples are useful when you need to represent a collection of values with a specific order and type.
- Tuples are immutable, which means you cannot modify their elements.
- If you need to modify the elements of a collection, you should use an array instead.

## Further reading

- [TypeScript documentation on tuples](https://www.typescriptlang.org/docs/handbook/2/objects.html#tuple-types)
- [MDN web docs on tuples in JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object#tuple)