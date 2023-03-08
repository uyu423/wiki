---
title: Node.js 中的流和管道：动手指南
description: 
published: true
date: 2023-02-01T20:36:28.576Z
tags: 
editor: markdown
dateCreated: 2023-02-01T20:36:26.895Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Streams and Piping in Node.js: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/streams-and-piping-in-node-js-a-hands-on-guide)
{.links-list}


# Node.js 中的流和管道：动手指南

如果您是 Node.js 开发人员，您很可能在代码中使用过流。流是 Node.js 的基本组成部分，用于执行各种任务，包括处理 HTTP 请求和响应、读取和写入文件等。

在本文中，我们将采用实践方法来了解 Node.js 中的流和管道。我们将涵盖以下主题：

- 什么是流？
- 流类型
- 创建流
- 管道流
-错误处理

## 什么是流？

流是处理可以读取或写入的数据的抽象。流是 Node.js 的关键部分，用于执行各种任务，包括处理 HTTP 请求和响应、读取和写入文件等。

Streams 可以被认为是一个数据管道，其中数据通过流从源流向目的地。流可用于从源读取数据、将数据写入目标或两者兼而有之。

## 流类型

有四种类型的流：可读、可写、双工和转换。

- 可读流用于从源读取数据。
- 可写流用于将数据写入目的地。
- 双工流用于读取和写入数据。
- 转换流用于在数据流经流时转换数据。

## 创建流

有几种不同的方法可以在 Node.js 中创建流。

一种方法是使用内置的流模块：

```javascript
const stream = require('stream');

const readableStream = new stream.Readable();
const writableStream = new stream.Writable();
const duplexStream = new stream.Duplex();
const transformStream = new stream.Transform();
```

另一种方法是使用内置的 `fs` 模块：

```javascript
const fs = require('fs');

const readableStream = fs.createReadStream('/path/to/file');
const writableStream = fs.createWriteStream('/path/to/file');
```

## 管道流

管道是一种将流连接在一起以便数据从一个流流向另一个流的方法。

例如，您可以将可读流通过管道传输到可写流：

```javascript
readableStream.pipe(writableStream);
```

管道可用于将多个流链接在一起。例如，您可以将可读流通过管道传输到转换流，转换流转换数据，然后将转换流通过管道传输到可写流：

```javascript
readableStream.pipe(transformStream).pipe(writableStream);
```

## 错误处理

使用流时处理错误很重要。错误的发生可能有多种原因，例如流意外关闭或数据损坏。

使用流时，有几种不同的方法来处理错误。

一种方法是在流中监听“error”事件：

```javascript
stream.on('error', (err) => {
  // handle the error
});
```

另一种方法是使用带有回调函数的 .pipe() 方法：

```javascript
stream.pipe(destination, (err) => {
  // handle the error
});
```

最后，您可以使用带有 Promise 的 .catch() 方法：

```javascript
stream.catch((err) => {
  // handle the error
});
```

## 结论

在本文中，我们采用了一种实践方法来了解 Node.js 中的流和管道。我们涵盖了以下主题：

- 什么是流？
- 流类型
- 创建流
- 管道流
- 错误处理