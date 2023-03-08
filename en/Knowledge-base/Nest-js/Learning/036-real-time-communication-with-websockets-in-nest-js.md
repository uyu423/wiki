---
title: 036: Real-time communication with WebSockets in Nest.js
description: 
published: true
date: 2023-02-08T11:56:15.060Z
tags: 
editor: markdown
dateCreated: 2023-02-08T11:56:08.842Z
---

- [036: Comunicación en tiempo real con WebSockets en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/036-real-time-communication-with-websockets-in-nest-js)
{.links-list}
- [036: 在 Nest.js 中与 WebSockets 进行实时通信***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/036-real-time-communication-with-websockets-in-nest-js)
{.links-list}
- [036: Nest.js에서 WebSocket과 실시간 통신***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/036-real-time-communication-with-websockets-in-nest-js)
{.links-list}


# Real-time communication with WebSockets in Nest.js

WebSocket is a computer communications protocol, providing full-duplex communication channels over a single TCP connection. The WebSocket protocol was standardized in 2011, and the WebSocket API in Web IDL is being standardized by the W3C.

WebSocket is designed to be implemented in web browsers and web servers, but it can be used by any client or server application. The WebSocket protocol makes possible more interaction between a browser and a web site, facilitating live content and the creation of real-time games. This is made possible by providing a standardized way for the server to send content to the browser without being solicited by the client, and allowing for messages to be passed back and forth while keeping the connection open. In this way, a two-way (bi-directional) ongoing conversation can take place between the browser and the server.

## How does WebSocket work?

WebSocket uses a long-held (two-way) TCP socket connection between the client and the server. Once the connection is established, it stays open until the client or server decides to close it. This is different from the typical HTTP connection, which is normally closed after each request/response cycle.

The WebSocket connection is initiated by an HTTP request with an Upgrade header. The client sends a request to the server, asking to upgrade the connection to a WebSocket from a normal HTTP connection. If the server agrees to upgrade the connection, it responds with an HTTP response with an Upgrade header. Once the connection is upgraded, the client and server can send each other data in both directions.

The data that is exchanged between the client and server is in the form of messages. Each message has a type, and a payload of data. The type of the message determines how the data in the payload is to be interpreted.

There are four message types:

- **Text**: The payload of the message is interpreted as a UTF-8 encoded string.
- **Binary**: The payload of the message is interpreted as raw binary data.
- **Close**: The connection is closed.
- **Ping**: The client is asking the server if it is still there. The server responds with a Pong message.

## Why use WebSocket?

HTTP is a great protocol, but it has some limitations. One of the main limitations is that it is a request/response protocol. This means that the client has to send a request to the server, and then wait for a response. The server can not send data to the client without the client first requesting it.

This limitation can be worked around by using polling. The client can send a request to the server asking if there is any new data, and the server can respond with the new data if there is any. This works, but it has some drawbacks.

- It is inefficient, as the client has to keep sending requests even if there is no new data.
- It adds latency, as the client has to wait for a response before it can send another request.
- It is not real-time, as there is a delay between the server generating new data, and the client receiving it.

WebSocket removes these limitations by providing a full-duplex communications channel over a single TCP connection. This means that the client and server can send data to each other at the same time, without having to wait for a response.

## Getting started with WebSocket in Nest.js

Nest.js is a framework for building server-side applications. It is built on top of Node.js, and uses TypeScript.

Nest.js provides a way to use WebSocket with the @nestjs/websockets module.

To use @nestjs/websockets, you need to install it from npm:

```
npm install @nestjs/websockets
```

Once @nestjs/websockets is installed, you can create a Nest.js server like this:

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

In the example above, we have imported the WsAdapter from @nestjs/platform-ws, and passed it to the useWebSocketAdapter() method. This will cause the Nest.js server to use the WebSocket protocol instead of HTTP.

We can then create a controller to handle WebSocket messages:

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

In the example above, we have created a controller with two methods. The first method, findAll(), is subscribed to the 'events' topic. This means that it will be called whenever a client sends a message to the 'events' topic. The findAll() method returns an Observable that will emit a message to the client.

The second method, identity(), is subscribed to the 'identity' topic. This means that it will be called whenever a client sends a message to the 'identity' topic. The identity() method returns an Observable that will emit the data that was sent by the client.

We have also defined two methods, handleConnection() and handleDisconnect(), which will be called when a client connects and disconnects from the WebSocket server.

## Sending and receiving messages

Once the Nest.js server is running, we can send messages to it using a WebSocket client. There are many WebSocket clients available, but for this example we will use the ws NPM package.

To install the ws package, run the following command:

```
npm install ws
```

Once the ws package is installed, we can create a client like this:

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

In the example above, we have created a WebSocket client that connects to the Nest.js server. We have defined two event handlers, one for when the connection is opened, and one for when a message is received.

In the open event handler, we are sending a message to the server. The message has a type of 'events', and a payload of 'hello world'.

In the message event handler, we are printing the data that was received from the server.

## Conclusion

In this article, we have seen how to use WebSocket to create real-time applications with Nest.js. We have seen how to create a Nest.js server, and how to send and receive messages with a WebSocket client.