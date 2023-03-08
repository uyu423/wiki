---
title: Node.js
description: 
published: true
date: 2023-02-01T02:04:40.962Z
tags: 
editor: markdown
dateCreated: 2023-02-01T02:04:39.377Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Node.js***English** version of this document is available*](/en/Knowledge-base/Dictionary/node-js)
{.links-list}


# 概述
Node.js 是一种开源、跨平台的 JavaScript 运行时环境，可在 Web 浏览器之外执行 JavaScript 代码。它用于创建服务器端和网络应用程序。 Node.js 旨在构建可扩展的网络应用程序，通常用于创建 Web 服务器和网络工具。

# 历史
Node.js 于 2009 年由 Ryan Dahl 创建。它最初是作为基于 Chrome 的 V8 JavaScript 引擎构建的 JavaScript 运行时发布的。自首次发布以来，Node.js 已成为最流行的 Web 开发平台之一。

# 描述
Node.js 是一个 JavaScript 运行时环境，允许开发人员使用 JavaScript 编写服务器端和网络应用程序。它基于 Chrome 的 V8 JavaScript 引擎构建，并使用事件驱动、非阻塞 I/O 模型，使其轻巧高效。 Node.js 旨在构建可扩展的网络应用程序，通常用于创建 Web 服务器和网络工具。

# 特征
Node.js 具有多项特性，使其成为极具吸引力的 Web 开发平台。它是开源的、跨平台的，并且拥有一个庞大、活跃的开发者社区。它还快速高效，具有事件驱动的非阻塞 I/O 模型，使其轻量级且高效。 Node.js 还拥有大量的库和模块，可以轻松开发应用程序。

# 例子
下面是一个创建 Web 服务器的 Node.js 应用程序的简单示例：

```
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

# 优点和缺点
Node.js 具有多项优势，使其成为极具吸引力的 Web 开发平台。它是开源的、跨平台的，并且拥有一个庞大、活跃的开发者社区。它还快速高效，具有事件驱动的非阻塞 I/O 模型，使其轻量级且高效。 Node.js 还拥有大量的库和模块，可以轻松开发应用程序。

然而，Node.js 也有一些缺点。它不适合 CPU 密集型应用程序，并且可能难以调试。此外，如果没有适当保护，Node.js 应用程序可能容易受到安全问题的影响。

#争议
由于使用 JavaScript 语言，Node.js 一直是一些争议的主题。一些开发人员认为 JavaScript 不是适合服务器端开发的语言，而其他人则认为它是 Web 开发的理想语言。

# 相关技术
Node.js 通常与其他技术结合使用，例如 MongoDB、Express.js 和 Angular.js。这些技术可以一起使用来创建强大的 Web 应用程序。

# 题外话
Node.js 通常用于创建实时应用程序，例如聊天应用程序和在线游戏。它还用于创建物联网 (IoT) 应用程序，例如家庭自动化系统。

# 其他
Node.js 是一个越来越流行的 Web 开发平台，许多大公司都在使用它，例如 Netflix、PayPal 和 Uber。它还用于创建桌面应用程序，例如 Atom 和 Visual Studio Code。