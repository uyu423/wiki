---
title: 027：使用 Nest.js 实现微服务
description: 
published: true
date: 2023-02-15T07:32:35.248Z
tags: 
editor: markdown
dateCreated: 2023-02-15T07:32:27.448Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [027: Implementing microservices with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/027-implementing-microservices-with-nest-js)
{.links-list}


# 使用 Nest.js 实现微服务

微服务是一种流行的架构风格，用于构建可扩展且有弹性的云应用程序。 Nest.js 是一个用于构建高效、可扩展和企业级服务器端应用程序的 Node.js 框架。

在本文中，我们将学习如何使用 Nest.js 实现微服务。我们将从了解微服务是什么以及它们为何有用开始。然后我们将看看如何使用 Nest.js 创建一个简单的微服务。最后，我们将学习如何将微服务部署到云平台。

## 什么是微服务？

微服务是一种软件架构风格，其中应用程序构建为一组小型、独立的服务。每个服务都有单一的职责，可以独立部署和扩展。

与传统的整体架构相比，微服务具有许多优势。它们更易于开发、部署和扩展。它们也更具弹性，因为一项服务的故障不会影响其他服务。

## 使用 Nest.js 创建微服务

现在我们已经了解了什么是微服务，让我们学习如何使用 Nest.js 创建一个简单的微服务。

Nest.js 是一个用于构建高效、可扩展和企业级服务器端应用程序的 Node.js 框架。它使用 TypeScript，它是 JavaScript 的超集，提供静态类型检查和其他好处。

要创建 Nest.js 微服务，我们将使用 Nest CLI。 Nest CLI 是一个命令行界面，可以轻松创建、构建和测试 Nest.js 应用程序。

首先，我们将为我们的微服务创建一个新目录：

```
mkdir my-microservice
```

接下来，我们将在我们的目录中初始化一个新的 Nest.js 项目：

```
nest init
```

这将在我们的目录中创建一个名为“package.json”的文件。该文件包含有关我们项目的信息，包括我们需要安装的依赖项。

接下来，我们将为我们的项目安装依赖项：

```
npm install
```

现在我们的项目已经设置好了，我们可以开始编写我们的微服务了。我们将从创建一个名为 `src/app.controller.ts` 的文件开始：

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller()
export class AppController {
  @Get()
  root(): string {
    return 'Hello World!';
  }
}
```

该文件包含一个名为“AppController”的控制器。这个控制器包含一个单一的方法，“root()”，它返回字符串“Hello World!”。

接下来，我们将创建一个名为 src/app.module.ts 的文件：

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';

@Module({
  controllers: [AppController],
})
export class AppModule {}
```

该文件包含一个名为“AppModule”的模块。该模块包含我们的“AppController”。

最后，我们将创建一个名为 src/main.ts 的文件：

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

该文件包含将启动我们的微服务的代码。首先，我们创建一个新的“NestFactory”，这是一个用于创建 Nest.js 应用程序的工厂。然后我们将我们的 AppModule 传递给 NestFactory。最后，我们调用 `listen()` 方法在端口 `3000` 上启动微服务。

现在我们的微服务已经完成，我们可以通过运行以下命令来启动它：

```
npm start
```

然后我们可以在 http://localhost:3000 访问我们的微服务。

## 部署微服务

现在我们已经了解了如何使用 Nest.js 创建微服务，让我们学习如何部署它。

有许多不同的方法来部署微服务。在本文中，我们将学习如何使用 Docker 将我们的微服务部署到云平台。

Docker 是一种工具，可以轻松地在容器中打包、部署和运行应用程序。容器是一个独立的环境，其中包含应用程序运行所需的一切，例如代码、运行时、系统工具和库。

要使用 Docker 将我们的微服务部署到云平台，我们首先需要创建一个“Dockerfile”：

```
FROM node:10.16.0-alpine

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

这个 Dockerfile 包含构建我们的 Docker 镜像的说明。首先，我们指定要使用的“节点”图像。接下来，我们为我们的应用程序创建一个工作目录。然后，我们将 `package.json` 文件复制到我们的工作目录。我们使用此文件为我们的应用程序安装依赖项。

接下来，我们将其余的应用程序代码复制到我们的工作目录中。最后，我们公开端口 3000 并指定容器启动时应运行的命令。

现在我们有了 `Dockerfile`，我们可以构建我们的 Docker 镜像了：

```
docker build -t my-microservice .
```

此命令将创建一个带有“my-microservice”标签的 Docker 镜像。然后我们可以运行我们的 Docker 镜像：

```
docker run -d -p 3000:3000 my-microservice
```

此命令将从我们的“my-microservice”图像启动一个容器。 `-d` 标志指定容器应以分离模式运行。这意味着容器将在后台运行。 `-p` 标志指定我们主机上的端口 `3000` 应该映射到容器中的端口 `3000`。

然后我们可以在 http://localhost:3000 访问我们的微服务。

## 结论

在这篇文章中，我们学习了如何使用 Nest.js 实现微服务。我们已经了解了如何创建一个简单的微服务以及如何使用 Docker 将其部署到云平台。