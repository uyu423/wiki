---
title: 开始使用 TypeScript 和 Node.js
description: 
published: true
date: 2023-02-01T10:57:23.771Z
tags: 
editor: markdown
dateCreated: 2023-02-01T10:57:22.329Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Getting Started with TypeScript and Node.js***English** version of this document is available*](/en/Knowledge-base/TypeScript/getting-started-with-typescript-and-node-js)
{.links-list}



# 开始使用 TypeScript 和 Node.js

TypeScript 是 JavaScript 的类型化超集，可编译为纯 JavaScript。任何浏览器。任何主机。任何操作系统。开源。

Node.js 是一个基于 Chrome 的 V8 JavaScript 引擎构建的 JavaScript 运行时。

## 为什么使用 TypeScript？

TypeScript 是 JavaScript，但有一个重要的区别。键入 TypeScript。

类型允许 TypeScript 提供代码完成、重构和类型检查等关键优势。

类型还可以更轻松地记录代码。而且，当与 Visual Studio Code 等 IDE 一起使用时，类型可以通过提供代码完成和内联文档来提供更丰富的开发体验。

## 为什么使用 Node.js？

Node.js 是一个用于构建快速且可扩展的网络应用程序的平台。

Node.js 使用事件驱动、非阻塞 I/O 模型，使其轻量级且高效。

Node.js 的包生态系统 npm 是世界上最大的开源库生态系统。

## 入门

要开始使用 TypeScript 和 Node.js，您需要安装 Node.js。

安装 Node.js 后，您可以创建一个 TypeScript 文件并使用 `tsc` 命令行工具将其编译为 JavaScript。

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

这将创建一个名为“greeter.js”的文件，其中包含已编译的 JavaScript。

要运行编译后的 JavaScript，您需要使用 Node.js 运行时。

```
node greeter.js
```

您还可以将 TypeScript 与现有的 JavaScript 代码结合使用。

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

## TypeScript 和 Node.js 资源

- [打字稿](https://www.typescriptlang.org/)
- [Node.js](https://nodejs.org/)
- [Visual Studio 代码](https://code.visualstudio.com/)