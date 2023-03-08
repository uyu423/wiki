---
title: 037：使用 Nest.js 和 WebSockets 实现实时聊天
description: 
published: true
date: 2023-02-02T05:47:42.265Z
tags: 
editor: markdown
dateCreated: 2023-02-02T05:47:40.625Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [037: Implementing real-time chat with Nest.js and WebSockets***English** document is available*](/en/Knowledge-base/Nest-js/Learning/037-implementing-real-time-chat-with-nest-js-and-websockets)
{.links-list}


# 037：使用 Nest.js 和 WebSockets 实现实时聊天

在本文中，我们将向您展示如何使用 WebSocket 协议轻松地将实时聊天功能添加到 Nest.js 网络应用程序。

## 什么是 WebSocket？

WebSocket 是一种通信协议，允许在 Web 浏览器和 Web 服务器之间进行全双工、双向通信。换句话说，它允许客户端和服务器之间的实时双向通信。

## 为什么要使用 WebSocket？

WebSocket 是构建实时应用程序（如聊天应用程序）的绝佳选择，因为它提供了客户端和服务器之间的持久连接。这意味着一旦建立连接，客户端和服务器都可以随时发送和接收数据。

## WebSocket 是如何工作的？

WebSocket 协议使用握手在客户端和服务器之间建立连接。一旦建立连接，客户端和服务器就可以实时发送和接收数据。

## 什么是 Nest.js？

Nest.js 是一个用于构建可扩展的服务器端应用程序的 Node.js 框架。它使用现代 JavaScript，使用 TypeScript（赋予其强类型）构建，并结合了面向对象编程、函数式编程和响应式编程的元素。

## 为什么使用 Nest.js？

Nest.js 是构建服务器端应用程序的绝佳选择，因为它构建在 Node.js 之上，而 Node.js 是一个以可扩展性着称的平台。此外，Nest.js 使用 TypeScript，这赋予了它强类型化和更结构化的代码库。最后，Nest.js 结合了面向对象编程、函数式编程和响应式编程的元素，使其成为一个非常强大的框架。

## Nest.js 是如何工作的？

Nest.js 建立在 Node.js 之上，Node.js 是一个以可扩展性着称的平台。此外，Nest.js 使用 TypeScript，这赋予了它强类型化和更结构化的代码库。最后，Nest.js 结合了面向对象编程、函数式编程和响应式编程的元素，使其成为一个非常强大的框架。

## 如何使用 WebSocket 将实时聊天添加到 Nest.js web 应用程序

在本节中，我们将向您展示如何使用 WebSocket 协议向 Nest.js Web 应用程序添加实时聊天功能。

### Step 1: 创建一个 Nest.js 项目

首先，您需要创建一个 Nest.js 项目。如果你没有安装 Nest.js，你可以使用以下命令安装它：

```
npm install -g @nestjs/cli
```

安装 Nest.js 后，您可以使用以下命令创建一个新的 Nest.js 项目：

```
nest new project-name
```

### 步骤2：安装WebSocket模块

接下来，您需要安装 WebSocket 模块。 WebSocket 模块是一个 Node.js 模块，允许您使用 WebSocket 协议。

您可以使用以下命令安装 WebSocket 模块：

```
npm install --save @nestjs/websockets
```

### Step 3：启用WebSocket模块

安装 WebSocket 模块后，您需要在 Nest.js 应用程序中启用它。您可以通过将以下代码行添加到 src/app.module.ts 文件来执行此操作：

```typescript
@Module({
  imports: [
    // ...
    WebsocketsModule.forRoot(),
  ],
  // ...
})
export class AppModule {}
```

### 第四步：创建WebSocket网关

接下来，您需要创建一个 WebSocket 网关。 WebSocket 网关是处理传入 WebSocket 连接的 Nest.js 服务。

您可以使用以下命令创建 WebSocket 网关：

```
nest generate gateway websocket
```

这将生成一个新文件 src/websocket/websocket.gateway.ts。

### Step 5：处理传入的 WebSocket 连接

创建 WebSocket 网关后，您将需要处理传入的 WebSocket 连接。您可以通过将以下代码添加到 src/websocket/websocket.gateway.ts 文件来执行此操作：

```typescript
@WebSocketGateway()
export class WebsocketGateway {

  @WebSocketServer()
  server;

  @WebSocketConnect()
  connect(@ConnectedSocket() socket) {
    // ...
  }

  @WebSocketDisconnect()
  disconnect(@ConnectedSocket() socket) {
    // ...
  }

}
```

@WebSocketGateway() 装饰器用于创建 WebSocket 网关。 @WebSocketServer() 装饰器用于将 WebSocket 服务器注入 WebSocket 网关。 @WebSocketConnect() 装饰器用于处理传入的 WebSocket 连接。 @WebSocketDisconnect() 装饰器用于处理 WebSocket 断开连接。

### Step 6：创建聊天服务

接下来，您需要创建一个聊天服务。聊天服务将负责发送和接收消息。

您可以使用以下命令创建聊天服务：

```
nest generate service chat
```

这将生成一个新文件 src/chat/chat.service.ts。

### Step 7: 实现聊天服务

创建聊天服务后，您需要实施它。您可以通过将以下代码添加到 src/chat/chat.service.ts 文件来执行此操作：

```typescript
@Injectable()
export class ChatService {

  constructor(
    private readonly websocketGateway: WebsocketGateway,
  ) {}

  sendMessage(message: string) {
    // ...
  }

  getMessages() {
    // ...
  }

}
```

ChatService 类有两个方法：sendMessage() 和 getMessages()。 sendMessage() 方法用于向聊天服务发送消息。 getMessages() 方法用于接收来自聊天服务的消息。

### Step 8: 创建一个聊天控制器

接下来，您需要创建一个聊天控制器。聊天控制器将负责处理 HTTP 请求。

您可以使用以下命令创建聊天控制器：

```
nest generate controller chat
```

这将生成一个新文件 src/chat/chat.controller.ts。

### Step 9: 实现聊天控制器

创建聊天控制器后，您需要实施它。您可以通过将以下代码添加到 src/chat/chat.controller.ts 文件来执行此操作：

```typescript
@Controller('chat')
export class ChatController {

  constructor(
    private readonly chatService: ChatService,
  ) {}

  @Get()
  getMessages() {
    // ...
  }

  @Post()
  sendMessage(@Body() message: string) {
    // ...
  }

}
```

ChatController 类有两个方法：getMessages() 和 sendMessage()。 getMessages() 方法用于处理 GET 请求。 sendMessage() 方法用于处理 POST 请求。

### Step 10: 将聊天服务连接到 WebSocket 网关

在此步骤中，您需要将聊天服务连接到 WebSocket 网关。您可以通过将以下代码添加到 src/chat/chat.service.ts 文件来执行此操作：

```typescript
@Injectable()
export class ChatService {

  constructor(
    private readonly websocketGateway: WebsocketGateway,
  ) {}

  sendMessage(message: string) {
    this.websocketGateway.server.emit('message', message);
  }

  getMessages() {
    // ...
  }

}
```

sendMessage() 方法使用 emit() 方法向 WebSocket 服务器发送消息。

### Step 11：将聊天控制器连接到聊天服务

在此步骤中，您需要将聊天控制器连接到聊天服务。您可以通过将以下代码添加到 src/chat/chat.controller.ts 文件来执行此操作：

```typescript
@Controller('chat')
export class ChatController {

  constructor(
    private readonly chatService: ChatService,
  ) {}

  @Get()
  getMessages() {
    return this.chatService.getMessages();
  }

  @Post()
  sendMessage(@Body() message: string) {
    this.chatService.sendMessage(message);
  }

}
```

getMessages() 方法使用 getMessages() 方法从聊天服务获取消息。 sendMessage() 方法使用 sendMessage() 方法向聊天服务发送消息。

### Step 12: 测试聊天应用

要测试聊天应用程序，您可以使用像 Postman 这样的工具。

首先，您需要启动 Nest.js 应用程序。您可以通过运行以下命令来执行此操作：

```
npm start
```

接下来，您需要向 /chat 端点发送 POST 请求。您可以使用以下 URL 执行此操作：

```
http://localhost:3000/chat
```

在请求正文中，您需要包含一条消息。例如，您可以使用以下消息：

```
Hello, world!
```

发送请求后，您应该会在控制台中看到该消息。

## 结论

在本文中，我们向您展示了如何使用 WebSocket 协议轻松地将实时聊天功能添加到 Nest.js 网络应用程序。