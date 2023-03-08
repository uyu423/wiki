---
title: Kubernetes 和 Linux 容器编排
description: 
published: true
date: 2023-02-12T03:32:21.441Z
tags: 
editor: markdown
dateCreated: 2023-02-12T03:32:14.467Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes and Linux Container Orchestration***English** document is available*](/en/Knowledge-base/Linux/kubernetes-and-linux-container-orchestration)
{.links-list}


# 什么是 Kubernetes？

Kubernetes 是最初由 Google 设计的开源容器编排平台。它现在由云原生计算基金会维护。它可用于自动化容器化应用程序的部署、扩展和管理。

# 什么是 Linux 容器？

Linux 容器是一个软件包，其中包含在隔离环境中运行应用程序或服务所需的所有组件。容器是虚拟机的替代品，可以提供许多好处，例如提高资源利用率、可移植性和安全性。

# Kubernetes 和 Linux 容器编排

Kubernetes 常用于容器编排，即对多个容器的管理。这可能包括部署、扩展和监控容器等任务。 Linux 容器可以与 Kubernetes 一起使用，以提供轻量级和可移植的应用程序环境。

# 开始使用 Kubernetes

有一些 Kubernetes 安装选项，包括使用托管解决方案或将其安装在您自己的基础设施上。出于开发和测试目的，您还可以使用单节点 Kubernetes 集群，它可以运行在 Docker 等 Linux 容器平台上。

安装 Kubernetes 后，您就可以开始部署应用程序了。为此，您需要创建一个 Kubernetes 部署文件。此文件包含有关您的应用程序的所有必要信息，例如要使用的容器映像、副本数和任何公开的端口。

以下是一个简单 PHP 应用程序的示例部署文件：

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-php-app
  labels:
    app: my-php-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-php-app
  template:
    metadata:
      labels:
        app: my-php-app
    spec:
      containers:
      - name: my-php-app
        image: php:7.2-apache
        ports:
        - containerPort: 80
```

该文件可用于通过运行以下命令来部署应用程序：

```
$ kubectl apply -f my-php-app.yaml
```

# 结论

Kubernetes 是用于管理容器化应用程序的强大工具。它可用于自动化容器的部署、扩展和管理。 Linux 容器可以与 Kubernetes 一起使用，以提供轻量级和可移植的应用程序环境。