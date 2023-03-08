---
title: Kubernetes Web UI：使用仪表板管理您的集群
description: 
published: true
date: 2023-02-14T02:32:33.112Z
tags: 
editor: markdown
dateCreated: 2023-02-14T02:32:25.890Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes Web UI: Managing Your Cluster with the Dashboard***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-web-ui-managing-your-cluster-with-the-dashboard)
{.links-list}


# Kubernetes Web UI：使用仪表板管理集群

Kubernetes 是一种功能强大的容器编排工具，可帮助您大规模管理应用程序和资源。 Kubernetes 仪表板是一个基于 Web 的 UI，可以帮助您管理 Kubernetes 集群。在本文中，我们将了解如何使用仪表板来管理您的集群。

## 访问仪表板

要访问仪表板，您需要启动并运行 Kubernetes 集群。您可以按照 Kubernetes 文档中的说明[设置本地集群](https://kubernetes.io/docs/setup/learning-environment/minikube/)。

集群启动并运行后，您可以通过运行以下命令访问仪表板：

```
kubectl proxy
```

这将启动 Kubernetes API 服务器的代理，并使仪表板在 http://localhost:8001/api/v1/namespaces/kube-system/services/kubernetes-dashboard:/proxy/ 可用。

## 创建 Kubernetes 集群

要创建 Kubernetes 集群，您需要有一个正在运行的 Kubernetes 集群。您可以按照 Kubernetes 文档中的说明[设置本地集群](https://kubernetes.io/docs/setup/learning-environment/minikube/)。

启动并运行 Kubernetes 集群后，您可以通过运行以下命令来创建新集群：

```
kubectl create cluster my-cluster
```

您可以通过运行以下命令来验证集群是否已创建：

```
kubectl get clusters
```

## 删除 Kubernetes 集群

要删除 Kubernetes 集群，您需要有一个正在运行的 Kubernetes 集群。您可以按照 Kubernetes 文档中的说明[设置本地集群](https://kubernetes.io/docs/setup/learning-environment/minikube/)。

启动并运行 Kubernetes 集群后，您可以通过运行以下命令删除集群：

```
kubectl delete cluster my-cluster
```

您可以通过运行以下命令来验证集群是否已删除：

```
kubectl get clusters
```

## 管理节点

Kubernetes 仪表板可用于管理 Kubernetes 集群中的节点。要查看集群中的节点列表，请单击左侧导航栏中的“节点”链接。这将打开一个页面，其中列出集群中的所有节点。

在此页面中，您可以查看有关每个节点的信息，例如其 IP 地址、操作系统和内核版本。您还可以对节点执行操作，例如删除它们或放大或缩小它们。

## 管理 Pod

Kubernetes 仪表板可用于管理 Kubernetes 集群中的 pod。要查看集群中的 pod 列表，请单击左侧导航中的“Pods”链接。这将打开一个页面，其中列出集群中的所有 pod。

在此页面中，您可以查看有关每个 pod 的信息，例如它的 IP 地址和它运行的节点。您还可以对 pod 执行操作，例如删除它们或放大或缩小它们。

## 管理部署

Kubernetes 仪表板可用于管理 Kubernetes 集群中的部署。要查看集群中的部署列表，请单击左侧导航中的“部署”链接。这将打开一个页面，其中列出集群中的所有部署。

在此页面中，您可以查看有关每个部署的信息，例如部署中的副本数和 Pod。您还可以对部署执行操作，例如向上或向下扩展它们。

## 管理服务

Kubernetes 仪表板可用于管理 Kubernetes 集群中的服务。要查看集群中的服务列表，请单击左侧导航中的“服务”链接。这将打开一个页面，列出集群中的所有服务。

在此页面中，您可以查看有关每个服务的信息，例如服务类型和属于该服务的 pod。您还可以对服务执行操作，例如编辑服务或删除服务。

## 结论

在本文中，我们了解了如何使用 Kubernetes 仪表板来管理 Kubernetes 集群。我们已经了解了如何创建和删除集群、如何管理节点和 Pod，以及如何管理部署和服务。