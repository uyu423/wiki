---
title: 裸机上的 Kubernetes：在物理服务器上部署集群
description: 
published: true
date: 2023-02-14T08:33:07.814Z
tags: 
editor: markdown
dateCreated: 2023-02-14T08:33:06.021Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes on Bare Metal: Deploying Clusters on Physical Servers***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-bare-metal-deploying-clusters-on-physical-servers)
{.links-list}


# Kubernetes on Bare Metal：在物理服务器上部署集群

如今，越来越多地使用容器来打包和部署应用程序。这是因为与传统虚拟机相比，容器具有许多优势，例如更便携、占用空间更小以及启动速度更快。

Kubernetes 是一种流行的容器编排工具，可用于管理大量容器。 Kubernetes 通常与基于云的解决方案一起使用，但它也可以部署在裸机服务器上。

在裸机服务器上部署 Kubernetes 比将其与基于云的解决方案一起使用具有一些优势。例如，它可以更具成本效益，并且您可以更好地控制硬件。

在本文中，我们将了解如何在裸机服务器上部署 Kubernetes 集群。我们还将研究您在执行此操作时可能面临的一些挑战。

## 概述

在我们开始之前，让我们快速浏览一下我们将在本文中使用的一些关键概念。

**Kubernetes**：Kubernetes 是一种容器编排工具，可用于管理大量容器。

**裸机服务器**：裸机服务器是没有虚拟化层的物理服务器。

**集群**：集群是一组用于运行应用程序或服务的服务器。

**主节点**：主节点是用来管理Kubernetes集群的服务器。

**工作节点**：工作节点是用于运行容器的服务器。

## 先决条件

在开始之前，您需要准备以下物品：

- 一组裸机服务器。对于本文，我们将使用三台服务器。
- 服务器可以连接到的网络交换机。
- 一种在服务器上安装 Kubernetes 的方法。对于本文，我们将使用 Kubernetes 安装程序 kubeadm。

## 安装 Kubernetes

在本节中，我们将了解如何在服务器上安装 Kubernetes。我们将使用 Kubernetes 安装程序 kubeadm。

Kubeadm 是一个可以用来安装和配置 Kubernetes 的工具。它的设计易于使用和扩展。

### 安装 kubeadm

我们需要做的第一件事是在服务器上安装 kubeadm。我们可以使用以下命令执行此操作：

```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update && sudo apt-get install -y kubeadm
```

### 初始化主节点

安装 kubeadm 后，我们可以初始化主节点。这是将用于管理 Kubernetes 集群的服务器。

要初始化主节点，我们需要使用 kubeadm init 命令。此命令将在服务器上启动 Kubernetes 控制平面。

```
sudo kubeadm init
```

命令完成后，您将看到如下所示的消息：

```
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following commands:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

You can now join any number of machines by running the following on each node
as root:

  kubeadm join 10.0.0.1:6443 --token ahc2xf.i0f4v9f0johtr5b4 --discovery-token-ca-cert-hash sha256:7ad1f8d3c908f3f558eaebf09abf8c3bdbbebfa7a7faebcbadea1a1a7fd0c74
```

您将需要运行输出中列出的命令，以便将您的服务器配置为使用 Kubernetes 集群。

### 加入工作节点

现在主节点已启动并正在运行，我们可以将工作节点添加到集群中。工作节点是用于运行容器的服务器。

要将工作节点添加到集群，我们需要使用 kubeadm join 命令。此命令会将服务器添加到 Kubernetes 集群。

```
sudo kubeadm join 10.0.0.1:6443 --token ahc2xf.i0f4v9f0johtr5b4 --discovery-token-ca-cert-hash sha256:7ad1f8d3c908f3f558eaebf09abf8c3bdbbebfa7a7faebcbadea1a1a7fd0c74
```

## 配置集群

在本节中，我们将了解如何配置 Kubernetes 集群。

### 配置主节点

我们需要做的第一件事是配置主节点。我们可以通过运行以下命令来完成此操作：

```
sudo kubectl apply -f https://git.io/weave-kube-1.6
```

此命令将在服务器上创建一个 pod 网络。 Pod 网络是用于连接容器的网络。

### 配置工作节点

接下来，我们需要配置工作节点。我们可以通过在每个工作节点上运行以下命令来完成此操作：

```
sudo kubectl apply -f https://git.io/weave-kube-1.6
```

此命令将在服务器上创建一个 pod 网络。 Pod 网络是用于连接容器的网络。

## 部署应用程序

在本节中，我们将了解如何将应用程序部署到 Kubernetes 集群。

我们将使用位于示例目录中的 nginx-deployment.yaml 文件。此文件包含 nginx 部署的配置。

要部署应用程序，我们需要运行以下命令：

```
kubectl apply -f examples/nginx-deployment.yaml
```

此命令将在 Kubernetes 集群上创建部署。部署是一组复制集。复制集是一组 Pod。

## 访问应用程序

在本节中，我们将了解如何访问我们部署的应用程序。

要访问应用程序，我们需要创建一个入口资源。入口资源是用于将流量路由到应用程序的资源。

我们可以通过运行以下命令来创建入口资源：

```
kubectl apply -f examples/nginx-ingress.yaml
```

此命令将在 Kubernetes 集群上创建入口资源。

创建入口资源后，我们可以通过以下 URL 访问应用程序：

http://<集群IP>

## 删除集群

在本节中，我们将了解如何删除 Kubernetes 集群。

要删除集群，我们需要使用 kubectl delete 命令。此命令将删除集群中的所有资源。

```
kubectl delete -f examples/nginx-deployment.yaml
kubectl delete -f examples/nginx-ingress.yaml
```

## 结论

在本文中，我们了解了如何在裸机服务器上部署 Kubernetes 集群。我们还研究了如何将应用程序部署到集群。