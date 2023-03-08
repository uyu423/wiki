---
title: 075：使用 Node.js 在 Kubernetes 上部署 TensorFlow.js 应用程序
description: 
published: true
date: 2023-02-03T00:17:49.268Z
tags: 
editor: markdown
dateCreated: 2023-02-03T00:17:44.588Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [075: Deploying TensorFlow.js Applications on Kubernetes with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/075-deploying-tensorflow-js-applications-on-kubernetes-with-node-js)
{.links-list}


# 075：使用 Node.js 在 Kubernetes 上部署 TensorFlow.js 应用程序

TensorFlow.js 是一个强大的 JavaScript 机器学习工具，而 Node.js 是服务器端 JavaScript 应用程序的流行运行时。在本文中，我们将向您展示如何在流行的容器编排平台 Kubernetes 上部署 TensorFlow.js 应用程序。

Kubernetes 是大规模部署容器化应用程序的绝佳平台。它提供了自动缩放、负载平衡和滚动更新等功能，这在管理大型应用程序时非常有用。

Node.js 是服务器端 JavaScript 应用程序的流行运行时。它速度很快，并且拥有庞大的库和工具生态系统。

TensorFlow.js 是一个强大的 JavaScript 机器学习工具。它允许您在浏览器或 Node.js 中训练和部署模型。

在 Kubernetes 上部署 TensorFlow.js 应用程序是提高应用程序可用性和性能的好方法。 Kubernetes 可以提供自动缩放和负载平衡等功能，这在管理大型应用程序时可以提供很大的帮助。

在本文中，我们将向您展示如何在 Kubernetes 上部署 TensorFlow.js 应用程序。我们假设您对 Kubernetes 和 TensorFlow.js 有基本的了解。如果您是 Kubernetes 的新手，可以查看我们的 Kubernetes 101 帖子。

## 先决条件

在开始之前，您需要具备以下条件：

- 一个 Kubernetes 集群。如果您没有，可以查看我们关于如何创建 Kubernetes 集群的指南。
- TensorFlow.js 应用程序。如果您没有，可以查看我们关于如何创建 TensorFlow.js 应用程序的指南。

## 部署应用程序

拥有 Kubernetes 集群和 TensorFlow.js 应用程序后，您可以在 Kubernetes 上部署该应用程序。

我们假设您对 Kubernetes 和 TensorFlow.js 有基本的了解。如果您是 Kubernetes 的新手，可以查看我们的 Kubernetes 101 帖子。

要部署该应用程序，您需要创建一个 Kubernetes 部署。 Deployment 是一个 Kubernetes 对象，它描述了一组 pod 的期望状态。

要创建 Deployment，您需要创建一个描述 Deployment 的 YAML 文件。下面是一个示例 YAML 文件，它描述了 TensorFlow.js 应用程序的部署：

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tfjs-deployment
spec:
  selector:
    matchLabels:
      app: tfjs-app
  replicas: 1
  template:
    metadata:
      labels:
        app: tfjs-app
    spec:
      containers:
      - name: tfjs-container
        image: <your-docker-image>
        ports:
        - containerPort: 3000
```

在 YAML 文件中，您需要指定容器的图像。这应该是您的 TensorFlow.js 应用程序的图像。

拥有 YAML 文件后，您可以通过运行以下命令来创建 Deployment：

```
kubectl apply -f <your-yaml-file>
```

这将在您的 Kubernetes 集群中创建一个 Deployment。 Deployment 将创建一个运行 TensorFlow.js 应用程序的 pod。

## 访问应用程序

创建 Deployment 后，您可以通过创建 Service 来访问应用程序。 Service 是一个 Kubernetes 对象，它提供了一种访问一组 pod 的方法。

要创建服务，您需要创建一个描述该服务的 YAML 文件。下面是一个 YAML 文件示例，它描述了 TensorFlow.js 应用程序的服务：

```yaml
apiVersion: v1
kind: Service
metadata:
  name: tfjs-service
spec:
  type: LoadBalancer
  selector:
    app: tfjs-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 3000
```

在 YAML 文件中，您需要指定服务的选择器。这应该与 Deployment 的标签选择器相匹配。

拥有 YAML 文件后，您可以通过运行以下命令来创建服务：

```
kubectl apply -f <your-yaml-file>
```

这将在您的 Kubernetes 集群中创建一个服务。该服务将提供一种方法来访问运行 TensorFlow.js 应用程序的 pod。

## 删除部署

完成 Deployment 后，您可以通过运行以下命令将其删除：

```
kubectl delete deployment tfjs-deployment
```

这将删除 Deployment 及其创建的 pod。