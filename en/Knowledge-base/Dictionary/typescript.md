---
title: TypeScript
description: 
published: true
date: 2023-02-01T00:57:39.691Z
tags: 
editor: markdown
dateCreated: 2023-02-01T00:57:35.963Z
---

- [TypeScript***Korean** version of this document is available*](/ko/Knowledge-base/Dictionary/typescript)
{.links-list}
- [TypeScript***Japanese** version of this document is available*](/ja/Knowledge-base/Dictionary/typescript)
{.links-list}
- [TypeScript***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Dictionary/typescript)
{.links-list}


# Overview
TypeScript is an open-source programming language developed and maintained by Microsoft. It is a superset of JavaScript, meaning that any valid JavaScript code is also valid TypeScript code. TypeScript adds optional static typing and class-based object-oriented programming to the language. It is designed for the development of large applications and transcompiles to JavaScript.

# History
TypeScript was first released in October 2012. It was developed by Microsoft to provide a typed superset of JavaScript that would be more suitable for large-scale applications. TypeScript has since become one of the most popular programming languages and is used by many large companies, including Microsoft, Google, and Facebook.

# Description
TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. It adds optional static typing and class-based object-oriented programming to the language. It is designed for the development of large applications and transcompiles to JavaScript. The TypeScript compiler is itself written in TypeScript and compiled to JavaScript.

# Features
TypeScript has many features that make it an attractive language for developing large applications. It has optional static typing, which allows developers to catch errors at compile time rather than at runtime. It also has classes, interfaces, and modules, which allow developers to structure their code in a more organized way. TypeScript also has support for generics, which allow developers to write code that can work with multiple types of data.

# Example
Below is an example of a simple TypeScript program that prints "Hello World!" to the console:

```typescript
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
  greet() {
    return "Hello, " + this.greeting;
  }
}

let greeter = new Greeter("world");

console.log(greeter.greet());
```

# Pros and Cons
TypeScript has many advantages over plain JavaScript. It has optional static typing, which allows developers to catch errors at compile time rather than at runtime. It also has classes, interfaces, and modules, which allow developers to structure their code in a more organized way. TypeScript also has support for generics, which allow developers to write code that can work with multiple types of data.

However, TypeScript also has some disadvantages. It is more complex than plain JavaScript, so it can be difficult to learn. It also requires a build process, which can be time-consuming. Finally, it is not as widely used as plain JavaScript, so there may be fewer resources available for learning and debugging.

# Related Technology
TypeScript is related to JavaScript, as it is a typed superset of the language. It is also related to other typed languages, such as C# and Java, as it has similar features, such as classes and interfaces.

# Digression
TypeScript is an open-source programming language developed and maintained by Microsoft. It is a typed superset of JavaScript, meaning that any valid JavaScript code is also valid TypeScript code. TypeScript adds optional static typing and class-based object-oriented programming to the language. It is designed for the development of large applications and transcompiles to JavaScript.