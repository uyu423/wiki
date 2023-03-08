---
title: 软件开发 011：Node.js 和 Express.js
description: 
published: true
date: 2023-02-16T11:55:36.817Z
tags: 
editor: markdown
dateCreated: 2023-02-16T11:55:34.910Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Software Development 011: Node.js and Express.js***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-011-node-js-and-express-js)
{.links-list}


# 软件开发 011：Node.js 和 Express.js

在这篇文章中，我们将研究 Node.js 和 Express.js，这两种用于软件开发的流行工具。

Node.js 是一个 JavaScript 运行时环境，允许您在浏览器之外运行 JavaScript 代码。这使其成为开发服务器端应用程序的理想选择。

Express.js 是 Node.js 的 Web 应用程序框架。它提供了一组用于构建 Web 应用程序的工具。

## 节点

Node.js 是一个 JavaScript 运行时环境，允许您在浏览器之外运行 JavaScript 代码。这使其成为开发服务器端应用程序的理想选择。

Node.js 基于谷歌浏览器中使用的 V8 JavaScript 引擎。 Node.js 还有一个庞大的开源库生态系统，可用于各种任务。

### 安装 Node.js

安装 Node.js 是一个简单的过程。您可以从 [Node.js 网站](https://nodejs.org/en/) 下载 Node.js 安装程序。

下载安装程序后，运行它并按照说明进行操作。 Node.js 将安装在您的计算机上。

### 运行 Node.js

安装 Node.js 后，您可以使用 Node.js 运行时运行 JavaScript 代码。

要运行 JavaScript 文件，请使用以下命令：

```
node {filename}
```

例如，要运行名为“hello.js”的文件，您可以使用以下命令：

```
node hello.js
```

Node.js 将执行 hello.js 文件中的代码并将结果打印到控制台。

## Express.js

Express.js 是 Node.js 的 Web 应用程序框架。它提供了一组用于构建 Web 应用程序的工具。

Express.js 是构建 Web 应用程序的流行选择。它易于使用并且拥有庞大的用户社区。

### 你好世界

让我们创建一个简单的“Hello, World!”使用 Express.js 的应用程序。

创建一个名为“hello.js”的文件并添加以下代码：

```javascript
const express = require('express');

const app = express();

app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(3000, () => {
  console.log('Hello, World! app is listening on port 3000');
});
```

此代码创建一个 Express.js 应用程序，该应用程序使用“Hello, World!”响应 HTTP `GET` 请求。信息。

`app.listen()` 方法在端口 3000 上启动 Express.js 应用程序。

要运行该应用程序，请使用以下命令：

```
node hello.js
```

您现在可以通过 http://localhost:3000 访问该应用程序。

## 结论

在这篇文章中，我们研究了 Node.js 和 Express.js。我们已经了解了如何使用 Node.js 运行时安装 Node.js 和运行 JavaScript 代码。我们还了解了如何使用 Express.js 创建一个简单的 Web 应用程序。