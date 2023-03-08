---
title: Dockerfile 最佳实践：创建可靠的 Docker 镜像
description: 
published: true
date: 2023-02-15T23:32:48.918Z
tags: 
editor: markdown
dateCreated: 2023-02-15T23:32:47.219Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Dockerfile Best Practices: Creating Reliable Docker Images***English** document is available*](/en/Knowledge-base/Docker/dockerfile-best-practices-creating-reliable-docker-images)
{.links-list}


# Dockerfile 最佳实践：创建可靠的 Docker 镜像

Dockerfiles 是使用 Docker 的基本部分。它们允许您创建自己的图像，这些图像可用于创建新容器。精心设计的 Dockerfile 可以让您轻松创建、维护和更新镜像，从长远来看可以节省您大量的时间和精力。

本文将提供一些创建可靠的 Docker 镜像的最佳实践，目的是让 Docker 用户的生活更轻松。

## 使用.dockerignore

.dockerignore 文件用于指定应从图像中排除的文件和目录。这对于排除图像中不需要的文件很有用，例如临时文件或构建工件。

要创建 .dockerignore 文件，只需在项目的根目录中创建一个名为“.dockerignore”的文件，然后添加每个你希望排除的文件或目录，每行一个。例如：

```
.dockerignore

# Exclude all temporary files
*.tmp

# Exclude all build artifacts
build/
```

## 保持你的 Dockerfile 简单

简单的 Dockerfile 比复杂的更容易理解和维护。它也更有可能与未来版本的 Docker 兼容。

保持 Dockerfile 简单的一种方法是避免使用复杂的 shell 命令。如果可能，使用现有的 docker 镜像作为您自己的镜像的基础，并使用 apt 或 yum 等包管理器安装必要的软件。

保持 Dockerfile 简单的另一种方法是避免安装不必要的软件。如果您只是将图像用于特定目的，则无需安装带有文本编辑器、Web 浏览器等的完整操作系统。

## 为你的基础镜像使用一个特定的标签

使用来自 Docker 注册表的基础映像时，请始终指定特定标签，而不是使用“最新”标签。 “最新”标签经常被开发人员用来表示图像的最新开发版本，这可能不适合生产使用。

## 使用单个 RUN 指令

如果可能，请在 Dockerfile 中使用单个 RUN 指令而不是多个指令。这将使您的图像更容易构建，并减少图像中的层数，这对性能很重要。

要使用单个 RUN 指令，只需将您希望运行的所有命令组合成一行，并用 && 分隔。例如：

```
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:my-ppa && \
    apt-get update && \
    apt-get install -y my-software
```

## 使用特定用户

默认情况下，容器以 root 用户身份运行。这可能存在安全风险，因为在容器中运行的任何进程都可以完全访问主机。

为避免这种情况，您可以在 Dockerfile 中创建一个新用户，并使用该用户在容器中运行任何进程。例如：

```
# Create a new user
RUN useradd -ms /bin/bash myuser

# Use the new user for all subsequent commands
USER myuser
```

## 使用特定的工作目录

创建容器时，会为其指定一个默认工作目录。可以使用 Dockerfile 中的 WORKDIR 指令覆盖此目录。

指定一个特定的工作目录是个好主意，因为它可以更容易地在容器中查找文件，并有助于不同机器之间的可移植性。例如：

```
# Set the working directory to /app
WORKDIR /app
```

## 避免使用 ADD 和 COPY

ADD 和 COPY 指令很相似，但它们之间有一些重要的区别。 ADD 可用于从远程 URL 中提取文件，而 COPY 只能用于从构建上下文中复制文件。

ADD 也比 COPY 更强大，因为它可以自动解决文件之间的依赖关系。例如，如果您添加一个 .tar.gz 文件，ADD 将自动从存档中提取文件。

由于这些差异，通常建议在 Dockerfile 中使用 COPY 而不是 ADD。

## 指定健康检查

健康检查是一种测试，用于确定容器是否健康并且应该继续运行。如果健康检查失败，容器将停止并重新启动。

可以使用 Dockerfile 中的 HEALTHCHECK 指令指定健康检查。例如：

```
# Check that the container is healthy every 30 seconds
# and that the HTTP service is responding on port 80
HEALTHCHECK --interval=30s --timeout=5s \
    CMD wget -qO- http://localhost:80/ || exit 1
```

## 使用多阶段构建

多阶段构建是 Docker 的一项功能，它允许您在单个构建过程中创建多个图像。这对于创建更小、更安全的图像很有用，因为您可以在构建图像后从图像中删除不需要的文件。

要使用多阶段构建，只需在 Dockerfile 中创建多个 FROM 指令，每个指令具有不同的图像名称。例如：

```
# Build stage
FROM golang:1.8 as builder

WORKDIR /src

COPY . .

RUN go build -o app

# Run stage
FROM alpine:latest

WORKDIR /app

COPY --from=builder /src/app .

CMD ["./app"]
```

## 结论

通过遵循本文中描述的最佳实践，您可以使您的 Dockerfile 更可靠、更易于理解和维护。从长远来看，这将为您节省时间和精力，并使您作为 Docker 用户的生活更加轻松。