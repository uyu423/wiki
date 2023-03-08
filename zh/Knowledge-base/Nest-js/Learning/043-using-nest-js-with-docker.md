---
title: 043：将 Nest.js 与 Docker 结合使用
description: 
published: true
date: 2023-02-15T14:32:51.932Z
tags: 
editor: markdown
dateCreated: 2023-02-15T14:32:50.208Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [043: Using Nest.js with Docker***English** document is available*](/en/Knowledge-base/Nest-js/Learning/043-using-nest-js-with-docker)
{.links-list}


# 在 Docker 中使用 Nest.js

Docker 是开发和部署 Web 应用程序的绝佳工具。它允许您将应用程序打包到一个易于部署和管理的独立环境中。

Nest.js 是一个用于构建高效、可扩展的 Node.js 服务器端应用程序的框架。它使用现代 JavaScript，使用 TypeScript（为 JavaScript 带来静态类型检查）构建，并结合了面向对象编程和函数式编程的元素。

在本文中，我们将学习如何将 Nest.js 与 Docker 结合使用。我们将从创建一个简单的 Nest.js 应用程序开始，然后使用 Docker 将其容器化。我们还将学习如何使用 Docker Compose 来管理应用程序的依赖项。

## 创建一个 Nest.js 应用程序

让我们从创建一个简单的 Nest.js 应用程序开始。我们将我们的应用程序称为“todo-list”。

首先，我们需要安装 Nest.js CLI。我们可以使用 npm 来做到这一点：

```
npm install -g @nestjs/cli
```

安装 Nest.js CLI 后，我们可以使用以下命令创建我们的应用程序：

```
nest new todo-list
```

这将创建一个名为“todo-list”的新目录，并为我们的 Nest.js 应用程序生成基本脚手架。

接下来，我们需要为我们的应用程序安装依赖项。我们可以使用 npm 来做到这一点：

```
cd todo-list
npm install
```

现在我们的应用程序的依赖项已安装，我们可以使用以下命令启动应用程序：

```
npm start
```

这将在端口 3000 上启动应用程序。我们可以通过导航到 http://localhost:3000 在浏览器中查看应用程序。

## 容器化我们的应用程序

现在我们已经启动并运行了一个基本的 Nest.js 应用程序，让我们使用 Docker 将其容器化。

首先，我们需要在应用程序的根目录中创建一个名为“Dockerfile”的文件。该文件将包含构建 Docker 映像的说明。

我们的 Dockerfile 将从以下行开始：

```
FROM node:10-alpine
```

此行指定我们要使用 Node.js 10 Alpine 映像作为 Docker 映像的基础映像。 Alpine 是一个轻量级的 Linux 发行版，非常适合用作我们应用程序的基础映像。

接下来，我们需要将应用程序的文件复制到图像中。我们可以使用 COPY 命令来做到这一点：

```
COPY . .
```

这会将当前目录中的所有文件复制到图像中。

现在我们的文件已被复制，我们需要安装应用程序的依赖项。我们可以使用 npm 命令来做到这一点：

```
RUN npm install
```

最后，我们需要指定将用于启动应用程序的命令。我们可以使用 CMD 命令来做到这一点：

```
CMD ["npm", "start"]
```

这将在容器启动时启动我们的应用程序。

我们的 Dockerfile 现已完成。我们可以使用以下命令构建我们的 Docker 镜像：

```
docker build -t todo-list .
```

这将使用我们的 Dockerfile 中的说明构建一个名为“todo-list”的图像。

构建镜像后，我们可以使用以下命令运行它：

```
docker run -d -p 3000:3000 todo-list
```

这将基于我们的“todo-list”图像启动一个容器，并将容器上的端口 3000 映射到我们主机上的端口 3000。

我们现在可以通过导航到 http://localhost:3000 在浏览器中查看我们的应用程序。

## 使用 Docker 组合

Docker Compose 是一个用于定义和运行多容器 Docker 应用程序的工具。它允许您在单个文件中指定应用程序的依赖项，然后使用单个命令启动所有容器。

让我们在应用程序的根目录中创建一个“docker-compose.yml”文件。该文件将包含使用 Docker Compose 运行我们的应用程序的说明。

我们的 docker-compose.yml 文件将以以下行开头：

```
version: '3'
```

此行指定我们使用的是 Docker Compose 文件格式的版本 3。

接下来，我们需要指定我们的应用程序所依赖的服务。我们可以使用“服务”键来做到这一点：

```
services:
  todo-list:
    image: todo-list
    ports:
      - "3000:3000"
```

这定义了一个名为“todo-list”的服务，它使用“todo-list”图像并将容器上的端口 3000 映射到我们主机上的端口 3000。

现在我们的 docker-compose.yml 文件已经完成，我们可以使用以下命令启动我们的应用程序：

```
docker-compose up
```

这将启动我们的 docker-compose.yml 文件中定义的所有容器。

我们现在可以通过导航到 http://localhost:3000 在浏览器中查看我们的应用程序。

## 结论

在这篇文章中，我们学习了如何将 Nest.js 与 Docker 结合使用。我们首先创建一个简单的 Nest.js 应用程序，然后使用 Docker 将其容器化。我们还学习了如何使用 Docker Compose 来管理应用程序的依赖项。