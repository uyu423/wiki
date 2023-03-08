---
title: 使用 TypeScript 和 WebSockets 创建实时应用程序
description: 
published: true
date: 2023-01-31T10:57:33.948Z
tags: 
editor: markdown
dateCreated: 2023-01-31T10:57:32.383Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Creating Real-Time Applications with TypeScript and WebSockets***English** version of this document is available*](/en/Knowledge-base/TypeScript/creating-real-time-applications-with-typescript-and-websockets)
{.links-list}



# 使用 TypeScript 和 WebSockets 创建实时应用程序

WebSockets 是用于创建实时应用程序的强大工具。结合 TypeScript，它们可以通过静态类型检查、代码完成等提供出色的开发体验。在本文中，我们将探索如何使用 TypeScript 和 WebSockets 创建一个简单的聊天应用程序。

## 什么是 WebSocket？

WebSockets 是一种通过现有 TCP 连接创建双向实时通信通道的技术。它们受到所有主要浏览器的支持，可用于创建各种应用程序，从简单的聊天客户端到复杂的多人游戏。

## 入门

首先，我们需要设置一个可以处理 WebSocket 连接的服务器。对于本文，我们将使用流行的 Node.js 框架 Express。

首先，我们将为我们的项目创建一个新目录并安装依赖项：

```
mkdir chat-app
cd chat-app
npm init -y
npm install --save express
npm install --save ws
```

接下来，我们将为我们的服务器代码创建一个文件：

```
touch server.js
```

并粘贴以下代码：

```javascript
const express = require('express');
const WebSocket = require('ws');

const app = express();

const PORT = process.env.PORT || 8080;

const server = app.listen(PORT, () => {
  console.log(`Server listening on port ${PORT}`);
});

const wss = new WebSocket.Server({ server });

wss.on('connection', (ws) => {
  console.log('Client connected');

  ws.on('message', (message) => {
    console.log(`Received message: ${message}`);
  });

  ws.send('Hello!');
});
```

让我们分解一下这里发生的事情。首先，我们需要 Express 和 WebSocket 模块。接下来，我们创建一个 Express 服务器并将其配置为侦听端口 8080。然后，我们创建一个新的 WebSocket 服务器，将 Express 服务器作为“服务器”选项传入。

接下来，我们为客户端连接到 WebSocket 服务器时设置一个事件处理程序。当客户端连接时，我们会向控制台记录一条消息。然后，我们为客户端发送消息时设置事件处理程序。收到消息后，我们再次将其记录到控制台。最后，我们向客户端发送一条消息。

要运行服务器，我们可以使用 node 命令：

```
node server.js
```

## 创建客户端

现在我们已经启动并运行了服务器，让我们创建一个客户端。对于本文，我们将使用流行的 React 框架。

首先，我们需要安装依赖项：

```
npm install --save react
npm install --save react-dom
npm install --save @types/react
npm install --save @types/react-dom
npm install --save ws
npm install --save @types/ws
```

然后，我们将为我们的客户端代码创建一个文件：

```
touch client.js
```

并粘贴以下代码：

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import * as ws from 'ws';

const socket = new ws('ws://localhost:8080');

socket.onopen = () => {
  console.log('Connected to server');
};

socket.onmessage = (event) => {
  console.log(event.data);
};

socket.send('Hello from the client!');

ReactDOM.render(
  <div>Hello, world!</div>,
  document.getElementById('root')
);
```

首先，我们导入 React 和 ReactDOM 模块。然后，我们导入 WebSocket 模块。接下来，我们创建一个新的 WebSocket 实例，传入我们服务器的 URL。

然后，我们为套接字何时打开以及何时收到消息设置事件处理程序。当套接字打开时，我们将一条消息记录到控制台。收到消息后，我们再次将其记录到控制台。最后，我们向服务器发送消息。

## 结论

在本文中，我们了解了如何使用 TypeScript 和 WebSockets 创建一个简单的聊天应用程序。虽然这个示例很简单，但它展示了 WebSockets 在创建实时应用程序方面的强大功能。