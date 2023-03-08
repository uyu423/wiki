---
title: 053: 使用 Nest.js 和 WebRTC 进行实时通信
description: 
published: true
date: 2023-02-06T23:55:58.392Z
tags: 
editor: markdown
dateCreated: 2023-02-06T23:55:56.700Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [053: Using Nest.js with WebRTC for real-time communication***English** document is available*](/en/Knowledge-base/Nest-js/Learning/053-using-nest-js-with-webrtc-for-real-time-communication)
{.links-list}


# 05: 使用 Nest.js 和 WebRTC 进行实时通信

WebRTC 是一个强大的工具，可用于各种应用，包括实时通信。 Nest.js 是一个 Node.js 框架，可用于构建可扩展的应用程序。在本文中，我们将向您展示如何将 Nest.js 与 WebRTC 结合使用来构建实时通信应用程序。

## 先决条件

在我们开始之前，您需要做一些事情才能跟进。首先，您需要安装 Node.js 和 npm。您可以在此处找到有关如何执行此操作的说明：[Node.js](https://nodejs.org/en/download/) 和 [npm](https://www.npmjs.com/get-npm)。

接下来，您需要安装 Nest.js CLI。您可以通过运行以下命令来执行此操作：

```
npm install -g @nestjs/cli
```

## 创建一个 Nest.js 项目

现在您已经安装了 Nest.js CLI，您可以使用它来创建一个新的 Nest.js 项目。为此，请运行以下命令：

```
nest new project-name
```

将“项目名称”替换为您的项目名称。这将创建一个同名的新目录，并在其中初始化一个新的 Nest.js 项目。

## 安装依赖

现在你有了一个 Nest.js 项目，你需要安装一些依赖项。您需要的第一个依赖项是 [Socket.io](https://socket.io/)。 Socket.io 是一个实时通信库，用于处理客户端和服务器之间的通信。要安装它，请运行以下命令：

```
npm install socket.io
```

您需要的下一个依赖项是 [Express](https://expressjs.com/)。 Express 是 Node.js 的 Web 应用程序框架，将用于为客户端提供静态文件。要安装它，请运行以下命令：

```
npm install express
```

## 配置 Socket.io

现在您已经安装了依赖项，您需要配置 Socket.io。为此，打开“src/main.ts”文件并添加以下代码：

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

此代码将配置 Socket.io 以使用 Nest.js 服务器。它还将配置 Express 以提供来自“public”目录的静态文件和来自“views”目录的视图。

## 创建控制器

现在您已经配置了 Socket.io，您可以创建控制器。为此，请运行以下命令：

```
nest generate controller controller-name
```

将“控制器名称”替换为您的控制器名称。这将在“src/controllers”目录中生成一个名为“controller-name.controller.ts”的新文件。

打开“src/controllers/controller-name.controller.ts”文件并添加以下代码：

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

此代码创建一个具有单个端点的控制器。端点是接受消息正文的 POST 请求。然后使用 Socket.io 将消息发送到客户端。

## 创建视图

现在您已经创建了控制器，您可以创建视图了。为此，在“views”目录中创建一个名为“index.hbs”的新文件。将以下代码添加到“index.hbs”文件中：

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

此代码创建一个简单的 HTML 表单，允许用户输入消息。然后使用 Socket.io 将消息发送到服务器。然后服务器将向所有客户端发送消息。然后该消息将显示在页面上。

## 运行应用程序

现在您已经创建了应用程序，您可以通过运行以下命令来运行它：

```
npm start
```

然后，您可以通过 http://localhost:3000 访问该应用程序。

## 结论

在本文中，我们向您展示了如何将 Nest.js 与 WebRTC 结合使用来构建实时通信应用程序。我们还向您展示了如何使用 Socket.io 来处理客户端和服务器之间的通信。