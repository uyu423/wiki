---
title: 037: Nullish Coalescing in TypeScript: How to Use the Nullish Coalescing Operator
description: 
published: true
date: 2023-03-10T10:32:35.911Z
tags: 
editor: markdown
dateCreated: 2023-03-10T10:32:35.911Z
---

- [037: TypeScript의 Nullish 병합: Nullish 병합 연산자 사용 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/037-nullish-coalescing-in-typescript-how-to-use-the-nullish-coalescing-operator)
{.links-list}



Nullish Coalescing in TypeScript: How to Use the Nullish Coalescing Operator

TypeScript is a powerful language that adds type annotations to JavaScript, making it more reliable and easier to maintain. One of the features introduced in TypeScript 3.7 is the nullish coalescing operator, which is a shorthand for checking whether a value is null or undefined before using a default value. In this post, we'll explore how to use the nullish coalescing operator in TypeScript, and how it can help you write more robust code.

## What is the Nullish Coalescing Operator?

The nullish coalescing operator (??) is a new operator in TypeScript that allows you to define a default value for a variable if it is null or undefined. Here's an example:

```typescript
const foo = null ?? 'default'; // foo === 'default'
const bar = undefined ?? 'default'; // bar === 'default'
const baz = 'value' ?? 'default'; // baz === 'value'
```

In this example, the nullish coalescing operator checks whether the value of the variable is null or undefined. If it is, it returns the default value 'default'. If the value of the variable is not null or undefined, it returns the value of the variable itself.

Note that the nullish coalescing operator only checks for null or undefined values, not falsy values like 0 or ''. If you want to check for falsy values as well, you can use the logical OR operator (||) instead.

## Why Use the Nullish Coalescing Operator?

The nullish coalescing operator is a handy shorthand for checking whether a value is null or undefined before using a default value. This can help you write more concise and readable code, especially when dealing with optional parameters or default values.

Consider the following example:

```typescript
function printMessage(message?: string) {
  console.log(message || 'Hello, world!');
}
```

In this example, the printMessage function takes an optional parameter message, which defaults to 'Hello, world!' if it is not provided. However, the logical OR operator (||) used here will also return the default value if message is falsy, which is not what we want. To fix this, we can use the nullish coalescing operator instead:

```typescript
function printMessage(message?: string) {
  console.log(message ?? 'Hello, world!');
}
```

Now, the printMessage function will only use the default value if message is null or undefined, which is the behavior we expect.

## Additional Information

- The nullish coalescing operator is not supported in all browsers yet. If you need to support older browsers, you may need to use a polyfill or transpile your code to an older version of JavaScript.

## Conclusion

The nullish coalescing operator is a useful addition to TypeScript that can help you write more concise and readable code. By using the nullish coalescing operator, you can define default values for variables and parameters without worrying about falsy values. If you're not already using the nullish coalescing operator in your TypeScript projects, give it a try and see how it can simplify your code.

## Further Reading

- [TypeScript Nullish Coalescing Operator](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html#nullish-coalescing)
- [MDN Web Docs: Nullish coalescing operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)