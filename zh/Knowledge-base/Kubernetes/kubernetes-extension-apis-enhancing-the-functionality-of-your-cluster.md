---
title: Kubernetes 扩展 API：增强集群的功能
description: 
published: true
date: 2023-02-17T18:17:25.107Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:23:22.423Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Kubernetes Extension APIs: Enhancing the Functionality of Your Cluster***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-extension-apis-enhancing-the-functionality-of-your-cluster)
{.links-list}



# Kubernetes 扩展 API：增强集群的功能

Kubernetes 是一个开源系统，用于自动部署、扩展和管理容器化应用程序。它将构成应用程序的容器分组为逻辑单元，以便于管理和发现。 Kubernetes 还提供存储编排、网络和安全机制。

扩展 Kubernetes 功能是一个热门话题，并且有很多方法可以做到这一点。在本文中，我们将重点关注 Kubernetes 扩展 API。我们将讨论它们是什么、它们如何工作以及您可能想要使用它们的原因。我们还将提供一些示例代码来帮助您入门。

## 什么是 Kubernetes 扩展 API？

Kubernetes 扩展 API 是一组 API，可让您扩展 Kubernetes 集群的功能。它们提供了一种在不更改核心代码的情况下向 Kubernetes 添加新功能的方法。

扩展 API 作为 CustomResourceDefinitions (CRD) 实现。 CRD 是一种向 Kubernetes 添加新资源的方法。资源是 Kubernetes 可以管理的对象，例如 Pod 或服务。 CRD 允许您定义 Kubernetes 可以管理的新资源。

## Kubernetes 扩展 API 如何工作？

Kubernetes 扩展 API 作为 CustomResourceDefinitions (CRD) 实现。 CRD 是一种向 Kubernetes 添加新资源的方法。资源是 Kubernetes 可以管理的对象，例如 Pod 或服务。 CRD 允许您定义 Kubernetes 可以管理的新资源。

每个 CRD 都有资源的描述，包括名称、类型和属性。 Kubernetes 使用此信息来创建新资源。然后，您可以使用 Kubernetes API 来管理这个新资源。

## 为什么使用 Kubernetes 扩展 API？

Kubernetes 扩展 API 提供了一种在不更改核心代码的情况下向 Kubernetes 添加新功能的方法。如果您想要添加新功能，或者如果您想要在不影响集群稳定性的情况下试验新代码，这会很有用。

扩展 API 还提供了一种与 Kubernetes 社区共享代码的方法。如果你认为你的代码对其他人有用，你可以提交它以包含在 Kubernetes 中。

## 示例代码

下面是 CustomResourceDefinition 的一个简单示例：

```
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: mycrd.example.com
spec:
  scope: Cluster
  group: example.com
  version: v1
  names:
    plural: mycrds
    singular: mycrd
    kind: MyCrd
    shortNames:
    - crd
  validation:
    openAPIV3Schema:
      description: MyCrds are ..."
      type: object
      properties:
        spec:
          type: object
          properties:
            size:
              type: integer
              minimum: 1
              maximum: 100
          required:
          - size
  subresources:
    status: {}
```

该 CRD 定义了一个名为“MyCrd”的资源。此资源有一个名为“大小”的属性，它是 1 到 100 之间的整数。

您可以使用 Kubernetes API 创建、更新和删除 MyCrds：

```
# Create a MyCrd
apiVersion: example.com/v1
kind: MyCrd
metadata:
  name: mycrd-1
spec:
  size: 10

# Update a MyCrd
apiVersion: example.com/v1
kind: MyCrd
metadata:
  name: mycrd-1
spec:
  size: 20

# Delete a MyCrd
apiVersion: example.com/v1
kind: MyCrd
metadata:
  name: mycrd-1
spec:
  size: 0
```

## 结论

Kubernetes 扩展 API 提供了一种在不更改核心代码的情况下向 Kubernetes 添加新功能的方法。它们作为 CustomResourceDefinitions (CRD) 实现，这是一种向 Kubernetes 添加新资源的方式。每个 CRD 都有资源的描述，包括名称、类型和属性。 Kubernetes 使用此信息来创建新资源。

您可以使用 Kubernetes Extension API 向 Kubernetes 添加新功能，或者在不影响集群稳定性的情况下试验新代码。如果你认为你的代码对其他人有用，你可以提交它以包含在 Kubernetes 中。