---
title: 023: Mixing JavaScript and TypeScript: How to Use TypeScript with Existing JavaScript Code
description: 
published: true
date: 2023-03-07T18:32:46.682Z
tags: 
editor: markdown
dateCreated: 2023-03-07T18:32:38.394Z
---

- [023: JavaScript와 TypeScript 혼합: TypeScript를 기존 JavaScript 코드와 함께 사용하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/023-mixing-javascript-and-typescript-how-to-use-typescript-with-existing-javascript-code)
{.links-list}



Mixing JavaScript and TypeScript: How to Use TypeScript with Existing JavaScript Code

TypeScript is a superset of JavaScript that adds static typing, classes, interfaces, and other features to JavaScript. It is a popular choice for developing large-scale applications, as it offers better code maintainability and scalability. However, many existing JavaScript projects may not have been developed with TypeScript in mind. In this post, we will explore how to use TypeScript with existing JavaScript code.

## Why Use TypeScript with Existing JavaScript Code?

There are several reasons why you might want to use TypeScript with existing JavaScript code:

- **Type Safety**: TypeScript offers static typing, which can help catch errors at compile time instead of runtime. This can improve code quality and reduce the likelihood of bugs.

- **Improved Code Maintainability**: TypeScript provides tools for organizing and structuring code, making it easier to understand and maintain.

- **Scalability**: TypeScript supports object-oriented programming principles, making it easier to build large-scale applications.

## Setting up a TypeScript Project

Before we can start using TypeScript with existing JavaScript code, we need to set up a TypeScript project. We can do this using the following steps:

1. Install TypeScript using npm:

```npm install -g typescript```

2. Create a new folder for our project:

```mkdir my-project```

3. Navigate to the project folder:

```cd my-project```

4. Initialize a new TypeScript project:

```tsc --init```

This will create a `tsconfig.json` file in our project folder, which we can use to configure our TypeScript project.

## Using TypeScript with Existing JavaScript Code

Once we have set up our TypeScript project, we can start using TypeScript with existing JavaScript code. There are several ways to do this:

### 1. Rename `.js` Files to `.ts`

One way to use TypeScript with existing JavaScript code is to simply rename our `.js` files to `.ts` files. This allows us to start using TypeScript features, such as static typing, in our existing code.

However, this approach has some limitations. For example, TypeScript will not be able to infer types for any external dependencies that we are using, so we will need to manually add type definitions for these dependencies.

### 2. Use Type Declarations

Another way to use TypeScript with existing JavaScript code is to use type declarations. Type declarations are files that describe the types of external JavaScript libraries and APIs.

We can install type declarations using npm:

```npm install @types/library-name```

For example, if we want to use type declarations for the jQuery library, we can install them using:

```npm install @types/jquery```

Once we have installed the type declarations, we can start using TypeScript with the external library.

### 3. Use JSDoc Annotations

JSDoc annotations are a way to add type information to JavaScript code. We can use JSDoc annotations to add type information to our existing JavaScript code, allowing us to start using TypeScript features.

For example, we can add JSDoc annotations to the following function to specify the types of the parameters and return value:

```javascript
/**
 * Adds two numbers together.
 * @param {number} x - The first number.
 * @param {number} y - The second number.
 * @returns {number} The sum of x and y.
 */
function add(x, y) {
  return x + y;
}
```

Once we have added JSDoc annotations to our code, we can start using TypeScript features, such as static typing.

## Conclusion

Using TypeScript with existing JavaScript code can help improve code quality, maintainability, and scalability. We can start using TypeScript with existing JavaScript code by renaming `.js` files to `.ts`, using type declarations, or adding JSDoc annotations. By following these steps, we can start taking advantage of TypeScript features in our existing JavaScript projects.

## Additional Information

- TypeScript Handbook: https://www.typescriptlang.org/docs/handbook/intro.html

## Warnings

- Renaming `.js` files to `.ts` files may cause some errors if the JavaScript code uses features that are not supported by TypeScript.

## Dangers

- Type declarations may not always be up-to-date or accurate, which can lead to errors in our code. It is important to check the quality of the type declarations before using them in our projects.

## Further Reading

- "JavaScript to TypeScript Conversion Guide": https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html
- "TypeScript vs. JavaScript: Should You Migrate Your Project?": https://www.altar.io/blog/typescript-vs-javascript-should-you-migrate-your-project