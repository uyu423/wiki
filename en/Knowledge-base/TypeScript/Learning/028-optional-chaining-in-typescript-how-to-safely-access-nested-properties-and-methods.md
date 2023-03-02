---
title: 028: Optional Chaining in TypeScript: How to Safely Access Nested Properties and Methods
description: 
published: true
date: 2023-03-02T22:32:12.439Z
tags: 
editor: markdown
dateCreated: 2023-03-02T22:32:12.439Z
---

- [028: TypeScript의 선택적 연결: 중첩된 속성 및 메서드에 안전하게 액세스하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/028-optional-chaining-in-typescript-how-to-safely-access-nested-properties-and-methods)
{.links-list}


## Introduction

In TypeScript, accessing nested properties and methods can be a bit tricky, especially when dealing with optional values. Fortunately, TypeScript provides a feature called optional chaining that simplifies this task. In this post, we will explore what optional chaining is, how it works, and how to use it in TypeScript.

## What is Optional Chaining?

Optional chaining is a feature introduced in TypeScript version 3.7 that allows developers to safely access nested properties and methods of an object, even if some of the intermediate values are null or undefined. 

Before the introduction of optional chaining, developers had to write lengthy and error-prone code to check if each intermediate property or method exists before accessing it. With optional chaining, developers can simply use the ? operator to indicate that a property or method may not exist and TypeScript will automatically handle the null or undefined checks.

## How Does Optional Chaining Work?

Optional chaining works by checking if each intermediate property or method in a chain of property accesses exists before accessing it. If any intermediate value is null or undefined, the entire expression evaluates to undefined.

Here's an example to illustrate how optional chaining works:

```typescript
interface Person {
  name: string;
  address?: {
    street: string;
    city: string;
  };
}

const person: Person = {
  name: "John Doe",
};

const city = person.address?.city;
console.log(city); // Output: undefined
```

In the above example, we have an interface `Person` with an optional `address` property that has two nested properties `street` and `city`. We then create an object `person` with only the `name` property set.

Next, we try to access the `city` property of the `address` object using optional chaining. Since the `address` property is not set, the expression `person.address?.city` evaluates to `undefined`.

## Using Optional Chaining in TypeScript

To use optional chaining in TypeScript, simply add the `?` operator after the property or method that may not exist. Here's an example:

```typescript
const street = person.address?.street;
console.log(street); // Output: undefined
```

In the above example, we try to access the `street` property of the `address` object using optional chaining. Since the `address` property is not set, the expression `person.address?.street` evaluates to `undefined`.

You can also use optional chaining with method calls. Here's an example:

```typescript
interface User {
  name: string;
  getAddress?(): string;
}

const user: User = {
  name: "Jane Doe",
};

const address = user.getAddress?.();
console.log(address); // Output: undefined
```

In the above example, we have an interface `User` with an optional method `getAddress` that returns a string. We then create an object `user` with only the `name` property set.

Next, we try to call the `getAddress` method using optional chaining. Since the `getAddress` method is not set, the expression `user.getAddress?.()` evaluates to `undefined`.

## Additional Information

- Optional chaining is supported in TypeScript version 3.7 or later.
- Optional chaining is also supported in JavaScript, but it may not work in older browsers.

## Conclusion

Optional chaining is a useful feature in TypeScript that simplifies accessing nested properties and methods, especially when dealing with optional values. By using optional chaining, developers can write cleaner and more concise code that is less prone to errors.

## Further Reading

- [TypeScript Documentation: Optional Chaining](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html#optional-chaining)
- [MDN Web Docs: Optional Chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)