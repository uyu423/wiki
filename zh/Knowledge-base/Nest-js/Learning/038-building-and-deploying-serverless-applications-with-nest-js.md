---
title: 038：使用 Nest.js 构建和部署无服务器应用程序
description: 
published: true
date: 2023-02-12T14:18:02.637Z
tags: 
editor: markdown
dateCreated: 2023-02-12T14:17:55.773Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [038: Building and deploying serverless applications with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/038-building-and-deploying-serverless-applications-with-nest-js)
{.links-list}


# 038：使用 Nest.js 构建和部署无服务器应用程序

在本文中，我们将学习如何使用 Nest.js 构建和部署无服务器应用程序。

Nest.js 是一个用于构建可扩展的服务器端应用程序的 Node.js 框架。它使用现代 JavaScript，使用 TypeScript（提供强类型）构建，并结合了面向对象编程、函数式编程和响应式编程的元素。

Nest.js 是构建无服务器应用程序的绝佳选择。它轻巧、快速，并提供广泛的功能，例如对 TypeScript 的支持、易于使用的依赖注入系统和强大的模块系统。

使用 Nest.js 构建无服务器应用程序既快速又简单。在本文中，我们将逐步介绍创建简单的无服务器 Nest.js 应用程序并将其部署到 AWS Lambda 的步骤。

## 创建一个 Nest.js 应用程序

首先，我们需要创建一个新的 Nest.js 应用程序。我们可以使用 Nest CLI 生成一个新项目：

```
nest new serverless-app
```

这将创建一个名为“serverless-app”的新文件夹，其中包含 Nest.js 应用程序所需的基本文件和文件夹。

接下来，我们需要安装“@nestjs/serverless”包。这个包提供了构建无服务器 Nest.js 应用程序所需的模块和依赖项：

```
npm install --save @nestjs/serverless
```

现在我们已经安装了“@nestjs/serverless”包，我们可以创建一个新的无服务器 Nest.js 应用程序。

我们首先在 `src` 文件夹中创建一个名为 `main.ts` 的新文件。该文件将成为我们的无服务器 Nest.js 应用程序的入口点。

在 main.ts 中，我们需要从 @nestjs/core 包中导入 NestFactory 类。此类将用于创建一个新的 Nest.js 应用程序：

```typescript
import { NestFactory } from '@nestjs/core';
```

接下来，我们需要从“@nestjs/serverless”包中导入“ServerlessApplicationModule”。该模块将用于引导我们的 Nest.js 应用程序：

```typescript
import { ServerlessApplicationModule } from '@nestjs/serverless';
```

现在我们已经导入了 `NestFactory` 和 `ServerlessApplicationModule` 类，我们可以使用它们来创建一个新的 Nest.js 应用程序：

```typescript
async function bootstrap() {
  const app = await NestFactory.create(ServerlessApplicationModule);
  await app.listen(3000);
}
bootstrap();
```

在上面的代码中，我们使用 NestFactory 类来创建一个新的 Nest.js 应用程序。我们将 `ServerlessApplicationModule` 传递给 `create` 方法来引导应用程序。

最后，我们使用 `listen` 方法在端口 3000 上启动应用程序。

## 创建控制器

现在我们已经创建了 Nest.js 应用程序，让我们创建一个控制器。控制器负责处理传入的 HTTP 请求和返回响应。

在 Nest.js 中，控制器被创建为类。让我们在 `src/controllers` 文件夹中创建一个名为 `hello.controller.ts` 的新文件。

在 hello.controller.ts 中，我们需要从 @nestjs/common 包中导入 Controller 装饰器。这个装饰器用于将一个类标记为控制器：

```typescript
import { Controller } from '@nestjs/common';
```

接下来，我们需要从 @nestjs/common 包中导入 Get 装饰器。此装饰器用于将控制器方法标记为 HTTP `GET` 请求的处理程序：

```typescript
import { Get } from '@nestjs/common';
```

现在我们已经导入了 `Controller` 和 `Get` 装饰器，我们可以使用它们来创建一个控制器：

```typescript
@Controller('hello')
export class HelloController {
  @Get()
  hello() {
    return 'Hello, world!';
  }
}
```

在上面的代码中，我们创建了一个名为“HelloController”的控制器。这个控制器有一个名为“hello”的方法，它返回字符串“Hello, world!”。

我们还使用了 `Controller` 装饰器来指定该控制器的路径。在这种情况下，我们将路径指定为“hello”。这意味着当对 `/hello` 路径发出 `GET` 请求时，将调用 `hello` 方法。

## 注册控制器

现在我们已经创建了控制器，我们需要在 Nest.js 应用程序中注册它。

我们可以通过在 main.ts 中导入控制器并将其传递给 NestFactory.create 方法来做到这一点：

```typescript
import { HelloController } from './controllers/hello.controller';

async function bootstrap() {
  const app = await NestFactory.create(
    ServerlessApplicationModule,
    {
      controllers: [HelloController],
    },
  );
  await app.listen(3000);
}
bootstrap();
```

在上面的代码中，我们从 `hello.controller.ts` 导入了 `HelloController`。然后我们将它传递到 `NestFactory.create` 方法中的 `controllers` 数组。

这将向我们的 Nest.js 应用程序注册“HelloController”。

## 部署应用

现在我们已经创建了 Nest.js 应用程序并注册了我们的控制器，我们准备好部署我们的应用程序了。

我们将把我们的应用程序部署到 AWS Lambda。 Lambda 是一个无服务器平台，允许我们在不配置或管理服务器的情况下运行代码。

要将我们的应用程序部署到 Lambda，我们将使用“nest deploy”命令。此命令将打包我们的应用程序并将其部署到 Lambda：

```
nest deploy
```

此命令将创建一个新的 Lambda 函数并将我们的 Nest.js 应用程序部署到它。

部署完成后，我们可以通过向 `/hello` 路径发出 `GET` 请求来测试我们的应用程序。我们应该看到返回的 `Hello, world!` 字符串。

## 结论

在本文中，我们学习了如何使用 Nest.js 构建和部署无服务器应用程序。

Nest.js 是构建无服务器应用程序的绝佳选择。它轻巧、快速，并提供广泛的功能，例如对 TypeScript 的支持、易于使用的依赖注入系统和强大的模块系统。

使用 Nest.js 构建无服务器应用程序既快速又简单。在本文中，我们介绍了创建简单的无服务器 Nest.js 应用程序并将其部署到 AWS Lambda 的步骤。