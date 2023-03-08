---
title: Working with Asynchronous Programming in TypeScript and Node.js
description: 
published: true
date: 2023-02-16T13:19:25.307Z
tags: 
editor: markdown
dateCreated: 2023-02-16T13:19:23.160Z
---

- [Trabajar con programación asíncrona en TypeScript y Node.js***Spanish** document is available*](/es/Knowledge-base/TypeScript/working-with-asynchronous-programming-in-typescript-and-node-js)
{.links-list}
- [在 TypeScript 和 Node.js 中使用异步编程***Chinese Simplified** document is available*](/zh/Knowledge-base/TypeScript/working-with-asynchronous-programming-in-typescript-and-node-js)
{.links-list}
- [TypeScript 및 Node.js에서 비동기 프로그래밍 작업***Korean** document is available*](/ko/Knowledge-base/TypeScript/working-with-asynchronous-programming-in-typescript-and-node-js)
{.links-list}


# Working with Asynchronous Programming in TypeScript and Node.js

Asynchronous programming is a popular programming paradigm that allows for efficient code execution by avoiding blocking calls. In this article, we'll take a look at how to work with asynchronous programming in TypeScript and Node.js.

## What is Asynchronous Programming?

Asynchronous programming is a programming paradigm that allows for efficient code execution by avoiding blocking calls. Blocking calls are calls that wait for a response before continuing execution, which can cause performance issues.

With asynchronous programming, a program can continue executing other code while waiting for a response from a blocking call. This allows for more efficient code execution, as the program is not waiting idly for a response.

## Asynchronous Programming in TypeScript

TypeScript is a typed superset of JavaScript that compiles to clean, simple JavaScript code. It offers classes, modules, and interfaces to help you build robust components.

TypeScript is designed for development of large applications and transcompiles to JavaScript. Asynchronous programming is a popular programming paradigm in TypeScript, as it allows for efficient code execution by avoiding blocking calls.

There are two ways to work with asynchronous programming in TypeScript: Promises and async/await.

### Promises

Promises are a way to work with asynchronous code in TypeScript. A promise represents an operation that hasn't completed yet, but is expected to in the future.

Promises are used to handle asynchronous operations in TypeScript. A promise can be in one of three states:

- **Pending**: The operation has not yet completed.
- **Fulfilled**: The operation has completed successfully.
- **Rejected**: The operation has failed.

A promise can be created using the `Promise` constructor:

```typescript
const promise = new Promise((resolve, reject) => {
  // do something async
});
```

The `Promise` constructor takes a callback function with two parameters: `resolve` and `reject`. The `resolve` function is called when the asynchronous operation completes successfully. The `reject` function is called when the asynchronous operation fails.

Once a promise is created, you can use the `then()` method to register a callback function to be called when the promise is fulfilled:

```typescript
promise.then((result) => {
  // do something with the result
});
```

You can also use the `catch()` method to register a callback function to be called when the promise is rejected:

```typescript
promise.catch((error) => {
  // do something with the error
});
```

Here's an example of using a promise to load a image from a URL:

```typescript
const loadImage = (url: string): Promise<string> => {
  return new Promise((resolve, reject) => {
    const image = new Image();

    image.onload = () => resolve(url);
    image.onerror = () => reject(new Error(`Failed to load image from URL: ${url}`));

    image.src = url;
  });
};
```

In this example, we create a `Promise` that resolves with the image URL when the image has loaded, or rejects with an error if the image fails to load.

### Async/Await

Async/await is a way to work with asynchronous code in TypeScript. It allows you to write asynchronous code that looks and feels like synchronous code.

Async/await is built on top of promises and uses `async` and `await` keywords.

The `async` keyword is used to create an asynchronous function. An asynchronous function is a function that returns a promise:

```typescript
async function loadImage(url: string): Promise<string> {
  // do something async
}
```

The `await` keyword is used to wait for a promise to be resolved. It can only be used inside an `async` function:

```typescript
async function loadImage(url: string): Promise<string> {
  const image = await loadImage(url);
  // do something with the image
}
```

In this example, we use the `async` keyword to create an asynchronous function. We use the `await` keyword to wait for the `loadImage` function to be resolved.

Async/await is a popular way to work with asynchronous code in TypeScript, as it allows you to write asynchronous code that looks and feels like synchronous code.

## Asynchronous Programming in Node.js

Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. It uses an event-driven, non-blocking I/O model that makes it lightweight and efficient.

Node.js is designed for building scalable network applications. Asynchronous programming is a popular programming paradigm in Node.js, as it allows for efficient code execution by avoiding blocking calls.

There are two ways to work with asynchronous programming in Node.js: callbacks and promises.

### Callbacks

Callbacks are a way to work with asynchronous code in Node.js. A callback is a function that is called when an asynchronous operation completes.

When an asynchronous operation is started, a callback function is provided. The callback function is called when the asynchronous operation completes.

Callback functions are commonly used in Node.js for asynchronous operations such as file I/O.

Here's an example of using a callback function to read a file:

```javascript
const fs = require('fs');

fs.readFile('/path/to/file', (err, data) => {
  if (err) {
    // do something with the error
  } else {
    // do something with the data
  }
});
```

In this example, we use the `fs.readFile` function to read a file. The `fs.readFile` function takes a path to a file and a callback function. The callback function is called with an `err` and `data` parameters. If the `err` parameter is not `null`, then an error occurred. Otherwise, the `data` parameter contains the data from the file.

### Promises

Promises are a way to work with asynchronous code in Node.js. A promise represents an operation that hasn't completed yet, but is expected to in the future.

Promises are used to handle asynchronous operations in Node.js. A promise can be in one of three states:

- **Pending**: The operation has not yet completed.
- **Fulfilled**: The operation has completed successfully.
- **Rejected**: The operation has failed.

A promise can be created using the `Promise` constructor:

```javascript
const promise = new Promise((resolve, reject) => {
  // do something async
});
```

The `Promise` constructor takes a callback function with two parameters: `resolve` and `reject`. The `resolve` function is called when the asynchronous operation completes successfully. The `reject` function is called when the asynchronous operation fails.

Once a promise is created, you can use the `then()` method to register a callback function to be called when the promise is fulfilled:

```javascript
promise.then((result) => {
  // do something with the result
});
```

You can also use the `catch()` method to register a callback function to be called when the promise is rejected:

```javascript
promise.catch((error) => {
  // do something with the error
});
```

Here's an example of using a promise to load an image from a URL:

```javascript
const loadImage = (url: string): Promise<string> => {
  return new Promise((resolve, reject) => {
    const image = new Image();

    image.onload = () => resolve(url);
    image.onerror = () => reject(new Error(`Failed to load image from URL: ${url}`));

    image.src = url;
  });
};
```

In this example, we create a `Promise` that resolves with the image URL when the image has loaded, or rejects with an error if the image fails to load.

## Asynchronous Programming in Node.js

Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. It uses an event-driven, non-blocking I/O model that makes it lightweight and efficient.

Node.js is designed for building scalable network applications. Asynchronous programming is a popular programming paradigm in Node.js, as it allows for efficient code execution by avoiding blocking calls.

There are two ways to work with asynchronous programming in Node.js: callbacks and promises.

### Callbacks

Callbacks are a way to work with asynchronous code in Node.js. A callback is a function that is called when an asynchronous operation completes.

When an asynchronous operation is started, a callback function is provided. The callback function is called when the asynchronous operation completes.

Callback functions are commonly used in Node.js for asynchronous operations such as file I/O.

Here's an example of using a callback function to read a file:

```javascript
const fs = require('fs');

fs.readFile('/path/to/file', (err, data) => {
  if (err) {
    // do something with the error
  } else {
    // do something with the data
  }
});
```

In this example, we use the `fs.readFile` function to read a file. The `fs.readFile` function takes a path to a file and a callback function. The callback function is called with an `err` and `data` parameters. If the `err` parameter is not `null`, then an error occurred. Otherwise, the `data` parameter contains the data from the file.

### Promises

Promises are a way to work with asynchronous code in Node.js. A promise represents an operation that hasn't completed yet, but is expected to in the future.

Promises are used to handle asynchronous operations in Node.js. A promise can be in one of three states:

- **Pending**: The operation has not yet completed.
- **Fulfilled**: The operation has completed successfully.
- **Rejected**: The operation has failed.

A promise can be created using the `Promise` constructor:

```javascript
const promise = new Promise((resolve, reject) => {
  // do something async
});
```

The `Promise` constructor takes a callback function with two parameters: `resolve` and `reject`. The `resolve` function is called when the asynchronous operation completes successfully. The `reject` function is called when the asynchronous operation fails.

Once a promise is created, you can use the `then()` method to register a callback function to be called when the promise is fulfilled:

```javascript
promise.then((result) => {
  // do something with the result
});
```

You can also use the `catch()` method to register a callback function to be called when the promise is rejected:

```javascript
promise.catch((error) => {
  // do something with the error
});
```

Here's an example of using a promise to load an image from a URL:

```javascript
const loadImage = (url: string): Promise<string> => {
  return new Promise((resolve, reject) => {
    const image = new Image();

    image.onload = () => resolve(url);
    image.onerror = () => reject(new Error(`Failed to load image from URL: ${url}`));

    image.src = url;
  });
};
```

In this example, we create a `Promise` that resolves with the image URL when the image has loaded, or rejects with an error if the image fails to load.

## External Resources

- [Async Functions - TypeScript](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html#async-functions)
- [Callback functions in Node.js](https://nodejs.org/en/knowledge/javascript-conventions/callbacks/)
- [Using Promises in Node.js](https://nodejs.org/en/knowledge/javascript-conventions/using-promises-in-nodejs/)