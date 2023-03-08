---
title: Docker Hub：构建和共享您的 Docker 镜像
description: 
published: true
date: 2023-02-14T01:17:24.381Z
tags: 
editor: markdown
dateCreated: 2023-02-14T01:17:17.198Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Docker Hub: Building and Sharing Your Docker Images***English** document is available*](/en/Knowledge-base/Docker/docker-hub-building-and-sharing-your-docker-images)
{.links-list}


# Docker Hub：构建和共享您的 Docker 镜像

Docker Hub 是一个基于云的注册服务，用于构建和共享 Docker 镜像。借助 Docker Hub，您可以轻松构建、测试和部署应用程序。

Docker Hub 提供免费计划和付费专业计划。使用免费计划，您可以创建无限的公共存储库，但仅限于一个私有存储库。使用 Pro 计划，您可以创建无限数量的公共和私人存储库。

将镜像推送到 Docker Hub 有两种方式：

1. **docker push** 命令

2. **Docker Hub 网页界面**

## docker push 命令

**docker push** 命令将图像推送到 Docker 注册表。 Docker 注册表是存储和提供图像的主机。

**docker push** 命令要求您指定镜像名称和标签。例如，要将标签为“latest”的镜像推送到 Docker Hub，您可以使用以下命令：

```
docker push <username>/<image>:<tag>
```

将 <username> 替换为您的 Docker Hub 用户名，将 <image> 替换为图像名称，将 <tag> 替换为标签。

## Docker Hub 网页界面

Docker Hub Web 界面是一个基于 Web 的应用程序，可用于推送、拉取和管理 Docker 映像。

要使用 Web 界面将图像推送到 Docker Hub，请先登录到您的 Docker Hub 帐户。然后，单击 **Create Repository** 按钮。

输入存储库的名称和描述，然后单击 **Create** 按钮。

接下来，单击 **上传文件** 按钮。

选择您要上传的图片，然后单击 **上传** 按钮。

最后，单击 **Publish** 按钮。

您的图像现在已推送到 Docker Hub 上的存储库。

## 结论

Docker Hub 是与世界分享你的 Docker 镜像的好方法。借助 Docker Hub，您可以轻松构建、测试和部署应用程序。