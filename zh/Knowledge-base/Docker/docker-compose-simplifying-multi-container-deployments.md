---
title: Docker Compose：简化多容器部署
description: 
published: true
date: 2023-02-01T12:57:41.494Z
tags: 
editor: markdown
dateCreated: 2023-02-01T12:57:38.083Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Docker Compose: Simplifying Multi-Container Deployments***English** version of this document is available*](/en/Knowledge-base/Docker/docker-compose-simplifying-multi-container-deployments)
{.links-list}



# Docker Compose：简化多容器部署

Docker Compose 是一个用于定义和运行多容器 Docker 应用程序的工具。使用 Compose，您可以使用 YAML 文件来配置应用程序的服务。然后，使用一个命令，您可以从您的配置中创建并启动所有服务。

使用 Compose 基本上是一个三步过程。

1. 使用 Dockerfile 定义您的应用程序环境，以便它可以在任何地方复制。

2. 在 docker-compose.yml 中定义构成您的应用程序的服务，以便它们可以在隔离环境中一起运行。

3. 运行 docker-compose up，Compose 启动并运行您的整个应用程序。

## 使用 Dockerfile 定义应用程序的环境

Dockerfile 是一个文本文档，其中包含您通常手动执行以构建 Docker 映像的所有命令。

```
FROM node:8

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 8080

CMD [ "npm", "start" ]
```

您需要做的第一件事是指定要用于容器的基础映像。在本例中，我们使用 node:8，这是运行 Node.js 应用程序的流行图像。

接下来，WORKDIR 指令为 Dockerfile 中跟在它后面的任何 RUN、CMD、ENTRYPOINT、COPY 和 ADD 指令设置工作目录。

COPY 指令从 <src> 复制新文件或目录，并将它们添加到图像的文件系统路径 <dest> 中。

RUN 指令将在当前图像之上的新层中执行任何命令并提交结果。生成的提交图像将用于 Dockerfile 中的下一步。

在这种情况下，我们正在运行 npm install 它将安装我们的 package.json 文件中定义的所有依赖项。

副本。 .指令会将我们当前目录中的所有文件复制到容器中。

EXPOSE 指令通知 Docker 容器将在运行时监听指定的网络端口。

CMD 指令有两种形式。 exec 形式（首选形式）和 shell 形式。

exec 形式可以避免 shell 字符串修改，并使用不同的 shell，或者根本不使用 shell。这可以防止执行任何使用 shell 形式的 CMD 或 RUN 指令。

在这种情况下，我们使用 exec 形式，我们指定当容器启动时，它应该执行 npm start 命令。

## 在 docker-compose.yml 中定义构成您的应用程序的服务

现在我们有了 Dockerfile，我们可以在 docker-compose.yml 文件中定义我们的服务。

```
version: '3'

services:
  web:
    build: .
    ports:
     - "8080:8080"
```

在这个文件中，我们定义了一个名为 web 的服务。该服务是使用我们当前目录中的 Dockerfile 构建的。我们将主机上的端口 8080 映射到容器中的端口 8080。

## 运行 docker-compose up 和 Compose 启动并运行你的整个应用程序

现在我们有了 Dockerfile 和 docker-compose.yml 文件，我们可以通过运行 docker-compose up 来启动我们的应用程序。

```
$ docker-compose up
```

此命令将启动我们的 Web 服务并将日志打印到控制台。

## 结论

Docker Compose 是一个很棒的工具，可以简化部署多容器 Docker 应用程序的过程。通过使用 Dockerfile 和 docker-compose.yml 文件，您可以使用单个命令定义和运行整个应用程序。