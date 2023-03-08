---
title: 052: Using Nest.js with Server-Sent Events (SSE)
description: 
published: true
date: 2023-02-05T18:55:25.229Z
tags: 
editor: markdown
dateCreated: 2023-02-05T18:55:19.669Z
---

- [052: uso de Nest.js con eventos enviados por el servidor (SSE)***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/052-using-nest-js-with-server-sent-events-sse)
{.links-list}
- [052：将 Nest.js 与服务器发送的事件 (SSE) 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/052-using-nest-js-with-server-sent-events-sse)
{.links-list}
- [052: 서버 전송 이벤트(SSE)와 함께 Nest.js 사용***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/052-using-nest-js-with-server-sent-events-sse)
{.links-list}


# Using Nest.js with Server-Sent Events (SSE)

In this post, we'll go over how to use Nest.js with Server-Sent Events (SSE). Nest.js is a Node.js framework that helps you easily build server-side applications. SSE is a technology that allows you to push data from a server to a client in real-time.

We'll start by setting up a Nest.js project. Then, we'll create a controller that will push data to our client using SSE. Finally, we'll create a client that will receive the data from the server.

## Setting up a Nest.js project

First, let's create a new Nest.js project. We can use the Nest CLI to generate a new project. Run the following command:

```
nest new sse-project
```

This will create a new Nest.js project in a directory called `sse-project`.

## Creating a controller

Next, let's create a controller that will push data to our client. Create a new file called `src/controllers/data.controller.ts` and add the following code:

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

In this controller, we have a `getData` method that is decorated with the `@Get` decorator. This method will be called when a client makes a `GET` request to the `/data` endpoint.

The `@Res` decorator injects the `express` `Response` object into the method. We use this object to set the `Content-Type` header of the response to `text/event-stream` and to push data to the client.

## Creating a client

Now that we have a server that can push data to a client, let's create a client that can receive the data. Create a new file called `client.html` and add the following code:

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

In this file, we have a `<div>` element with an `id` of `data`. This is where the data from the server will be placed.

We also have a `<script>` element that creates a new `EventSource` object. This object will connect to the `/data` endpoint on our server. We then register a `onmessage` event handler that will be called when the server pushes data to the client.

## Running the application

Now that we have a server and a client, let's run the application. First, start the server by running the following command:

```
nest start
```

Then, open the `client.html` file in a browser. You should see the data from the server being displayed in the browser.