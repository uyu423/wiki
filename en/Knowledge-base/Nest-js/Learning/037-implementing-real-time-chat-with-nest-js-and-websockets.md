---
title: 037: Implementing real-time chat with Nest.js and WebSockets
description: 
published: true
date: 2023-02-02T05:51:26.847Z
tags: 
editor: markdown
dateCreated: 2023-02-02T05:47:40.628Z
---

- [037: Implementación de chat en tiempo real con Nest.js y WebSockets***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/037-implementing-real-time-chat-with-nest-js-and-websockets)
{.links-list}
- [037：使用 Nest.js 和 WebSockets 实现实时聊天***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/037-implementing-real-time-chat-with-nest-js-and-websockets)
{.links-list}
- [037: Nest.js 및 WebSockets로 실시간 채팅 구현***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/037-implementing-real-time-chat-with-nest-js-and-websockets)
{.links-list}


# 037: Implementing real-time chat with Nest.js and WebSockets

In this post, we'll show you how to easily add real-time chat capabilities to a Nest.js web application using the WebSocket protocol.

## What is WebSocket?

WebSocket is a communication protocol that allows for full-duplex, bi-directional communication between a web browser and a web server. In other words, it allows for two-way communication between a client and a server in real-time.

## Why use WebSocket?

WebSocket is a great choice for building real-time applications such as chat apps, because it provides a persistent connection between a client and a server. This means that once a connection is established, both the client and the server can send and receive data at any time.

## How does WebSocket work?

The WebSocket protocol uses a handshake to establish a connection between a client and a server. Once the connection is established, the client and server can send and receive data in real-time.

## What is Nest.js?

Nest.js is a Node.js framework for building scalable server-side applications. It uses modern JavaScript, is built with TypeScript (which gives it strong typing) and combines elements of Object-Oriented Programming, Functional Programming, and Reactive Programming.

## Why use Nest.js?

Nest.js is a great choice for building server-side applications, because it is built on top of Node.js, which is a platform that is known for its scalability. In addition, Nest.js uses TypeScript, which gives it strong typing and a more structured codebase. Finally, Nest.js combines elements of Object-Oriented Programming, Functional Programming, and Reactive Programming, which makes it a very powerful framework.

## How does Nest.js work?

Nest.js is built on top of Node.js, which is a platform that is known for its scalability. In addition, Nest.js uses TypeScript, which gives it strong typing and a more structured codebase. Finally, Nest.js combines elements of Object-Oriented Programming, Functional Programming, and Reactive Programming, which makes it a very powerful framework.

## How to add real-time chat to a Nest.js web application using WebSocket

In this section, we'll show you how to add real-time chat capabilities to a Nest.js web application using the WebSocket protocol.

### Step 1: Create a Nest.js project

First, you'll need to create a Nest.js project. If you don't have Nest.js installed, you can install it using the following command:

```
npm install -g @nestjs/cli
```

Once Nest.js is installed, you can create a new Nest.js project using the following command:

```
nest new project-name
```

### Step 2: Install the WebSocket module

Next, you'll need to install the WebSocket module. The WebSocket module is a Node.js module that allows you to work with the WebSocket protocol.

You can install the WebSocket module using the following command:

```
npm install --save @nestjs/websockets
```

### Step 3: Enable the WebSocket module

Once the WebSocket module is installed, you'll need to enable it in your Nest.js application. You can do this by adding the following line of code to the src/app.module.ts file:

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

### Step 4: Create a WebSocket gateway

Next, you'll need to create a WebSocket gateway. A WebSocket gateway is a Nest.js service that handles incoming WebSocket connections.

You can create a WebSocket gateway using the following command:

```
nest generate gateway websocket
```

This will generate a new file, src/websocket/websocket.gateway.ts.

### Step 5: Handle incoming WebSocket connections

Once you have created the WebSocket gateway, you'll need to handle incoming WebSocket connections. You can do this by adding the following code to the src/websocket/websocket.gateway.ts file:

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

The @WebSocketGateway() decorator is used to create a WebSocket gateway. The @WebSocketServer() decorator is used to inject the WebSocket server into the WebSocket gateway. The @WebSocketConnect() decorator is used to handle incoming WebSocket connections. The @WebSocketDisconnect() decorator is used to handle WebSocket disconnections.

### Step 6: Create a chat service

Next, you'll need to create a chat service. The chat service will be responsible for sending and receiving messages.

You can create a chat service using the following command:

```
nest generate service chat
```

This will generate a new file, src/chat/chat.service.ts.

### Step 7: Implement the chat service

Once you have created the chat service, you'll need to implement it. You can do this by adding the following code to the src/chat/chat.service.ts file:

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

The ChatService class has two methods: sendMessage() and getMessages(). The sendMessage() method is used to send messages to the chat service. The getMessages() method is used to receive messages from the chat service.

### Step 8: Create a chat controller

Next, you'll need to create a chat controller. The chat controller will be responsible for handling HTTP requests.

You can create a chat controller using the following command:

```
nest generate controller chat
```

This will generate a new file, src/chat/chat.controller.ts.

### Step 9: Implement the chat controller

Once you have created the chat controller, you'll need to implement it. You can do this by adding the following code to the src/chat/chat.controller.ts file:

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

The ChatController class has two methods: getMessages() and sendMessage(). The getMessages() method is used to handle GET requests. The sendMessage() method is used to handle POST requests.

### Step 10: Connect the chat service to the WebSocket gateway

In this step, you'll need to connect the chat service to the WebSocket gateway. You can do this by adding the following code to the src/chat/chat.service.ts file:

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

The sendMessage() method uses the emit() method to send messages to the WebSocket server.

### Step 11: Connect the chat controller to the chat service

In this step, you'll need to connect the chat controller to the chat service. You can do this by adding the following code to the src/chat/chat.controller.ts file:

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

The getMessages() method uses the getMessages() method to get messages from the chat service. The sendMessage() method uses the sendMessage() method to send messages to the chat service.

### Step 12: Test the chat application

To test the chat application, you can use a tool like Postman.

First, you'll need to start the Nest.js application. You can do this by running the following command:

```
npm start
```

Next, you'll need to send a POST request to the /chat endpoint. You can do this by using the following URL:

```
http://localhost:3000/chat
```

In the body of the request, you'll need to include a message. For example, you could use the following message:

```
Hello, world!
```

Once you've sent the request, you should see the message appear in the console.

## Conclusion

In this post, we've shown you how to easily add real-time chat capabilities to a Nest.js web application using the WebSocket protocol.