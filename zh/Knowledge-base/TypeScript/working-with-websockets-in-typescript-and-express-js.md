---
title: 在 TypeScript 和 Express.js 中使用 WebSockets
description: 
published: true
date: 2023-02-17T18:12:07.207Z
tags: 
editor: markdown
dateCreated: 2023-01-30T18:57:49.585Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Working with WebSockets in TypeScript and Express.js***English** version of this document is available*](/en/Knowledge-base/TypeScript/working-with-websockets-in-typescript-and-express-js)
{.links-list}





WebSockets 是一种非常流行的客户端和服务器之间的通信方式。它们通过单个 TCP 连接提供双向、全双工通信通道，并得到所有主要浏览器的良好支持。

在本文中，我们将向您展示如何在 TypeScript 和 Express.js 中使用 WebSockets。我们还将提供一些实际示例，说明如何在您的 Web 应用程序中使用它们。

## 什么是 WebSocket？

WebSockets 是一项相对较新的技术，它支持 Web 浏览器和服务器之间的双向实时通信。它们是传统 HTTP 请求-响应模型的替代方案，并提供更高效的通信渠道。

 WebSockets 基于 TCP 协议，并使用全双工通信通道。这意味着客户端和服务器可以同时发送和接收数据。

所有主流浏览器都支持 WebSockets，并且有许多得到良好支持的库和框架可以让您在 Web 应用程序中轻松使用它们。

## 为什么使用 WebSockets？

WebSockets 提供了许多优于传统 HTTP 请求-响应模型的优势。

它们效率更高，因为它们只需要一个 TCP 连接，该连接在通信期间保持打开状态。这意味着不需要像 HTTP 那样为每个请求建立新的连接。

它们的延迟也低得多，因为无需等待请求完成才能发送下一个请求。这对于需要实时通信的应用程序尤其重要，例如聊天应用程序、在线游戏等。

## WebSocket 是如何工作的？

WebSockets 使用一个名为 ws:// 的协议，它是 HTTP 协议的扩展。当客户端想要与服务器建立 WebSocket 连接时，它会使用此协议发送请求。

然后服务器响应 HTTP 101 切换到 WebSockets 协议状态代码，然后连接升级为 WebSocket 连接。

一旦建立连接，客户端和服务器就可以随时发送和接收数据。

## 在 TypeScript 中使用 WebSockets

有许多库可用于在 TypeScript 中提供 WebSocket 支持，例如 ws 和 socket.io。在本文中，我们将使用 socket.io 库。

Socket.io 是一个流行且得到良好支持的库，可以让您在 TypeScript 应用程序中轻松使用 WebSockets。它抽象了 WebSocket 协议的细节，并提供了一个可用于发送和接收数据的简单 API。

Socket.io 还提供了许多其他功能，例如发布/订阅消息、房间等。

## 安装 Socket.io

Socket.io 可以使用 npm 包管理器安装：

```
npm install socket.io
```

## 创建一个 Socket.io 服务器

Socket.io 应用程序有两部分：在浏览器中运行的客户端库和在 Node.js 平台上运行的服务器端库。

在本节中，我们将创建一个简单的 Socket.io 服务器，它将向所有连接的客户端广播“hello world”消息。

首先，我们需要导入 socket.io 库：

```typescript
import * as io from "socket.io";
```

接下来，我们将使用 Express.js 框架创建一个 HTTP 服务器：

```typescript
const app = express();
const server = http.createServer(app);
```

然后我们可以将 Socket.io 库绑定到 HTTP 服务器：

```typescript
const io = socketIO(server);
```

现在我们已经启动并运行了 Socket.io 服务器，我们需要编写一些代码来处理传入的连接。我们可以使用 ```connection``` event:

```打字稿
io.on("连接", (socket) => {
  //
});
```

The ```connection``` event is emitted when a client connects to the server. The ```socket``` object that is passed to the callback function represents the client connection.

We can now write some code to send a message to the client:

```打字稿
io.on("连接", (socket) => {
  socket.emit("你好", "你好，世界！");
});
```

The ```emit``` method is used to send a message to the client. The first argument is the name of the event, and the second argument is the data to be sent.

## Creating a Socket.io client

Now that we have a Socket.io server up and running, let's create a client that will connect to it and print out the "hello world" message.

First, we need to include the Socket.io client library in our HTML page:

```html
<script src="/socket.io/socket.io.js"></script>
```

Next, we'll create a new ```Socket``` instance, and connect it to our server:

```javascript
const socket = io("http://localhost:8080");
```

We can then listen for the ```hello``` event that we defined on the server:

```javascript
socket.on("你好", (数据) => {
  控制台日志（数据）； // “你好世界！”
});
```

## Sending and receiving data

In the previous section, we saw how to send data from the server to the client. In this section, we'll see how to do the reverse: send data from the client to the server.

We can do this using the ```send``` method:

```javascript
socket.send("你好", "你好，世界！");
```

On the server, we can listen for the ```message``` event:

```打字稿
socket.on("消息", (数据) => {
  控制台日志（数据）； // “你好世界！”
});
```

##结论

在本文中，我们了解了如何在 TypeScript 和 Express.js 中使用 WebSockets。我们还了解了如何创建 Socket.io 服务器和客户端，以及如何在它们之间发送和接收数据。