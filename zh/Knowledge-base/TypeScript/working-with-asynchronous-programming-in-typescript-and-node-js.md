---
title: 在 TypeScript 和 Node.js 中使用异步编程
description: 
published: true
date: 2023-02-16T13:19:33.899Z
tags: 
editor: markdown
dateCreated: 2023-02-16T13:19:23.151Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Working with Asynchronous Programming in TypeScript and Node.js***English** document is available*](/en/Knowledge-base/TypeScript/working-with-asynchronous-programming-in-typescript-and-node-js)
{.links-list}


# 在 TypeScript 和 Node.js 中使用异步编程

异步编程是一种流行的编程范例，它通过避免阻塞调用来实现高效的代码执行。在本文中，我们将了解如何在 TypeScript 和 Node.js 中使用异步编程。

## 什么是异步编程？

异步编程是一种编程范例，它通过避免阻塞调用来实现高效的代码执行。阻塞调用是在继续执行之前等待响应的调用，这可能会导致性能问题。

通过异步编程，程序可以在等待阻塞调用的响应时继续执行其他代码。这允许更有效的代码执行，因为程序不会无所事事地等待响应。

## TypeScript 中的异步编程

TypeScript 是 JavaScript 的类型化超集，可编译为干净、简单的 JavaScript 代码。它提供类、模块和接口来帮助您构建健壮的组件。

TypeScript 专为开发大型应用程序和转译为 JavaScript 而设计。异步编程是 TypeScript 中流行的编程范例，因为它通过避免阻塞调用来实现高效的代码执行。

在 TypeScript 中使用异步编程有两种方式：Promises 和 async/await。

### 承诺

Promises 是一种在 TypeScript 中使用异步代码的方式。 promise 表示尚未完成但预计在未来完成的操作。

Promises 用于处理 TypeScript 中的异步操作。承诺可以处于以下三种状态之一：

- **Pending**：操作尚未完成。
- **已完成**：操作已成功完成。
- **拒绝**：操作失败。

可以使用“Promise”构造函数创建一个 promise：

```typescript
const promise = new Promise((resolve, reject) => {
  // do something async
});
```

`Promise` 构造函数采用带有两个参数的回调函数：`resolve` 和 `reject`。当异步操作成功完成时，将调用“resolve”函数。异步操作失败时调用 `reject` 函数。

创建 promise 后，您可以使用 `then()` 方法注册一个回调函数，以便在 promise 实现时调用：

```typescript
promise.then((result) => {
  // do something with the result
});
```

您还可以使用 `catch()` 方法注册一个回调函数，以便在 promise 被拒绝时调用：

```typescript
promise.catch((error) => {
  // do something with the error
});
```

下面是使用承诺从 URL 加载图像的示例：

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

在此示例中，我们创建了一个“Promise”，当图像加载时使用图像 URL 进行解析，或者如果图像加载失败则拒绝错误。

### 异步/等待

Async/await 是一种在 TypeScript 中处理异步代码的方法。它允许您编写看起来和感觉起来都像同步代码的异步代码。

Async/await 建立在 promises 之上，并使用 async 和 await 关键字。

`async` 关键字用于创建异步函数。异步函数是返回承诺的函数：

```typescript
async function loadImage(url: string): Promise<string> {
  // do something async
}
```

`await` 关键字用于等待承诺得到解决。它只能在 `async` 函数中使用：

```typescript
async function loadImage(url: string): Promise<string> {
  const image = await loadImage(url);
  // do something with the image
}
```

在这个例子中，我们使用 `async` 关键字来创建一个异步函数。我们使用 `await` 关键字来等待 `loadImage` 函数被解析。

Async/await 是在 TypeScript 中使用异步代码的一种流行方式，因为它允许您编写看起来和感觉上都像同步代码的异步代码。

## Node.js 中的异步编程

Node.js 是一个基于 Chrome 的 V8 JavaScript 引擎构建的 JavaScript 运行时。它使用事件驱动、非阻塞 I/O 模型，使其轻量级且高效。

Node.js 专为构建可扩展的网络应用程序而设计。异步编程是 Node.js 中流行的编程范例，因为它通过避免阻塞调用来实现高效的代码执行。

在 Node.js 中使用异步编程有两种方式：回调和承诺。

### 回调

回调是在 Node.js 中处理异步代码的一种方式。回调是在异步操作完成时调用的函数。

当启动异步操作时，会提供一个回调函数。回调函数在异步操作完成时被调用。

回调函数通常用于 Node.js 中的异步操作，例如文件 I/O。

以下是使用回调函数读取文件的示例：

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

在这个例子中，我们使用 fs.readFile 函数来读取文件。 `fs.readFile` 函数接受一个文件路径和一个回调函数。使用 `err` 和 `data` 参数调用回调函数。如果 err 参数不为 null，则发生错误。否则，`data` 参数包含文件中的数据。

### 承诺

Promises 是一种在 Node.js 中使用异步代码的方式。 promise 表示尚未完成但预计在未来完成的操作。

Promises 用于处理 Node.js 中的异步操作。承诺可以处于以下三种状态之一：

- **Pending**：操作尚未完成。
- **已完成**：操作已成功完成。
- **拒绝**：操作失败。

可以使用“Promise”构造函数创建一个 promise：

```javascript
const promise = new Promise((resolve, reject) => {
  // do something async
});
```

`Promise` 构造函数采用带有两个参数的回调函数：`resolve` 和 `reject`。当异步操作成功完成时，将调用“resolve”函数。异步操作失败时调用 `reject` 函数。

创建 promise 后，您可以使用 `then()` 方法注册一个回调函数，以便在 promise 实现时调用：

```javascript
promise.then((result) => {
  // do something with the result
});
```

您还可以使用 `catch()` 方法注册一个回调函数，以便在 promise 被拒绝时调用：

```javascript
promise.catch((error) => {
  // do something with the error
});
```

下面是使用承诺从 URL 加载图像的示例：

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

在此示例中，我们创建了一个“Promise”，当图像加载时使用图像 URL 进行解析，或者如果图像加载失败则拒绝错误。

## Node.js 中的异步编程

Node.js 是一个基于 Chrome 的 V8 JavaScript 引擎构建的 JavaScript 运行时。它使用事件驱动、非阻塞 I/O 模型，使其轻量级且高效。

Node.js 专为构建可扩展的网络应用程序而设计。异步编程是 Node.js 中流行的编程范例，因为它通过避免阻塞调用来实现高效的代码执行。

在 Node.js 中使用异步编程有两种方式：回调和承诺。

### 回调

回调是在 Node.js 中处理异步代码的一种方式。回调是在异步操作完成时调用的函数。

当启动异步操作时，会提供一个回调函数。回调函数在异步操作完成时被调用。

回调函数通常用于 Node.js 中的异步操作，例如文件 I/O。

以下是使用回调函数读取文件的示例：

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

在这个例子中，我们使用 fs.readFile 函数来读取文件。 `fs.readFile` 函数接受一个文件路径和一个回调函数。使用 `err` 和 `data` 参数调用回调函数。如果 err 参数不为 null，则发生错误。否则，`data` 参数包含文件中的数据。

### 承诺

Promises 是一种在 Node.js 中使用异步代码的方式。 promise 表示尚未完成但预计在未来完成的操作。

Promises 用于处理 Node.js 中的异步操作。承诺可以处于以下三种状态之一：

- **Pending**：操作尚未完成。
- **已完成**：操作已成功完成。
- **拒绝**：操作失败。

可以使用“Promise”构造函数创建一个 promise：

```javascript
const promise = new Promise((resolve, reject) => {
  // do something async
});
```

`Promise` 构造函数采用带有两个参数的回调函数：`resolve` 和 `reject`。当异步操作成功完成时，将调用“resolve”函数。异步操作失败时调用 `reject` 函数。

创建 promise 后，您可以使用 `then()` 方法注册一个回调函数，以便在 promise 实现时调用：

```javascript
promise.then((result) => {
  // do something with the result
});
```

您还可以使用 `catch()` 方法注册一个回调函数，以便在 promise 被拒绝时调用：

```javascript
promise.catch((error) => {
  // do something with the error
});
```

下面是使用承诺从 URL 加载图像的示例：

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

在此示例中，我们创建了一个“Promise”，当图像加载时使用图像 URL 进行解析，或者如果图像加载失败则拒绝错误。

## 外部资源

- [异步函数 - TypeScript](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html# async-functions)
- [Node.js 中的回调函数](https://nodejs.org/en/knowledge/javascript-conventions/callbacks/)
- [在 Node.js 中使用 Promises](https://nodejs.org/en/knowledge/javascript-conventions/using-promises-in-nodejs/)