---
title: Node.js 和微服务：构建稳健的架构
description: 
published: true
date: 2023-02-15T06:55:44.718Z
tags: 
editor: markdown
dateCreated: 2023-02-15T06:55:43.122Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Node.js and Microservices: Building a Robust Architecture***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-microservices-building-a-robust-architecture)
{.links-list}


# Node.js 和微服务：构建稳健的架构

在云计算时代，越来越需要可以跨多个服务器部署的应用程序。这就是微服务的用武之地。微服务是一种将应用程序构建为一组可以独立部署和扩展的小型独立服务的方法。

Node.js 是构建微服务的流行平台。它轻巧高效，拥有庞大的库和工具生态系统。

在本文中，我们将了解如何使用 Node.js 构建微服务架构。我们将从一个简单的整体应用程序开始，并将其分解为一组微服务。然后我们将研究如何部署和扩展我们的微服务。

## 单体与微服务

在我们深入研究 Node.js 和微服务之前，让我们退后一步，了解单体架构和微服务架构之间的区别。

单体应用程序是作为单个大型单元构建的应用程序。应用程序的所有组件都紧密耦合并相互依赖。单体应用程序通常作为单个进程部署在单个服务器上。

微服务架构是将应用程序构建为一组小型独立服务的架构。这些服务松散耦合，可以独立部署和扩展。微服务通常部署为一组服务器上的一组小型、独立的进程。

使用微服务架构有几个主要好处：

* **可扩展性**：微服务可以独立部署和扩展，因此很容易根据需要扩展应用程序的特定部分。

* **隔离**：每个微服务都在自己的进程中运行，因此如果一个微服务失败，不会影响其他微服务。

* **灵活性**：微服务可以用不同的编程语言编写并部署在不同的服务器上，因此您可以为工作选择合适的工具。

## 分解单体

现在我们已经看到了微服务的好处，让我们看看如何将单体应用程序分解为一组微服务。

我们的示例单体应用程序是一个简单的待办事项列表。它有一个用于创建和管理待办事项的用户界面，以及一个用于存储数据的后端。后端是一个简单的关系数据库。

第一步是识别应用程序的不同组件。在我们的待办事项列表示例中，我们有几个明显的组成部分：

* 用户界面
* 后台数据库
* 待办事项列表数据

我们可以进一步将这些组件分解成更小的服务。例如，用户界面可以分解为处理 HTML 和 CSS 的前端服务和处理数据的后端服务。

后端数据库可以分解为处理数据的数据库服务和处理文件的存储服务。

待办事项列表数据可以分解为处理待办事项的任务服务和处理用户数据的用户服务。

我们现在拥有一组可以独立部署和扩展的小型独立服务。

## 部署微服务

现在我们有了微服务，让我们看看如何部署它们。

有几种不同的方法来部署微服务。最常见的是使用容器编排器，例如 Docker Swarm 或 Kubernetes。

另一种选择是使用无服务器平台，例如 AWS Lambda 或 Azure Functions。无服务器平台对于没有大量流量或只是偶尔需要的微服务是一个不错的选择。

在我们的待办事项列表示例中，我们将使用 Docker Swarm 部署我们的微服务。我们将创建一个定义我们服务的 docker-compose.yml 文件：

```yaml
version: "3"

services:
  frontend:
    image: frontend:latest
    ports:
      - "80:80"
    deploy:
      replicas: 2
      update_config:
        parallelism: 2
        delay: 10s
  backend:
    image: backend:latest
    ports:
      - "8080:8080"
    deploy:
      replicas: 2
      update_config:
        parallelism: 2
        delay: 10s
  database:
    image: database:latest
    ports:
      - "3306:3306"
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
  storage:
    image: storage:latest
    ports:
      - "9000:9000"
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
  task:
    image: task:latest
    ports:
      - "8081:8081"
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
  user:
    image: user:latest
    ports:
      - "8082:8082"
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
```

然后我们可以使用以下命令部署我们的服务：

```
$ docker stack deploy -c docker-compose.yml todo
```

## 扩展微服务

一旦部署了我们的微服务，我们就可以根据需要扩大或缩小它们。例如，我们可以将前端服务从两个副本扩展到四个副本：

```
$ docker service scale todo_frontend=4
```

我们还可以将后端服务缩小到一个副本：

```
$ docker service scale todo_backend=1
```

## 结论

在本文中，我们了解了如何使用 Node.js 构建微服务架构。我们已经了解了如何将单体式应用程序分解为一组小型的独立服务，以及如何部署和扩展这些服务。

虽然微服务提供了许多好处，但它们也带来了一些挑战。例如，管理一组小型、独立的服务可能很复杂。服务之间的通信会增加应用程序的延迟。

尽管存在这些挑战，微服务仍然是构建可扩展、有弹性的应用程序的强大方式。 Node.js 是构建微服务的绝佳平台。