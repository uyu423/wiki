---
title: Docker 容器简介
description: 
published: true
date: 2023-02-01T13:36:43.044Z
tags: 
editor: markdown
dateCreated: 2023-02-01T13:36:41.590Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [An Introduction to Docker Containers***English** version of this document is available*](/en/Knowledge-base/Docker/an-introduction-to-docker-containers)
{.links-list}



# Docker 容器简介

在本文中，我们将讨论 Docker 容器是什么、它们如何工作，以及与其他虚拟化技术相比它们提供的一些好处。

## 什么是 Docker 容器？

Docker 容器是一种虚拟化技术，允许您打包和隔离应用程序及其依赖项，使其易于在任何平台上部署和运行。

与虚拟机等其他虚拟化技术不同，Docker 容器不需要为每个应用程序配备单独的操作系统。这使它们的重量更轻，启动速度也更快。

## Docker 容器如何工作？

Docker 容器通过使用 Linux 内核对命名空间和控制组 (cgroups) 的内置支持来工作。

命名空间允许您将应用程序与系统的其余部分隔离开来，这样它就好像是系统上运行的唯一应用程序一样。这种隔离是通过为应用程序创建一组单独的资源来实现的，例如进程 ID、网络接口和安装点。

控制组 (cgroup) 允许您限制应用程序可以使用的资源量，例如 CPU 和内存。这确保了一个应用程序不会占用所有资源并使其他应用程序挨饿。

## 为什么使用 Docker 容器？

您可能想要使用 Docker 容器的原因有很多。

Docker 容器比虚拟机重量轻得多，因此它们启动速度更快。这对于开发很重要，您可能希望快速启动一个新容器来测试一些东西。

Docker 容器也是可移植的，因此您可以轻松地将它们从一台服务器移动到另一台服务器。这对于生产很方便，您可能希望将应用程序移动到不同的服务器以进行扩展或冗余。

Docker 容器的另一大好处是它们允许您将应用程序与系统的其余部分隔离开来。这对于安全性很重要，因为它减少了系统的攻击面。

## 如何使用 Docker 容器

现在我们已经看到了 Docker 容器的一些好处，让我们看看如何使用它们。

您首先需要的是 Docker 主机。这是安装了 Docker 守护进程的 Linux 服务器。守护进程是运行容器的进程。

您可以在自己的服务器上安装 Docker 守护程序，也可以使用 Amazon Elastic Container Service (ECS) 或 Google Container Engine (GKE) 等服务。

有了 Docker 主机后，就可以开始创建容器了。每个容器都是从 Docker 映像创建的。映像是一个模板，其中包含运行应用程序所需的文件和软件。

有两种获取 Docker 镜像的方法。第一种是使用 Dockerfile 等工具创建自己的映像。第二种是使用公共存储库，例如 Docker Hub。

一旦有了镜像，就可以使用 Docker 守护进程从中创建容器。 Docker 守护进程将从存储库中拉取镜像、创建容器并启动应用程序。

然后，您可以通过连接到 Docker 主机来访问该应用程序。例如，如果您正在运行 Web 应用程序，您将使用 Web 浏览器连接到主机的 IP 地址。

## 结论

Docker 容器是一种虚拟化技术，与其他虚拟化技术（例如虚拟机）相比具有许多优势。

Docker 容器重量更轻，因此它们启动速度更快。它们也是便携式的，因此您可以轻松地将它们从一台服务器移动到另一台服务器。

Docker 容器的另一大好处是它们允许您将应用程序与系统的其余部分隔离开来。这对于安全性很重要，因为它减少了系统的攻击面。

如果您正在寻找一种虚拟化应用程序的方法，Docker 容器是一个不错的选择。