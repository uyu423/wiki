---
title: Docker 镜像管理：标记和推送到注册表
description: 
published: true
date: 2023-02-01T21:43:22.575Z
tags: 
editor: markdown
dateCreated: 2023-02-01T21:43:18.417Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Docker Image Management: Tagging and Pushing to a Registry***English** document is available*](/en/Knowledge-base/Docker/docker-image-management-tagging-and-pushing-to-a-registry)
{.links-list}



# Docker 镜像管理：标记和推送到注册表

Docker 镜像是创建容器的基础。默认情况下，图像是从 Docker Hub 中提取的，这是一个由 Docker, Inc. 管理的公共注册表。但是，您也可以运行自己的注册表，并将图像推送到它。

本文介绍了两种管理 Docker 镜像的方法：标记和推送到注册表。

## 标记图像

您可以使用 `docker tag` 标记图像。例如，这对于用版本号标记图像很有用。要标记图像，请使用以下语法：

```
docker tag <image> <tag>
```

例如，要使用标签“1.7.9”标记图像“nginx”，您将运行以下命令：

```
docker tag nginx 1.7.9
```

标记对于管理图像很重要，因为它允许您在运行容器时指定图像的特定版本。默认情况下，使用 `latest` 标签，它对应于图像的最新版本。

## 将图像推送到注册表

标记图像后，您可以将其推送到注册表。您可以使用 `docker push` 命令将图像推送到注册表。该命令的语法如下：

```
docker push <registry>/<repository>/<image>
```

例如，要将镜像 `nginx` 推送到 Docker Hub，您可以使用以下命令：

```
docker push nginx
```

将图像推送到注册表是一种与他人共享图像的方式。通过将图像推送到注册表，您可以让其他人提取和使用它。

## 概括

在本文中，您了解了两种管理 Docker 映像的方法：标记和推送到注册表。标记图像是一种用版本号或其他信息标记它们的方法。将图像推送到注册表是与他人共享它们的一种方式。