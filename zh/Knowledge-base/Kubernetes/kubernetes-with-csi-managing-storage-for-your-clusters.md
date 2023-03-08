---
title: 带有 CSI 的 Kubernetes：管理集群的存储
description: 
published: true
date: 2023-02-14T12:32:40.332Z
tags: 
editor: markdown
dateCreated: 2023-02-14T12:32:38.589Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes with CSI: Managing Storage for Your Clusters***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-csi-managing-storage-for-your-clusters)
{.links-list}


# 带有 CSI 的 Kubernetes：管理集群的存储

容器存储接口 (CSI) 是容器编排解决方案（例如 Kubernetes）使用的一组 API，用于为其应用程序配置和管理块存储。虽然 Kubernetes 内置了对一些存储解决方案的支持，例如 Google Cloud Storage，但使用 CSI 可以让 Kubernetes 支持更广泛的存储解决方案。

在本文中，我们将了解如何将 CSI 与 Kubernetes 结合使用来管理集群的存储。我们还将了解使用 CSI 的一些好处，以及它如何帮助您更轻松地管理应用程序的存储。

## 什么是犯罪现场调查？

容器存储接口 (CSI) 是容器编排解决方案（例如 Kubernetes）使用的一组 API，用于为其应用程序配置和管理块存储。虽然 Kubernetes 内置了对一些存储解决方案的支持，例如 Google Cloud Storage，但使用 CSI 可以让 Kubernetes 支持更广泛的存储解决方案。

CSI 提供了一组 API，可用于为容器配置和管理存储。例如，您可以使用 CSI 为容器创建存储卷，将其附加到正在运行的容器，或将其与正在运行的容器分离。您还可以使用 CSI 对容器的存储卷进行快照或删除存储卷。

## 如何在 Kubernetes 中使用 CSI

在 Kubernetes 中使用 CSI 很简单。首先，您需要在每个 Kubernetes 节点上为您的存储解决方案安装 CSI 驱动程序。接下来，您需要为您的存储解决方案创建一个存储类。最后，您需要为每个需要存储的应用程序创建一个 Persistent Volume Claim (PVC)。

安装 CSI 驱动程序超出了本文的范围，但您可以在存储解决方案的文档中找到相关说明。

安装 CSI 驱动程序后，您可以为存储解决方案创建存储类。存储类定义将用于您的应用程序的存储特性。例如，存储类可以定义存储的大小、复制因子和性能配置文件。

要创建存储类，您需要使用 kubectl 命令行工具。以下命令将为名为“mystorage”的假设存储解决方案创建一个存储类：

```
kubectl create storage-class mystorage \
--provisioner=csi.mystorage.com \
--parameters=size=1Gi,replicationFactor=3,performanceProfile=low
```

一旦定义了存储类，就可以为每个需要存储的应用程序创建一个 PVC。 PVC 是对特定存储类的存储请求。例如，以下 PVC 从“mystorage”存储类请求 1 GB 的存储空间：

```
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: mystorage-pvc
  namespace: default
spec:
  storageClassName: mystorage
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

当您创建 PVC 时，Kubernetes 将从存储类中提供一个存储卷并将其绑定到 PVC。然后，您可以使用 PVC 将存储卷装载到容器中。

## 使用 CSI 的好处

将 CSI 与 Kubernetes 结合使用有很多好处：

- **简化存储管理**：将 CSI 与 Kubernetes 结合使用有助于简化应用程序的存储管理。例如，您可以使用单个存储类为多个应用程序配置存储。

- **增加存储解决方案的灵活性**：CSI 允许 Kubernetes 支持更广泛的存储解决方案。如果您使用的是 Kubernetes 本身不支持的存储解决方案，这会很有帮助。

- **改进的存储解决方案集成**：CSI 可以帮助改进 Kubernetes 和存储解决方案之间的集成。例如，某些存储解决方案可能会提供可与 Kubernetes 一起使用的附加功能，例如快照和复制。

## 结论

在本文中，我们研究了如何将 CSI 与 Kubernetes 结合使用来管理应用程序的存储。我们还了解了使用 CSI 的一些好处，例如简化存储管理和提高存储解决方案的灵活性。