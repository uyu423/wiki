---
title: 038: Global Declarations in TypeScript: How to Declare Global Variables and Functions
description: 
published: true
date: 2023-03-08T16:32:37.723Z
tags: 
editor: markdown
dateCreated: 2023-03-08T16:32:37.723Z
---

- [038: TypeScript의 전역 선언: 전역 변수 및 함수를 선언하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/038-global-declarations-in-typescript-how-to-declare-global-variables-and-functions)
{.links-list}



Global Declarations in TypeScript: How to Declare Global Variables and Functions

TypeScript is a superset of JavaScript that provides optional static typing, classes, and interfaces. It helps developers write more maintainable and scalable code. One of TypeScript's features is the ability to declare global variables and functions.

In this post, we'll look at how to declare global variables and functions in TypeScript and why you might want to do so.

## Global Declarations in TypeScript

When you declare a variable or function in TypeScript, it's scoped to the file or module in which it's declared. This means that other files or modules cannot access it unless it's exported.

However, there are situations where you may want to declare a variable or function that's accessible across your entire application. This is where global declarations come in.

A global declaration is a variable or function that's accessible across your entire application, regardless of the file or module in which it's declared. To declare a global variable or function in TypeScript, you use the `declare` keyword.

Here's an example of how to declare a global variable in TypeScript:

```typescript
declare var myGlobalVariable: string;
```

In this example, we're declaring a global variable called `myGlobalVariable` of type `string`. We're not providing a value for the variable, as it will be initialized elsewhere in our application.

Similarly, here's an example of how to declare a global function in TypeScript:

```typescript
declare function myGlobalFunction(): void;
```

In this example, we're declaring a global function called `myGlobalFunction` that takes no arguments and returns `void`.

## Using Global Declarations

Once you've declared a global variable or function, you can use it anywhere in your application. Here's an example of how to use the global variable we declared earlier:

```typescript
myGlobalVariable = "Hello, world!";
console.log(myGlobalVariable);
```

In this example, we're assigning the value `"Hello, world!"` to `myGlobalVariable` and then logging it to the console.

Here's an example of how to use the global function we declared earlier:

```typescript
myGlobalFunction();
```

In this example, we're calling `myGlobalFunction`.

## Why Use Global Declarations?

You might be wondering why you would want to use global declarations in TypeScript. After all, TypeScript encourages you to write modular code that's scoped to individual files or modules.

However, there are situations where global declarations can be useful. For example:

- You might be working with a legacy codebase that's not written in TypeScript, and you want to declare some global variables or functions that are used throughout the codebase.
- You might be working with a third-party library that expects certain global variables or functions to be defined.
- You might be working with a complex application that has many modules, and you want to declare some global variables or functions that are used across multiple modules.

In these situations, global declarations can help you write cleaner, more maintainable code.

## Additional Information

- When declaring global variables or functions, it's a good practice to prefix their names with something unique to avoid naming collisions with other global variables or functions.
- You can also declare global variables or functions using the `window` object in TypeScript. For example:

```typescript
declare global {
  interface Window {
    myGlobalVariable: string;
    myGlobalFunction: () => void;
  }
}
```

This syntax declares the `myGlobalVariable` and `myGlobalFunction` properties on the `window` object, making them accessible globally.

## Conclusion

In this post, we've looked at how to declare global variables and functions in TypeScript using the `declare` keyword. We've also discussed why you might want to use global declarations in your TypeScript applications.

By using global declarations, you can write cleaner, more maintainable code that's easier to work with across multiple files or modules.

## Further Reading

- [TypeScript Handbook: Declarations](https://www.typescriptlang.org/docs/handbook/declaration-files/introduction.html)
- [TypeScript Deep Dive: Global Declarations](https://basarat.gitbook.io/typescript/type-system/global-declarations)