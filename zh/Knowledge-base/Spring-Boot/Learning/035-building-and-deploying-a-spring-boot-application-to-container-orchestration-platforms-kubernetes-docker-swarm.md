---
title: 035：构建 Spring Boot 应用程序并将其部署到容器编排平台（Kubernetes、Docker Swarm）
description: 
published: true
date: 2023-02-04T03:32:43.466Z
tags: 
editor: markdown
dateCreated: 2023-02-04T03:32:38.112Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [035: Building and deploying a Spring Boot application to container orchestration platforms (Kubernetes, Docker Swarm)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/035-building-and-deploying-a-spring-boot-application-to-container-orchestration-platforms-kubernetes-docker-swarm)
{.links-list}


# 035：构建 Spring Boot 应用程序并将其部署到容器编排平台（Kubernetes、Docker Swarm）

Spring Boot 是一种流行的基于 Java 的框架，用于开发微服务。在本文中，我们将学习如何将 Spring Boot 应用程序容器化并将其部署到 Kubernetes 和 Docker Swarm。

## 将 Spring Boot 应用程序容器化

要容器化 Spring Boot 应用程序，我们首先需要创建一个 `Dockerfile`。 `Dockerfile` 是一个文本文件，其中包含构建 Docker 映像的说明。

我们将从在 Spring Boot 项目的根目录中创建一个 `Dockerfile` 开始。

```
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG JAR_FILE
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```

在这个 Dockerfile 中，我们使用 openjdk:8-jdk-alpine 作为我们的基础镜像。我们还使用 `VOLUME` 来创建用于存储临时文件的挂载点。

接下来，我们将 Spring Boot `.jar` 文件作为 `app.jar` 复制到容器中，并将其设置为 `ENTRYPOINT`。

现在我们有了 `Dockerfile`，我们可以构建我们的 Docker 镜像了。我们将使用 `docker build` 命令来构建我们的镜像，并使用 `latest` 标签对其进行标记。

```
$ docker build -t my-spring-boot-app:latest .
```

## 部署到 Kubernetes

Kubernetes 是一个流行的容器编排平台。它可用于将一组容器作为一个单元进行管理。

要将我们的 Spring Boot 应用程序部署到 Kubernetes，我们首先需要创建一个“Deployment”。 `Deployment` 定义了一组相同的 pod，并确保其中一定数量的 pod 始终运行。

我们将在项目的根目录中创建一个“deployment.yaml”文件。

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-spring-boot-app
  labels:
    app: my-spring-boot-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-spring-boot-app
  template:
    metadata:
      labels:
        app: my-spring-boot-app
    spec:
      containers:
      - name: my-spring-boot-app
        image: my-spring-boot-app:latest
        ports:
        - containerPort: 8080
```

在这个文件中，我们定义了一个副本数为 3 的“Deployment”。我们还定义了一个“selector”和“template”，它们指定了“Deployment”将管理的 pod。

现在，我们可以使用 `kubectl` 命令行工具在 Kubernetes 中创建我们的 `Deployment`。

```
$ kubectl apply -f deployment.yaml
```

## 部署到 Docker Swarm

Docker Swarm 是 Docker 的容器编排平台。它可用于将一组 Docker 容器作为一个单元进行管理。

要将我们的 Spring Boot 应用程序部署到 Docker Swarm，我们首先需要创建一个“Stack”。 “堆栈”是一组部署在一起的服务。

我们将在项目的根目录中创建一个 `stack.yaml` 文件。

```yaml
version: "3.1"

services:

  my-spring-boot-app:
    image: my-spring-boot-app:latest
    ports:
      - "8080:8080"
    deploy:
      replicas: 3
```

在这个文件中，我们定义了一个带有单一服务的 `Stack`，`my-spring-boot-app`。我们还指定要部署此服务的 3 个副本。

现在，我们可以使用 docker stack 命令将 `Stack` 部署到 Docker Swarm。

```
$ docker stack deploy -c stack.yaml my-spring-boot-app
```

## 附加信息

- 如果您使用的是 Kubernetes，您还可以创建一个“服务”来将您的应用程序暴露给外界。
- 如果您使用的是 Docker Swarm，您还可以创建一个“网络”以允许您的服务之间进行通信。

## 进一步阅读的资源

- [Spring Boot 参考文档 - 将 Spring Boot 应用程序容器化](https://docs.spring.io/spring-boot/docs/current/reference/html/deploying-spring-boot.html# deploying-spring-boot-containerizing )
- [Kubernetes 文档 - 创建部署](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/# creating-a-deployment)
- [Docker 文档 - 将堆栈部署到 Swarm](https://docs.docker.com/engine/reference/commandline/stack_deploy/# deploy-a-stack-to-a-swarm)