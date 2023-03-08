---
title: Azure 上的 Kubernetes：在 Microsoft Azure 上部署集群
description: 
published: true
date: 2023-02-01T16:18:02.250Z
tags: 
editor: markdown
dateCreated: 2023-02-01T16:17:58.197Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Kubernetes on Azure: Deploying Clusters on Microsoft Azure***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-azure-deploying-clusters-on-microsoft-azure)
{.links-list}


# Azure 上的 Kubernetes：在 Microsoft Azure 上部署集群

Kubernetes 是一个开源系统，用于自动部署、扩展和管理容器化应用程序。它将构成应用程序的容器分组为逻辑单元，以便于管理和发现。 Microsoft Azure 提供了一种称为 Azure Kubernetes 服务 (AKS) 的托管 Kubernetes 服务，可以快速轻松地在 Azure 中部署生产就绪的 Kubernetes 集群。

在本文中，我们将向您展示如何使用 AKS 在 Azure 上部署 Kubernetes 集群。我们还将向您展示如何将简单的应用程序部署到集群并将其公开到 Internet。

##先决条件

在开始之前，您需要具备以下条件：

- 一个 Azure 帐户。如果您没有，可以注册免费试用。
- 安装在本地计算机上的 Azure CLI。
- kubectl 命令行工具。

## 创建 AKS 集群

第一步是使用 Azure CLI 创建 AKS 群集。我们将使用 az aks create 命令创建一个资源组、一个 AKS 集群，并生成一个 kubeconfig 文件。 kubeconfig 文件由 kubectl 工具用于连接到 Kubernetes 集群。

运行以下命令创建 AKS 群集：

```
az aks create \
  --resource-group myResourceGroup \
  --name myAKSCluster \
  --node-count 3 \
  --generate-ssh-keys
```

创建 AKS 群集需要几分钟时间。准备就绪后，您可以使用 kubectl 工具连接到集群。

## 连接到集群

要连接到 AKS 集群，您需要从 Azure 检索集群凭据并配置 kubectl 以使用它们。

运行以下命令以检索凭据：

```
az aks get-credentials \
  --resource-group myResourceGroup \
  --name myAKSCluster
```

这将下载一个 kubeconfig 文件并将其与您机器上现有的 kubeconfig 文件合并。

现在可以使用 kubectl 工具与 AKS 群集进行交互。运行以下命令以获取集群中的节点列表：

```
kubectl get nodes
```

## 部署应用程序

现在我们有了一个工作的 Kubernetes 集群，我们可以向它部署一个应用程序。对于此示例，我们将部署一个用 Node.js 编写的简单 Web 应用程序。

首先，我们需要创建应用程序的 Docker 镜像。我们将使用项目根目录中的 Dockerfile 来构建镜像。运行以下命令来构建图像：

```
docker build -t my-app:v1 .
```

构建镜像后，我们可以将其推送到 Docker 注册表。对于此示例，我们会将其推送到 Azure 容器注册表 (ACR)。

首先，我们需要创建一个 ACR 实例。我们可以使用 az acr create 命令来执行此操作。运行以下命令创建 ACR 实例：

```
az acr create \
  --resource-group myResourceGroup \
  --name myACR \
  --sku Basic
```

一旦创建了 ACR 实例，我们就可以将 Docker 镜像推送到它。执行以下命令推送镜像：

```
docker push myacr.azurecr.io/my-app:v1
```

现在映像已推送到 ACR，我们可以将其部署到我们的 AKS 集群。我们将使用 Kubernetes 部署来执行此操作。部署是管理一组 pod 副本的资源。 Pod 是 Kubernetes 中的基本部署单元。它是一组部署在同一主机上的一个或多个容器。

我们将使用 kubectl 工具来创建部署。运行以下命令以创建部署：

```
kubectl create deployment my-app --image=myacr.azurecr.io/my-app:v1
```

这将创建一个名为 my-app 的部署，该部署将管理一组副本。 Pod 将从我们推送到 ACR 的 my-app:v1 镜像创建。

我们可以使用 kubectl get deployments 命令来查看我们刚刚创建的部署：

```
kubectl get deployments
```

我们还可以使用 kubectl get pods 命令查看部署管理的 pod：

```
kubectl get pods
```

## 公开应用程序

现在我们的应用程序已部署，我们需要将其公开到 Internet 以便用户可以访问它。我们可以通过创建 Kubernetes 服务来做到这一点。服务是一种抽象，它定义了一组逻辑 pod 和访问它们的策略。

我们将创建一个 LoadBalancer 类型的服务。这将在 Azure 中创建一个负载均衡器并将其映射到由 my-app 部署管理的 pod。

运行以下命令以创建服务：

```
kubectl expose deployment my-app --type=LoadBalancer --port=80 --target-port=8080
```

这将创建一个名为 my-app 的服务，该服务在负载均衡器上公开端口 80。到此端口的流量将转发到由 my-app 部署管理的 pod 上的端口 8080。

我们可以使用 kubectl get services 命令来查看我们刚刚创建的服务：

```
kubectl get services
```

创建服务后，需要几分钟时间来配置负载均衡器并为服务分配公共 IP 地址。您可以使用 kubectl get services 命令查看服务的状态：

```
kubectl get services
```

创建服务后，您可以使用公共 IP 地址在 Web 浏览器中访问应用程序。

## 删除集群

如果不再需要 AKS 群集，可以将其删除以停止产生费用。要删除集群，请运行以下命令：

```
az aks delete \
  --resource-group myResourceGroup \
  --name myAKSCluster
```

## 结论

在本文中，我们向您展示了如何使用 AKS 在 Azure 上部署 Kubernetes 集群。我们还向您展示了如何将一个简单的应用程序部署到集群并将其公开到 Internet。