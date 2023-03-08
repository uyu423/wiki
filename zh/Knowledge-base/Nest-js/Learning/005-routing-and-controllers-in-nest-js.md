---
title: 005: Nest.js 中的路由和控制器
description: 
published: true
date: 2023-02-14T16:32:32.708Z
tags: 
editor: markdown
dateCreated: 2023-02-14T16:32:24.569Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [005: Routing and controllers in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/005-routing-and-controllers-in-nest-js)
{.links-list}


# 介绍

Nest.js 是一个用于构建服务器端应用程序的 Node.js 框架。它基于 Express.js 并使用 TypeScript，它是 JavaScript 的超集，为语言添加了静态类型。

Nest.js 是一个相对较新的框架，因此它没有 Express.js 那样多的文档或社区支持。然而，它越来越受欢迎，并被微软、谷歌和亚马逊等公司使用。

在这篇文章中，我们将看看如何在 Nest.js 中设置路由和控制器。我们还将了解使用 Nest.js 相对于 Express.js 的一些好处。

# 在 Nest.js 中设置路由和控制器

我们需要做的第一件事是安装 Nest.js 框架。我们可以使用 Node.js 包管理器 npm 来完成此操作。

```
npm install --save @nestjs/common
```

安装 Nest.js 后，我们可以在我们的项目中创建一个名为 app.controller.ts 的新文件。该文件将包含我们的控制器逻辑。

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('/')
export class AppController {
  @Get()
  root() {
    return 'Hello, world!';
  }
}
```

在上面的代码中，我们从 @nestjs/common 导入了 Controller 和 Get 装饰器。然后我们使用 @Controller 装饰器在 / 路径上创建了一个新的控制器。

最后，我们创建了一个新的 root 方法并用 @Get 装饰器装饰它。当对 `/` 路径发出 GET 请求时，将调用此方法。

我们现在可以创建一个名为 main.ts 的新文件。该文件将用于启动我们的 Nest.js 应用程序。

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

在上面的代码中，我们从 `@nestjs/core` 导入了 `NestFactory` 和 `AppModule`。然后我们使用 `NestFactory` 来创建一个新的 Nest.js 应用程序并传入我们的 `AppModule`。

最后，我们调用了 listen 方法在端口 3000 上启动应用程序。

如果我们现在使用 `node main.ts` 运行应用程序，我们应该看到以下输出：

```
$ node main.ts
[Nest] 7100   - 2020-03-22 10:54:54   [NestFactory] Starting Nest application...
[Nest] 7100   - 2020-03-22 10:54:54   [InstanceLoader] AppModule dependencies initialized +0ms
[Nest] 7100   - 2020-03-22 10:54:54   [RouterExplorer] Mapped {,GET} route +2ms
[Nest] 7100   - 2020-03-22 10:54:54   [NestApplication] Nest application successfully started +2ms
```

如果我们现在打开浏览器并导航到“http://localhost:3000/”，我们应该会看到以下输出：

```
Hello, world!
```

# 结论

在本文中，我们了解了如何在 Nest.js 中设置路由和控制器。我们还研究了使用 Nest.js 相对于 Express.js 的一些好处。

如果您正在寻找使用 TypeScript 的 Node.js 框架，那么 Nest.js 绝对值得考虑。