---
title: 052：将 Nest.js 与服务器发送的事件 (SSE) 结合使用
description: 
published: true
date: 2023-02-05T18:55:21.302Z
tags: 
editor: markdown
dateCreated: 2023-02-05T18:55:19.661Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [052: Using Nest.js with Server-Sent Events (SSE)***English** document is available*](/en/Knowledge-base/Nest-js/Learning/052-using-nest-js-with-server-sent-events-sse)
{.links-list}


# 将 Nest.js 与服务器发送事件 (SSE) 结合使用

在这篇文章中，我们将介绍如何将 Nest.js 与服务器发送事件 (SSE) 结合使用。 Nest.js 是一个 Node.js 框架，可帮助您轻松构建服务器端应用程序。 SSE 是一种允许您将数据从服务器实时推送到客户端的技术。

我们将从设置 Nest.js 项目开始。然后，我们将创建一个控制器，使用 SSE 将数据推送到我们的客户端。最后，我们将创建一个将从服务器接收数据的客户端。

## 设置一个 Nest.js 项目

首先，让我们创建一个新的 Nest.js 项目。我们可以使用 Nest CLI 生成一个新项目。运行以下命令：

```
nest new sse-project
```

这将在名为 sse-project 的目录中创建一个新的 Nest.js 项目。

## 创建控制器

接下来，让我们创建一个将数据推送到客户端的控制器。创建一个名为 `src/controllers/data.controller.ts` 的新文件并添加以下代码：

```typescript
import { Controller, Get, Res } from '@nestjs/common';
import { Response } from 'express';

@Controller('data')
export class DataController {
  @Get()
  getData(@Res() res: Response) {
    // Set the content type of the response to "text/event-stream"
    res.setHeader('Content-Type', 'text/event-stream');
    // Push some data to the client
    res.write('data: This is some data\n\n');
    // Close the connection
    res.end();
  }
}
```

在这个控制器中，我们有一个用 @Get 装饰器装饰的 getData 方法。当客户端向 `/data` 端点发出 `GET` 请求时，将调用此方法。

`@Res` 装饰器将 `express` `Response` 对象注入到方法中。我们使用此对象将响应的“Content-Type”标头设置为“text/event-stream”并将数据推送到客户端。

## 创建客户端

现在我们有一个可以将数据推送到客户端的服务器，让我们创建一个可以接收数据的客户端。创建一个名为“client.html”的新文件并添加以下代码：

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>SSE Client</title>
  </head>
  <body>
    <h1>SSE Client</h1>
    <div id="data">
      <!-- Data from the server will be placed here -->
    </div>
    <script>
      const source = new EventSource('http://localhost:3000/data');
      source.onmessage = (event) => {
        const data = event.data;
        document.getElementById('data').innerHTML = data;
      };
    </script>
  </body>
</html>
```

在这个文件中，我们有一个 `<div>` 元素，其 `id` 为 `data`。这是放置来自服务器的数据的地方。

我们还有一个 `<script>` 元素，它创建一个新的 `EventSource` 对象。该对象将连接到我们服务器上的“/data”端点。然后我们注册一个 onmessage 事件处理程序，当服务器向客户端推送数据时将调用该事件处理程序。

## 运行应用程序

现在我们有了服务器和客户端，让我们运行应用程序。首先，通过运行以下命令启动服务器：

```
nest start
```

然后，在浏览器中打开“client.html”文件。您应该会看到来自服务器的数据显示在浏览器中。