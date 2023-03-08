---
title: 036: 在 Nest.js 中与 WebSockets 进行实时通信
description: 
published: true
date: 2023-02-08T11:56:10.516Z
tags: 
editor: markdown
dateCreated: 2023-02-08T11:56:08.832Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [036: Real-time communication with WebSockets in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/036-real-time-communication-with-websockets-in-nest-js)
{.links-list}


# 在 Nest.js 中与 WebSockets 实时通信

WebSocket 是一种计算机通信协议，通过单个 TCP 连接提供全双工通信通道。 WebSocket 协议在 2011 年被标准化，Web IDL 中的 WebSocket API 正在被 W3C 标准化。

WebSocket 旨在在 Web 浏览器和 Web 服务器中实现，但它可以被任何客户端或服务器应用程序使用。 WebSocket 协议使浏览器和网站之间的更多交互成为可能，促进了实时内容和实时游戏的创建。这是通过为服务器提供一种标准化的方式来向浏览器发送内容而无需客户端请求，并允许在保持连接打开的情况下来回传递消息来实现的。通过这种方式，可以在浏览器和服务器之间进行双向（双向）正在进行的对话。

## WebSocket 是如何工作的？

WebSocket 在客户端和服务器之间使用长期（双向）TCP 套接字连接。建立连接后，它将保持打开状态，直到客户端或服务器决定关闭它。这与典型的 HTTP 连接不同，后者通常在每个请求/响应周期后关闭。

WebSocket 连接由带有升级标头的 HTTP 请求发起。客户端向服务器发送请求，要求将连接从普通的 HTTP 连接升级到 WebSocket。如果服务器同意升级连接，它会使用带有升级标头的 HTTP 响应进行响应。一旦连接升级，客户端和服务器就可以双向相互发送数据。

客户端和服务器之间交换的数据采用消息的形式。每条消息都有一个类型和一个数据负载。消息的类型决定了如何解释有效负载中的数据。

有四种消息类型：

- **文本**：消息的有效负载被解释为 UTF-8 编码的字符串。
- **二进制**：消息的有效负载被解释为原始二进制数据。
- **关闭**：连接已关闭。
- **Ping**：客户端正在询问服务器是否仍然存在。服务器以 Pong 消息响应。

## 为什么要使用 WebSocket？

HTTP 是一个很棒的协议，但它有一些局限性。主要限制之一是它是一个请求/响应协议。这意味着客户端必须向服务器发送请求，然后等待响应。没有客户端首先请求，服务器不能向客户端发送数据。

这个限制可以通过使用轮询来解决。客户端可以向服务器发送请求，询问是否有新数据，如果有，服务器可以响应新数据。这可行，但它有一些缺点。

- 这是低效的，因为即使没有新数据，客户端也必须继续发送请求。
- 它增加了延迟，因为客户端必须等待响应才能发送另一个请求。
- 它不是实时的，因为在服务器生成新数据和客户端接收数据之间存在延迟。

WebSocket 通过在单个 TCP 连接上提供全双工通信通道消除了这些限制。这意味着客户端和服务器可以同时向对方发送数据，而不必等待响应。

## Nest.js 中的 WebSocket 入门

Nest.js 是用于构建服务器端应用程序的框架。它建立在 Node.js 之上，并使用 TypeScript。

Nest.js 提供了一种通过 @nestjs/websockets 模块使用 WebSocket 的方法。

要使用@nestjs/websockets，你需要从 npm 安装它：

```
npm install @nestjs/websockets
```

安装 @nestjs/websockets 后，您可以像这样创建一个 Nest.js 服务器：

```typescript
import { NestFactory } from '@nestjs/core';
import { WsAdapter } from '@nestjs/platform-ws';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.useWebSocketAdapter(new WsAdapter(app));
  await app.listen(3000);
}
bootstrap();
```

在上面的示例中，我们从@nestjs/platform-ws 导入了 WsAdapter，并将其传递给 useWebSocketAdapter() 方法。这将导致 Nest.js 服务器使用 WebSocket 协议而不是 HTTP。

然后我们可以创建一个控制器来处理 WebSocket 消息：

```typescript
import {
  Controller,
  OnGatewayConnection,
  OnGatewayDisconnect,
  SubscribeMessage,
  WebSocketGateway,
  WsResponse,
} from '@nestjs/websockets';
import { Observable, of } from 'rxjs';
import { map } from 'rxjs/operators';

@Controller()
@WebSocketGateway()
export class AppController {
  @SubscribeMessage('events')
  findAll(client, data): Observable<WsResponse<number[]>> {
    return of([1, 2, 3]).pipe(map(item => ({ event: 'events', data: item })));
  }

  @SubscribeMessage('identity')
  identity(client, data: number): Observable<number> {
    return of(data);
  }

  @OnGatewayConnection()
  handleConnection(client) {
    console.log('Client connected');
  }

  @OnGatewayDisconnect()
  handleDisconnect(client) {
    console.log('Client disconnected');
  }
}
```

在上面的例子中，我们创建了一个有两个方法的控制器。第一个方法 findAll() 订阅了“事件”主题。这意味着只要客户端向“事件”主题发送消息，它就会被调用。 findAll() 方法返回一个 Observable，它将向客户端发送消息。

第二种方法 identity() 订阅了“identity”主题。这意味着只要客户端向“身份”主题发送消息，它就会被调用。 identity() 方法返回一个 Observable，它将发出客户端发送的数据。

我们还定义了两个方法，handleConnection() 和 handleDisconnect()，当客户端连接和断开与 WebSocket 服务器的连接时将调用它们。

## 发送和接收消息

Nest.js 服务器运行后，我们可以使用 WebSocket 客户端向其发送消息。有许多可用的 WebSocket 客户端，但对于本示例，我们将使用 ws NPM 包。

要安装 ws 包，请运行以下命令：

```
npm install ws
```

安装 ws 包后，我们可以像这样创建一个客户端：

```javascript
const WebSocket = require('ws');

const ws = new WebSocket('ws://localhost:3000');

ws.on('open', function open() {
  console.log('connected');
  ws.send(JSON.stringify({ event: 'events', data: 'hello world' }));
});

ws.on('message', function incoming(data) {
  console.log(data);
});
```

在上面的示例中，我们创建了一个连接到 Nest.js 服务器的 WebSocket 客户端。我们定义了两个事件处理程序，一个用于打开连接，一个用于接收消息。

在打开事件处理程序中，我们向服务器发送消息。该消息具有“事件”类型和“hello world”负载。

在消息事件处理程序中，我们正在打印从服务器接收到的数据。

## 结论

在本文中，我们了解了如何使用 WebSocket 通过 Nest.js 创建实时应用程序。我们已经了解了如何创建 Nest.js 服务器，以及如何使用 WebSocket 客户端发送和接收消息。