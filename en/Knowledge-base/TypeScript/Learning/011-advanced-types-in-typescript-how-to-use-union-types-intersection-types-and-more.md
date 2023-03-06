---
title: 011: Advanced Types in TypeScript: How to Use Union Types, Intersection Types, and More
description: 
published: true
date: 2023-03-06T14:33:07.655Z
tags: 
editor: markdown
dateCreated: 2023-03-06T14:33:07.655Z
---

- [011: TypeScript의 고급 유형: 공용체 유형, 교차 유형 등을 사용하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/011-advanced-types-in-typescript-how-to-use-union-types-intersection-types-and-more)
{.links-list}



Advanced Types in TypeScript: How to Use Union Types, Intersection Types, and More

TypeScript is a superset of JavaScript that provides static typing and other features to make it easier to write and maintain large-scale applications. One of the most powerful features of TypeScript is its support for advanced types, including union types, intersection types, and more. In this post, we'll explore these advanced types and how to use them effectively in your TypeScript code.

## Union Types

In TypeScript, a union type allows a variable to have more than one type. For example, you might have a variable that can be either a string or a number:

```typescript
let myVar: string | number;
```

This means that `myVar` can be assigned a value of either type `string` or type `number`. You can use union types to create more flexible and expressive types that can handle a wider range of values.

### Using Union Types for Function Parameters

One common use case for union types is to create flexible function parameters. For example, you might have a function that can accept either a string or a number:

```typescript
function myFunc(myParam: string | number) {
  // ...
}
```

This allows you to call `myFunc` with either a string or a number argument:

```typescript
myFunc("hello");
myFunc(42);
```

### Using Union Types for Return Types

You can also use union types for function return types. For example, you might have a function that returns either a string or a number:

```typescript
function myOtherFunc(): string | number {
  // ...
}
```

This means that the return value of `myOtherFunc` can be either a string or a number. You can use this to create more flexible functions that can return different types of values depending on the input.

### Additional Information

When using union types, it's important to be careful about type checking. You should always check the type of a variable before using it, to avoid runtime errors. For example:

```typescript
if (typeof myVar === "string") {
  // ...
} else if (typeof myVar === "number") {
  // ...
}
```

## Intersection Types

In TypeScript, an intersection type allows a variable to have multiple types at once. For example, you might have a variable that is both a string and an object:

```typescript
let myVar: string & object;
```

This means that `myVar` must be both a string and an object at the same time. You can use intersection types to create more precise and specific types that can handle complex data structures.

### Using Intersection Types for Function Parameters

One common use case for intersection types is to create more specific function parameters. For example, you might have a function that accepts an object with both a `name` property (a string) and an `age` property (a number):

```typescript
function myFunc(myParam: { name: string } & { age: number }) {
  // ...
}
```

This means that `myParam` must be an object that has both a `name` property (with a value of type `string`) and an `age` property (with a value of type `number`). You can use this to create more precise function parameters that only accept specific types of input.

### Using Intersection Types for Object Types

You can also use intersection types to create more specific object types. For example, you might have an object type that represents a person with a name and an age:

```typescript
type Person = {
  name: string;
  age: number;
};
```

You could then create a more specific object type that represents a student, with additional properties like `grade` and `school`:

```typescript
type Student = Person & {
  grade: number;
  school: string;
};
```

This means that a `Student` object must have all the properties of a `Person` object (a `name` property with a value of type `string` and an `age` property with a value of type `number`), as well as additional properties `grade` (a number) and `school` (a string).

### Additional Information

When using intersection types, it's important to be careful about type compatibility. You should only use intersection types when the types you're combining are compatible with each other. For example, you can't create an intersection type between a `string` and a `number`, because they are not compatible types.

## Type Guards

When using union types, it's often necessary to check the type of a variable before using it. TypeScript provides a feature called type guards that makes this easier.

A type guard is a function that takes a variable and returns a boolean value indicating whether the variable is of a certain type. For example, you might have a type guard that checks whether a variable is a string:

```typescript
function isString(myVar: any): myVar is string {
  return typeof myVar === "string";
}
```

This type guard takes a variable `myVar` of type `any` (which can be any type) and returns a boolean value indicating whether `myVar` is a string. The `myVar is string` syntax is a type predicate that tells TypeScript that if the function returns `true`, the variable is of type `string`.

You can then use this type guard to check the type of a variable before using it:

```typescript
if (isString(myVar)) {
  // myVar is now of type `string`
  console.log(myVar.toUpperCase());
}
```

### Additional Information

Type guards can be used with any type, not just union types. They are a powerful tool for ensuring type safety in your TypeScript code.

## Conditional Types

In TypeScript, a conditional type allows you to define a type that depends on a condition. For example, you might have a type that represents a person if they are over 18 years old, and a different type if they are under 18:

```typescript
type Person<T> = T extends { age: number; } & { age: infer U; } ? (
  U extends 18 ? { name: string; age: U; } : { name: string; age: U; id: string; }
) : never;
```

This type definition uses the `extends` keyword to define a condition: if a type `T` has an `age` property of type `number`, the conditional type returns a different type depending on the value of `U` (the inferred type of `age`). If `U` is 18, the type is `{ name: string; age: U; }`, and if `U` is not 18, the type is `{ name: string; age: U; id: string; }`.

### Additional Information

Conditional types can be complex and difficult to read. They are a powerful tool for creating types that depend on conditions, but should be used sparingly and with caution.

## Conclusion

Advanced types like union types, intersection types, and conditional types can make your TypeScript code more flexible and expressive. By using these types effectively, you can create more precise and specific types that can handle complex data structures and ensure type safety in your code. Happy coding!

## External Resources

- [TypeScript Handbook: Advanced Types](https://www.typescriptlang.org/docs/handbook/advanced-types.html)
- [TypeScript Deep Dive: Union Types](https://basarat.gitbook.io/typescript/type-system/union-types)
- [TypeScript Deep Dive: Intersection Types](https://basarat.gitbook.io/typescript/type-system/intersection-types)
- [TypeScript Deep Dive: Type Guards](https://basarat.gitbook.io/typescript/type-system/typeguard)
- [TypeScript Deep Dive: Conditional Types](https://basarat.gitbook.io/typescript/type-system/conditional-types)