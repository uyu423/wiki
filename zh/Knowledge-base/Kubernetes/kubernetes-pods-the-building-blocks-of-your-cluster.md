---
title: Kubernetes Pod：集群的构建块
description: 
published: true
date: 2023-02-17T18:05:45.604Z
tags: 
editor: markdown
dateCreated: 2023-01-30T14:32:40.141Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Kubernetes Pods: The Building Blocks of Your Cluster***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-pods-the-building-blocks-of-your-cluster)
{.links-list}



# Kubernetes Pod：集群的构建块

Kubernetes pod 是 Kubernetes 集群中最小的可部署单元，它们是集群的构建块。 Pod 是短暂的，这意味着它们不能保证在任何给定时间运行，并且可以根据需要删除和重新创建。

Pod 由 Kubernetes 控制平面管理，它们可能会在您不知情的情况下崩溃和重启。这是使用 Kubernetes 的好处之一：通过抽象化集群中的各个机器，您可以将整个集群视为一个实体。

Pod 包含一个或多个容器，它们可用于托管应用程序、数据库或您需要在 Kubernetes 集群中运行的任何其他内容。 Pod 始终在同一节点上共同定位和共同调度，这意味着它们可以共享卷和网络接口等资源。

创建 Pod 时，必须为 Pod 指定所需的状态，包括容器映像和任何必需的配置。然后 Kubernetes 将负责将 Pod 保持在所需状态。

Pod 是 Kubernetes 中的基本部署单元，通常用于承载无状态应用。如果需要在 Kubernetes 中运行有状态应用程序，则需要使用 StatefulSet。

## 创建一个 Pod

您可以使用 `kubectl` 命令行工具创建 pod，也可以使用清单文件。

### 使用`kubectl`

要使用 `kubectl` 创建 pod，您可以使用 `run` 命令。例如，要创建一个将运行 `nginx` 容器镜像的 pod，您可以使用以下命令：

```
kubectl run nginx --image=nginx
```

这将创建一个带有单个“nginx”容器的 pod。如果你想创建一个包含多个容器的 pod，你可以使用 `run-container` 命令：

```
kubectl run-container nginx-container --image=nginx --image=mysql
```

### 使用清单文件

或者，您可以通过创建一个“Pod”清单文件并使用“kubectl”“create”命令来创建一个 pod。例如，以下清单文件将创建一个带有单个“nginx”容器的 pod：

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx
```

然后，您可以通过运行以下命令来创建 pod：

```
kubectl create -f nginx.yaml
```

## 删除 Pod

可以使用 `kubectl` `delete` 命令删除 Pod。例如，要删除上一节中创建的`nginx` pod，您可以使用以下命令：

```
kubectl delete pod nginx
```

## Pod 状态

Pod 可以处于以下状态之一：

- **Pending**：pod 已创建，但其中的一个或多个容器尚未启动。
- **Running**：pod 及其所有容器都在运行。
- **成功**：pod 成功完成其工作并且其所有容器都处于“已退出”状态。
- **失败**：pod 失败，其所有容器都处于“退出”状态。
- **Unknown**：无法确定 pod 的状态。

## 结论

Kubernetes pod 是集群的构建块，它们用于托管应用程序、数据库或您需要在 Kubernetes 集群中运行的任何其他内容。 Pod 始终在同一节点上共同定位和共同调度，这意味着它们可以共享卷和网络接口等资源。

创建 Pod 时，必须为 Pod 指定所需的状态，包括容器映像和任何必需的配置。然后 Kubernetes 将负责将 Pod 保持在所需状态。

Pod 是 Kubernetes 中的基本部署单元，通常用于承载无状态应用。如果需要在 Kubernetes 中运行有状态应用程序，则需要使用 StatefulSet。