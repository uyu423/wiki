---
title: 015: Nest.js 中的错误处理
description: 
published: true
date: 2023-02-11T01:17:27.298Z
tags: 
editor: markdown
dateCreated: 2023-02-11T01:17:25.631Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [015: Error handling in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/015-error-handling-in-nest-js)
{.links-list}


# Nest.js 中的错误处理

开发 Web 应用程序可能很棘手 - 特别是涉及到错误处理时。在 Nest.js 中有很多方法可以处理错误，在这篇文章中我们将探索一些最常见的方法。

## 试着抓

try/catch 方法是 Nest.js 中最基本的错误处理方式。要使用此方法，您只需将代码包装在一个 try 块中，然后添加一个 catch 块来处理可能发生的任何错误。

这是一个简单的例子：

```javascript
try {
  // do something that might throw an error
} catch (err) {
  // handle the error
}
```

如果确实发生错误，它将被 catch 块捕获并进行相应处理。

## 异步错误处理

如果您使用的是异步代码（即使用 Promises 或 async/await 的代码），您仍然可以使用 try/catch 方法。但是，您需要注意以下事实：异步代码中抛出的错误实际上会被事件循环的下一个滴答捕获。

这意味着，如果你有一个围绕异步代码的 try/catch 块，则直到事件循环的下一个节拍才会执行 catch 块。这可能会令人困惑，所以让我们看一个例子：

```javascript
try {
  // do something that might throw an error
  setTimeout(() => {
    throw new Error('something went wrong');
  }, 1000);
} catch (err) {
  // this catch block will not be executed until 1000ms have passed
}
```

在上面的示例中，直到 1000 毫秒过去后才会捕获错误。这是因为 setTimeout 函数是异步的，错误只会在事件循环的下一次滴答时抛出。

为避免这种情况，您可以使用 Promise.catch 方法：

```javascript
try {
  // do something that might throw an error
  setTimeout(() => {
    throw new Error('something went wrong');
  }, 1000);
} catch (err) {
  // this catch block will not be executed until 1000ms have passed
}

Promise.catch((err) => {
  // this catch block will be executed immediately
});
```

## 错误处理中间件

如果你想集中你的错误处理，你可以使用 Nest.js 中间件。中间件是在请求到达您的控制器代码之前执行的功能。这使它成为放置错误处理逻辑的理想场所。

要创建中间件功能，您需要使用 @UseMiddleware 装饰器：

```javascript
import { UseMiddleware, Middleware } from '@nestjs/common';

@Middleware()
export class ErrorHandlerMiddleware implements NestMiddleware {
  // your middleware logic goes here
}
```

然后，要使用中间件，您需要在 Nest.js 模块中注册它：

```javascript
@Module({
  imports: [],
  controllers: [],
  providers: [],
  middleware: [ErrorHandlerMiddleware],
})
export class AppModule {}
```

现在，应用程序中发生的任何错误都将由中间件功能处理。

## 结论

如您所见，在 Nest.js 中有很多方法可以处理错误。您选择哪种方法取决于您的具体需求。但是，这篇文章中描述的所有方法都应该为您处理 Nest.js 应用程序中的错误提供一个良好的起点。