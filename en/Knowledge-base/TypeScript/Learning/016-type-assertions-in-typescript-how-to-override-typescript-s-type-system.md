---
title: 016: Type Assertions in TypeScript: How to Override TypeScript's Type System
description: 
published: true
date: 2023-03-02T11:32:16.860Z
tags: 
editor: markdown
dateCreated: 2023-03-02T11:32:15.426Z
---

- [016: TypeScript의 유형 어설션: TypeScript의 유형 시스템을 재정의하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/016-type-assertions-in-typescript-how-to-override-typescript-s-type-system)
{.links-list}


TypeScript is a superset of JavaScript that provides optional static typing and enables developers to write safer and more maintainable code. One of the key features of TypeScript is its type system, which helps catch errors at compile-time and improves code quality. However, there may be situations where you need to override TypeScript's type system to achieve a specific functionality, and this is where type assertions come in.

In this post, we will explore type assertions in TypeScript and learn how to use them to override TypeScript's type system. We will cover the following topics:

- What are type assertions?
- How to use type assertions in TypeScript
- Examples of using type assertions
- Additional information

## What are type assertions?

Type assertions in TypeScript are a way to tell the compiler that you know more about the type of a value than it does. It is a way to override the type system and tell TypeScript to treat a value as a different type, even if TypeScript's type checker does not agree.

Type assertions are not type casting. Type casting is a way to convert a value of one type to another type, while type assertions only tell TypeScript to treat a value as a different type without changing its value.

Type assertions are useful when you have a value that you know is of a specific type, but TypeScript does not. They are also useful when you want to use a value in a way that TypeScript does not allow because of its type.

## How to use type assertions in TypeScript

TypeScript provides two syntaxes for type assertions: the angle-bracket syntax and the as syntax.

### Angle-bracket syntax

The angle-bracket syntax is the original syntax for type assertions in TypeScript. It looks like this:

```typescript
let value: any = "hello world";
let length: number = (<string>value).length;
```

In this example, we declare a variable `value` of type `any` and assign it the value `"hello world"`. We then use the angle-bracket syntax to assert that `value` is a string and assign its length to the variable `length`.

### As syntax

The as syntax is a newer syntax for type assertions in TypeScript. It looks like this:

```typescript
let value: any = "hello world";
let length: number = (value as string).length;
```

In this example, we use the as syntax to assert that `value` is a string and assign its length to the variable `length`.

Both syntaxes are equivalent and can be used interchangeably. However, the as syntax is recommended by the TypeScript team because it is less likely to clash with JSX syntax.

## Examples of using type assertions

Let's look at some examples of using type assertions in TypeScript.

### Example 1: Asserting the type of a value

```typescript
let value: any = "hello world";
let length: number = (value as string).length;
```

In this example, we assert that `value` is a string and assign its length to the variable `length`.

### Example 2: Asserting the type of an object property

```typescript
interface Person {
    name: string;
    age: number;
}

let person: any = { name: "John", age: 30 };
let nameLength: number = (person as Person).name.length;
```

In this example, we declare an interface `Person` with two properties `name` and `age`. We then declare a variable `person` of type `any` and assign it an object with the same properties as `Person`. We use the as syntax to assert that `person` is of type `Person` and assign the length of its `name` property to the variable `nameLength`.

### Example 3: Asserting the type of a function return value

```typescript
function getLength(value: any): number {
    return (value as string).length;
}

let length: number = getLength("hello world");
```

In this example, we declare a function `getLength` that takes a value of type `any` and returns its length as a number. We use the as syntax to assert that the value is a string and return its length. We then call the function with the value `"hello world"` and assign its return value to the variable `length`.

## Additional information

Type assertions should be used with caution because they can lead to runtime errors if the asserted type is incorrect. It is always better to use TypeScript's type system whenever possible to catch errors at compile-time.

Type assertions should also be used sparingly because they can make code harder to read and maintain. If you find yourself using type assertions frequently, it may be a sign that your code needs to be refactored.

## Conclusion

Type assertions in TypeScript are a powerful tool that allows developers to override TypeScript's type system when needed. They can be used to solve specific problems but should be used with caution and sparingly. By using type assertions correctly, you can write safer and more maintainable code in TypeScript.

## Further reading

- [TypeScript Handbook: Type Assertions](https://www.typescriptlang.org/docs/handbook/basic-types.html#type-assertions)
- [TypeScript Deep Dive: Type Assertions](https://basarat.gitbook.io/typescript/type-system/typeassertion)