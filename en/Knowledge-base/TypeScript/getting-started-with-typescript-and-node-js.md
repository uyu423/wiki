---
title: Getting Started with TypeScript and Node.js
description: 
published: true
date: 2023-02-01T10:57:25.699Z
tags: 
editor: markdown
dateCreated: 2023-02-01T10:57:22.324Z
---

- [TypeScript 및 Node.js 시작하기***Korean** version of this document is available*](/ko/Knowledge-base/TypeScript/getting-started-with-typescript-and-node-js)
{.links-list}
- [开始使用 TypeScript 和 Node.js***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/TypeScript/getting-started-with-typescript-and-node-js)
{.links-list}



# Getting Started with TypeScript and Node.js

TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. Any browser. Any host. Any OS. Open source.

Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine.

## Why Use TypeScript?

TypeScript is JavaScript with an important difference. TypeScript is typed.

Types allow TypeScript to offer key benefits like code completion, refactoring, and type checking.

Types also make it easier to document code. And, when used with an IDE like Visual Studio Code, types can provide a richer development experience by offering code completion and inline documentation.

## Why Use Node.js?

Node.js is a platform for building fast and scalable network applications.

Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient.

Node.js' package ecosystem, npm, is the largest ecosystem of open source libraries in the world.

## Getting Started

To get started with TypeScript and Node.js, you will need to install Node.js.

Once Node.js is installed, you can create a TypeScript file and compile it to JavaScript using the `tsc` command line tool.

```
// greeter.ts
function greeter(person: string) {
    return "Hello, " + person;
}

let user = "Jane User";

document.body.textContent = greeter(user);
```

```
tsc greeter.ts
```

This will create a file called `greeter.js` that contains the compiled JavaScript.

To run the compiled JavaScript, you will need to use a Node.js runtime.

```
node greeter.js
```

You can also use TypeScript with existing JavaScript code.

```
// greeter.ts
function greeter(person: string) {
    return "Hello, " + person;
}

let user = "Jane User";

document.body.textContent = greeter(user);
```

```
// greeter.js
function greeter(person) {
    return "Hello, " + person;
}

let user = "Jane User";

document.body.textContent = greeter(user);
```

## TypeScript and Node.js Resources

- [TypeScript](https://www.typescriptlang.org/)
- [Node.js](https://nodejs.org/)
- [Visual Studio Code](https://code.visualstudio.com/)