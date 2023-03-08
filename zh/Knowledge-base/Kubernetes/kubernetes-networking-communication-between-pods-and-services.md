---
title: Kubernetes 网络：Pod 和服务之间的通信
description: 
published: true
date: 2023-02-08T20:32:16.122Z
tags: 
editor: markdown
dateCreated: 2023-02-08T20:32:14.553Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes Networking: Communication Between Pods and Services***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-networking-communication-between-pods-and-services)
{.links-list}


# Kubernetes 网络：Pod 和服务之间的通信

Kubernetes 网络是一个复杂的话题，事实上有多种不同的配置方式使它变得更加复杂。在本文中，我们将重点关注 Pod 和服务之间的通信。

Pod 是 Kubernetes 中部署的基本单元，可以被认为是类固醇上的容器。它们可以包含多个容器，拥有自己的 IP 地址，可用于将应用程序彼此隔离。

服务用于将在 Pod 中运行的应用程序暴露给外界。它们可以使用多种不同的方法公开，包括 ClusterIP、NodePort 和 LoadBalancer。

创建服务时，Kubernetes 会创建一个虚拟 IP (VIP) 地址，用于将流量路由到属于该服务的 pod。

## Pod 之间的通信

Pod 之间的通信由 Kubernetes 网络层处理。默认情况下，每个 pod 在集群中都分配了一个唯一的 IP 地址，并且可以使用该地址与其他 pod 通信。

Pod 也可以使用主机名相互通信。默认情况下，每个 pod 都分配有一个基于其 IP 地址的主机名。例如，如果 pod 的 IP 地址为 10.0.0.1，则其主机名将为 1-10-0-0-1.pods.cluster.local。

## 服务之间的通信

服务之间的通信由 Kubernetes 网络层处理。默认情况下，每个服务都在集群中分配了一个唯一的 IP 地址，并且可以使用该地址与其他服务进行通信。

服务也可以使用主机名相互通信。默认情况下，每个服务都分配有一个基于其 IP 地址的主机名。例如，如果服务的 IP 地址为 10.0.0.1，则其主机名将为 1-10-0-0-1.services.cluster.local。

## Pod 和服务之间的通信

Pod 可以使用服务的 IP 地址或主机名与服务通信。默认情况下，Pod 被分配一个基于服务 IP 地址的主机名。例如，如果一个 pod 的 IP 地址为 10.0.0.1，而一个服务的 IP 地址为 10.0.0.2，则该 pod 将能够使用主机名 2-10-0-0-2.services 与该服务通信.cluster.local。

Pod 还可以使用服务的 ClusterIP 地址与服务通信。默认情况下，ClusterIP 地址分配给 pod 的默认网络接口。例如，如果 pod 的 IP 地址为 10.0.0.1，服务的 ClusterIP 地址为 10.0.0.2，则 pod 将能够使用 ClusterIP 地址与服务通信。

## 结论

Kubernetes 网络是一个复杂的话题，但 Pod 和服务之间的通信是其中的关键部分。在本文中，我们介绍了 Pod 和服务如何相互通信的基础知识。