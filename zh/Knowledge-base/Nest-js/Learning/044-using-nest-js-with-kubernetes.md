---
title: 044：将 Nest.js 与 Kubernetes 结合使用
description: 
published: true
date: 2023-02-15T16:33:14.864Z
tags: 
editor: markdown
dateCreated: 2023-02-15T16:33:13.075Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [044: Using Nest.js with Kubernetes***English** document is available*](/en/Knowledge-base/Nest-js/Learning/044-using-nest-js-with-kubernetes)
{.links-list}


# 在 Kubernetes 中使用 Nest.js

Kubernetes 是一个强大的容器编排工具，Nest.js 是一个流行的 Node.js 框架。在这篇文章中，我们将向您展示如何将 Nest.js 与 Kubernetes 结合使用。

## 先决条件

- 一个 Kubernetes 集群
- 文本编辑器

## 安装 Nest.js

首先，我们需要安装 Nest.js。我们可以使用 Node.js 包管理器 npm 来做到这一点：

```
npm install -g @nestjs/cli
```

## 创建一个 Nest.js 项目

安装 Nest.js 后，我们可以使用 Nest.js CLI 创建一个新项目：

```
nest new project-name
```

## 运行一个 Nest.js 项目

我们可以使用以下命令运行我们的 Nest.js 项目：

```
npm run start
```

## 将 Nest.js 项目部署到 Kubernetes

我们可以使用 kubectl 命令行工具将 Nest.js 项目部署到 Kubernetes。

首先，我们需要创建一个名为“nest-deployment.yaml”的文件，其中包含以下内容：

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nest-deployment
spec:
  selector:
    matchLabels:
      app: nest
  replicas: 2
  template:
    metadata:
      labels:
        app: nest
    spec:
      containers:
      - name: nest
        image: YOUR_DOCKER_HUB_USERNAME/nest
        ports:
        - containerPort: 8080
```

将 `YOUR_DOCKER_HUB_USERNAME` 替换为您的 Docker Hub 用户名。

接下来，我们需要构建我们的 Nest.js 项目并将其推送到 Docker Hub：

```
docker build -t YOUR_DOCKER_HUB_USERNAME/nest .
docker push YOUR_DOCKER_HUB_USERNAME/nest
```

最后，我们可以将我们的 Nest.js 项目部署到 Kubernetes：

```
kubectl apply -f nest-deployment.yaml
```

## 访问 Nest.js 应用程序

我们可以通过 Kubernetes 集群 IP 地址访问我们的 Nest.js 应用程序：

```
http://CLUSTER_IP:8080
```

将 `CLUSTER_IP` 替换为您的 Kubernetes 集群的 IP 地址。

## 结论

在这篇文章中，我们向您展示了如何将 Nest.js 与 Kubernetes 结合使用。我们已经安装了 Nest.js，创建了一个新项目，并将其部署到 Kubernetes。我们还向您展示了如何通过 Kubernetes 集群 IP 地址访问您的 Nest.js 应用程序。