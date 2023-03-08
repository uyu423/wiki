---
title: 053: Using Nest.js with WebRTC for real-time communication
description: 
published: true
date: 2023-02-06T23:56:02.414Z
tags: 
editor: markdown
dateCreated: 2023-02-06T23:55:56.704Z
---

- [053: Uso de Nest.js con WebRTC para comunicación en tiempo real***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/053-using-nest-js-with-webrtc-for-real-time-communication)
{.links-list}
- [053: 使用 Nest.js 和 WebRTC 进行实时通信***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/053-using-nest-js-with-webrtc-for-real-time-communication)
{.links-list}
- [053: 실시간 통신을 위해 WebRTC와 함께 Nest.js 사용***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/053-using-nest-js-with-webrtc-for-real-time-communication)
{.links-list}


# 05: Using Nest.js with WebRTC for real-time communication

WebRTC is a powerful tool that can be used for a variety of applications, including real-time communication. Nest.js is a Node.js framework that can be used to build scalable applications. In this post, we'll show you how to use Nest.js with WebRTC to build a real-time communication application.

## Prerequisites

Before we get started, there are a few things you'll need to have in order to follow along. First, you'll need to have Node.js and npm installed. You can find instructions for how to do this here: [Node.js](https://nodejs.org/en/download/) and [npm](https://www.npmjs.com/get-npm).

Next, you'll need to install the Nest.js CLI. You can do this by running the following command:

```
npm install -g @nestjs/cli
```

## Creating a Nest.js project

Now that you have the Nest.js CLI installed, you can use it to create a new Nest.js project. To do this, run the following command:

```
nest new project-name
```

Replace "project-name" with the name of your project. This will create a new directory with the same name and initialize a new Nest.js project inside of it.

## Installing dependencies

Now that you have a Nest.js project, you'll need to install some dependencies. The first dependency you'll need is [Socket.io](https://socket.io/). Socket.io is a real-time communication library that will be used to handle the communication between the client and server. To install it, run the following command:

```
npm install socket.io
```

The next dependency you'll need is [Express](https://expressjs.com/). Express is a web application framework for Node.js that will be used to serve the static files for the client. To install it, run the following command:

```
npm install express
```

## Configuring Socket.io

Now that you have the dependencies installed, you'll need to configure Socket.io. To do this, open the "src/main.ts" file and add the following code:

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import * as socketIo from 'socket.io';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  const server = app.getHttpServer();
  const io = socketIo(server);

  app.useStaticAssets(join(__dirname, '..', 'public'));
  app.setBaseViewsDir(join(__dirname, '..', 'views'));
  app.setViewEngine('hbs');

  await app.listen(3000);
}
bootstrap();
```

This code will configure Socket.io to use the Nest.js server. It will also configure Express to serve the static files from the "public" directory and the views from the "views" directory.

## Creating the controller

Now that you have Socket.io configured, you can create the controller. To do this, run the following command:

```
nest generate controller controller-name
```

Replace "controller-name" with the name of your controller. This will generate a new file in the "src/controllers" directory with the name "controller-name.controller.ts".

Open the "src/controllers/controller-name.controller.ts" file and add the following code:

```javascript
import { Controller, Post, Body, Req, UseGuards } from '@nestjs/common';
import { Socket } from 'socket.io';
import { AuthGuard } from '@nestjs/passport';

@Controller('controller-name')
export class ControllerNameController {

  @UseGuards(AuthGuard())
  @Post('message')
  async message(@Req() req, @Body() body, @Socket() socket: Socket) {
    socket.emit('message', body);
  }

}
```

This code creates a controller with a single endpoint. The endpoint is a POST request that accepts a message body. The message is then emitted to the client using Socket.io.

## Creating the view

Now that you have the controller created, you can create the view. To do this, create a new file in the "views" directory with the name "index.hbs". Add the following code to the "index.hbs" file:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>WebRTC with Nest.js</title>
  </head>
  <body>
    <form id="form">
      <input type="text" id="message">
      <button type="submit">Send</button>
    </form>
    <div id="messages"></div>
    <script src="/socket.io/socket.io.js"></script>
    <script>
      const socket = io();
      const form = document.getElementById('form');
      const message = document.getElementById('message');
      const messages = document.getElementById('messages');

      form.addEventListener('submit', (e) => {
        e.preventDefault();
        socket.emit('message', message.value);
        message.value = '';
      });

      socket.on('message', (msg) => {
        const li = document.createElement('li');
        li.innerHTML = msg;
        messages.appendChild(li);
      });
    </script>
  </body>
</html>
```

This code creates a simple HTML form that allows the user to enter a message. The message is then emitted to the server using Socket.io. The server will then emit the message to all clients. The message will then be displayed on the page.

## Running the application

Now that you have the application created, you can run it by running the following command:

```
npm start
```

You can then access the application at http://localhost:3000.

## Conclusion

In this post, we've shown you how to use Nest.js with WebRTC to build a real-time communication application. We've also shown you how to use Socket.io to handle the communication between the client and server.