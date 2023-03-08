---
title: 使用 Kubernetes 和 Docker 部署后端应用程序
description: 
published: true
date: 2023-02-01T04:36:56.738Z
tags: 
editor: markdown
dateCreated: 2023-02-01T04:36:55.110Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Deploying Backend Applications with Kubernetes and Docker***English** version of this document is available*](/en/Knowledge-base/Backend/deploying-backend-applications-with-kubernetes-and-docker)
{.links-list}



# 使用 Kubernetes 和 Docker 部署后端应用程序

在本文中，我们将介绍如何使用 Kubernetes 和 Docker 部署后端应用程序。我们将首先了解这些技术是什么以及它们如何协同工作。然后，我们将提供有关如何设置 Kubernetes 集群并向其部署应用程序的分步指南。

## 什么是 Kubernetes？

Kubernetes 是一个容器编排平台，使开发人员能够大规模部署和管理容器化应用程序。 Kubernetes 自动执行容器化应用程序的配置、扩展和监控。它还提供了一种声明式配置模型，可以轻松部署和管理复杂的应用程序。

## 什么是 Docker？

Docker 是一个容器化平台，使开发人员能够在隔离环境中打包和部署应用程序。 Docker 容器为应用程序提供轻量级、可移植和独立的环境。它们易于部署，可以在任何支持 Docker 的平台上运行。

## Kubernetes 和 Docker 如何协同工作？

Kubernetes 和 Docker 协同工作，为部署和管理容器化应用程序提供了一个平台。 Kubernetes 自动执行 Docker 容器的配置、扩展和监控。它还提供了一种声明式配置模型，可以轻松部署和管理复杂的应用程序。

## 设置 Kubernetes 集群

在本节中，我们将介绍如何设置 Kubernetes 集群。我们将使用 Kubernetes 命令行工具 kubectl 来设置我们的集群。

首先，我们需要安装 kubectl。我们可以用 curl 做到这一点：

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
```

接下来，我们需要使 kubectl 二进制文件可执行：

```
chmod +x ./kubectl
```

最后，我们可以将 kubectl 二进制文件移动到我们的 PATH：

```
sudo mv ./kubectl /usr/local/bin/kubectl
```

现在我们已经安装了 kubectl，我们可以使用它来设置我们的 Kubernetes 集群。我们将使用 Minikube，这是一个在单个节点上运行的 Kubernetes 实现。

首先，我们需要安装 Minikube。我们可以用 curl 做到这一点：

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

接下来，我们需要使 Minikube 二进制文件可执行：

```
chmod +x minikube
```

最后，我们可以将 Minikube 二进制文件移动到我们的路径：

```
sudo mv minikube /usr/local/bin/
```

现在我们已经安装了 Minikube，我们可以使用它来设置我们的 Kubernetes 集群。要启动 Minikube 集群，请运行以下命令：

```
minikube start
```

这将启动一个只有一个节点的 Minikube 集群。

## 将应用程序部署到 Kubernetes

在本节中，我们将介绍如何将应用程序部署到 Kubernetes。我们将使用一个简单的 Node.js 应用程序作为示例。

首先，我们需要为我们的应用程序创建一个 Dockerfile。 Dockerfile 是一个文本文件，其中包含构建 Docker 映像的说明。

我们的 Dockerfile 将如下所示：

```
FROM node:8

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

此 Dockerfile 将使用 node:8 Docker 镜像作为基础镜像。然后它将 package.json 和 package-lock.json 文件从我们的项目复制到 /app 目录中。接下来，它将运行 npm install 来安装我们的依赖项。最后，它将我们项目文件的其余部分复制到 /app 目录并公开端口 3000。

现在我们有了 Dockerfile，我们可以构建我们的 Docker 镜像。我们将我们的图像命名为 my-app：

```
docker build -t my-app .
```

这将构建一个名为 my-app 的 Docker 镜像。

现在我们有了 Docker 镜像，我们可以将它推送到 Docker 注册表。我们将使用 Docker Hub 作为我们的注册表。

首先，我们需要创建一个 Docker Hub 帐户。然后，我们需要登录到我们的 Docker Hub 帐户：

```
docker login
```

接下来，我们需要用我们的 Docker Hub 用户名标记我们的 Docker 镜像：

```
docker tag my-app <your-docker-hub-username>/my-app
```

最后，我们可以将我们的 Docker 镜像推送到 Docker Hub：

```
docker push <your-docker-hub-username>/my-app
```

现在我们的 Docker 镜像在 Docker Hub 上，我们可以将它部署到我们的 Kubernetes 集群。

首先，我们需要创建部署。部署是管理一组副本的 Kubernetes 对象。副本是 Kubernetes 将在我们的节点上运行的应用程序的副本。

要创建部署，请运行以下命令：

```
kubectl create deployment my-app --image=<your-docker-hub-username>/my-app
```

这将创建一个名为 my-app 的部署。 --image 标志指定我们的部署将使用的 Docker 映像。

接下来，我们需要创建一个服务。服务是将我们的应用程序暴露给外界的 Kubernetes 对象。

要创建服务，请运行以下命令：

```
kubectl expose deployment my-app --type=LoadBalancer --port=80 --target-port=3000
```

这将创建一个名为 my-app 的服务。 --type 标志指定服务类型。 --port 标志指定我们的服务将使用的端口。 --target-port 标志指定我们的应用程序运行的端口。

最后，我们可以获得服务的 URL：

```
kubectl get service my-app
```

这将输出我们服务的 URL。我们现在可以通过此 URL 访问我们的应用程序。

## 结论

在本文中，我们介绍了如何使用 Kubernetes 和 Docker 部署后端应用程序。我们首先了解了这些技术是什么以及它们如何协同工作。然后，我们提供了有关如何设置 Kubernetes 集群并向其部署应用程序的分步指南。