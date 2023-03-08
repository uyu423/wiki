---
title: 在 TypeScript 和 Node.js 中使用数据流
description: 
published: true
date: 2023-02-17T18:06:45.149Z
tags: 
editor: markdown
dateCreated: 2023-01-30T15:36:42.650Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Working with Data Streams in TypeScript and Node.js***English** version of this document is available*](/en/Knowledge-base/TypeScript/working-with-data-streams-in-typescript-and-node-js)
{.links-list}

    
# 介绍

在本文中，我们将研究如何在 TypeScript 和 Node.js 中使用数据流。我们将介绍 Node.js 中可用的不同类型的流、如何创建它们以及如何使用它们来处理数据。

Node.js 流是可以帮助您更高效地处理数据的强大工具。流可用于读取和写入数据，并且可以链接在一起对数据执行复杂的操作。

Node.js 中有四种主要的流类型：可读、可写、双工和转换。可读流允许您从源读取数据，可写流允许您将数据写入目标，双工流允许您读取和写入数据，而转换流允许您在读取或写入数据时修改数据。

在本文中，我们将重点关注前两种类型的流：可读和可写。我们将了解如何创建可读和可写流，以及如何使用它们来读写数据。

# 创建可读流

有几种不同的方法可以在 Node.js 中创建可读流。最简单的方法是使用 `fs.createReadStream()` 方法：

```javascript
const fs = require('fs');

const readableStream = fs.createReadStream('/path/to/file');
```

此方法将文件路径作为其唯一参数，并返回可用于读取文件内容的可读流。

另一种创建可读流的方法是使用 `net.createServer()` 方法：

```javascript
const net = require('net');

const server = net.createServer((socket) => {
  // socket is a readable stream
});
```

此方法创建一个 TCP 服务器，并返回一个可读流，可用于从服务器读取数据。

# 创建可写流

可以使用 `fs.createWriteStream()` 方法创建可写流：

```javascript
const fs = require('fs');

const writableStream = fs.createWriteStream('/path/to/file');
```

此方法将文件路径作为其唯一参数，并返回可用于将数据写入文件的可写流。

另一种创建可写流的方法是使用 net.createServer() 方法：

```javascript
const net = require('net');

const server = net.createServer((socket) => {
  // socket is a writable stream
});
```

此方法创建一个 TCP 服务器，并返回一个可写流，可用于将数据写入服务器。

# 从可读流中读取

创建可读流后，您可以使用 read() 方法开始从中读取数据：

```javascript
readableStream.read();
```

此方法从流中读取数据并将其作为字符串返回。

如果没有数据可供读取，`read()` 方法将返回 `null`。

# 写入可写流

一旦创建了可写流，就可以开始使用 `write()` 方法向其中写入数据：

```javascript
writableStream.write('some data');
```

此方法将数据写入流。数据可以是字符串或缓冲区。

# 管道流在一起

Node.js 流最强大的功能之一是能够将流通过管道连接在一起。

管道允许您将两个或多个流连接在一起，以便将来自一个流的数据自动发送到另一个流。

例如，您可以将可读流通过管道传输到可写流：

```javascript
readableStream.pipe(writableStream);
```

这将导致可读流中的数据写入可写流。

您还可以通过管道将多个流连接在一起。例如，您可以将可读流通过管道传输到转换流，然后将转换流通过管道传输到可写流：

```javascript
readableStream
  .pipe(transformStream)
  .pipe(writableStream);
```

这将导致可读流中的数据被转换流转换，然后写入可写流。

# 结论

在本文中，我们了解了如何在 TypeScript 和 Node.js 中使用数据流。我们已经介绍了 Node.js 中可用的不同类型的流、如何创建它们以及如何使用它们来处理数据。

Node.js 流是可以帮助您更高效地处理数据的强大工具。流可用于读取和写入数据，并且可以链接在一起对数据执行复杂的操作。

如果您希望了解有关在 Node.js 中处理数据的更多信息，请务必查看这些其他重要资源：

- [Node.js Stream 手册](https://nodestreams.com/)
- [Node.js 流 API](https://nodejs.org/api/stream.html)
- [在 Node.js 中处理流数据](https://www.twilio.com/blog/working-with-streaming-data-in-node-js)
- [Node.js 流：你需要知道的一切](https://www.freecodecamp.org/news/node-js-streams-everything-you-need-to-know-c9143706be93/)