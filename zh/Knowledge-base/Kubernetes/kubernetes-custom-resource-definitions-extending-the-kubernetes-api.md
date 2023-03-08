---
title: Kubernetes 自定义资源定义：扩展 Kubernetes API
description: 
published: true
date: 2023-02-01T08:24:13.625Z
tags: 
editor: markdown
dateCreated: 2023-02-01T08:24:12.123Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Kubernetes Custom Resource Definitions: Extending the Kubernetes API***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-custom-resource-definitions-extending-the-kubernetes-api)
{.links-list}



# Kubernetes 自定义资源定义：扩展 Kubernetes API

Kubernetes 自定义资源定义 (CRD) 提供了一种使用表示用户定义对象的新资源扩展 Kubernetes API 的方法。 CRD 允许 Kubernetes 管理员和开发人员创建和使用新资源，而无需修改 Kubernetes API 服务器或编写任何代码。

在本文中，我们将了解 CRD 的工作原理以及如何使用它们来扩展 Kubernetes API。我们还将探索 CRD 的一些用例，并查看社区开发的一些 CRD 示例。

## 什么是 Kubernetes 自定义资源定义？

自定义资源定义 (CRD) 是一种定义新 Kubernetes 资源的方法。 CRD 用于使用表示用户定义对象的新资源来扩展 Kubernetes API。 CRD 允许 Kubernetes 管理员和开发人员创建和使用新资源，而无需修改 Kubernetes API 服务器或编写任何代码。

CRD 类似于内置的 Kubernetes 资源，例如 Pod 和服务。与内置资源一样，CRD 具有名称、模式和一组操作（例如创建、读取、更新和删除）。 CRD 还可以与内置资源结合使用，以创建新的复合资源。

## Kubernetes 自定义资源定义如何工作？

CRD 存储在 Kubernetes API 服务器中，并由 Kubernetes API 服务器用于验证和服务用户请求。 CRD 是使用 OpenAPI v3 规范定义的。

OpenAPI v3 规范是描述 RESTful API 的标准。它定义了 API 的结构、可以执行的操作、输入和输出格式以及身份验证方法。

Kubernetes API 服务器使用 OpenAPI v3 规范来验证用户请求。当用户向 Kubernetes API 服务器发送请求时，Kubernetes API 服务器使用 OpenAPI v3 规范来验证请求。如果请求有效，Kubernetes API 服务器将请求转发到适当的 CRD。

Kubernetes API 服务器使用 OpenAPI v3 规范来验证用户请求。如果请求有效，Kubernetes API 服务器将请求转发到适当的 CRD。

## 使用 Kubernetes 自定义资源定义有什么好处？

与传统的 API 开发方法相比，CRD 具有许多优势：

- CRD 允许您定义新资源，而无需修改 Kubernetes API 服务器或编写任何代码。
- CRD 存储在 Kubernetes API 服务器中，供 Kubernetes API 服务器用于验证和服务用户请求。
- CRD 是使用 OpenAPI v3 规范定义的，该规范是描述 RESTful API 的标准。
- CRD 可以与内置资源结合使用以创建新的复合资源。

## Kubernetes 自定义资源定义有哪些用例？

CRD 可用于使用表示用户定义对象的新资源来扩展 Kubernetes API。 CRD 允许 Kubernetes 管理员和开发人员创建和使用新资源，而无需修改 Kubernetes API 服务器或编写任何代码。

CRD 可用于创建代表以下内容的新资源：

- 集群对象，例如命名空间、节点和 Pod。
- 应用程序对象，例如 Deployments、Services 和 Ingresses。
- 自定义对象，例如客户记录、订单记录和产品记录。

## 如何创建 Kubernetes 自定义资源定义？

创建 CRD 分为两步：

1. 使用 OpenAPI v3 规范定义 CRD。
2. 向 Kubernetes API 服务器注册 CRD。

OpenAPI v3 规范是描述 RESTful API 的标准。它定义了 API 的结构、可以执行的操作、输入和输出格式以及身份验证方法。

Kubernetes API 服务器使用 OpenAPI v3 规范来验证用户请求。当用户向 Kubernetes API 服务器发送请求时，Kubernetes API 服务器使用 OpenAPI v3 规范来验证请求。如果请求有效，Kubernetes API 服务器将请求转发到适当的 CRD。

向 Kubernetes API 服务器注册 CRD 分为两步：

1. 创建一个名为 crd.yaml 的文件，内容如下：

```yaml
apiVersion: apiextensions.k8s.io/v1beta1
kind: CustomResourceDefinition
metadata:
  name: {crd-name}
spec:
  group: {crd-group}
  version: {crd-version}
  names:
    kind: {crd-kind}
    plural: {crd-plural}
  scope: {crd-scope}
```

2. 向 Kubernetes API 服务器注册 CRD：

```
kubectl create -f crd.yaml
```

## 如何使用 Kubernetes 自定义资源定义？

创建 CRD 后，您可以使用它来创建新资源。创建资源是一个两步过程：

1. 使用 OpenAPI v3 规范定义资源。
2. 使用 kubectl create 命令创建资源。

OpenAPI v3 规范是描述 RESTful API 的标准。它定义了 API 的结构、可以执行的操作、输入和输出格式以及身份验证方法。

Kubernetes API 服务器使用 OpenAPI v3 规范来验证用户请求。当用户向 Kubernetes API 服务器发送请求时，Kubernetes API 服务器使用 OpenAPI v3 规范来验证请求。如果请求有效，Kubernetes API 服务器将请求转发到适当的 CRD。

创建资源是一个两步过程：

1. 使用 OpenAPI v3 规范定义资源。
2. 使用 kubectl create 命令创建资源。

```
kubectl create -f {resource-definition.yaml}
```

## 有哪些 Kubernetes 自定义资源定义示例？

以下是社区开发的一些示例 CRD：

- [Kubernetes 命名空间](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/namespaces.md)
- [Kubernetes 节点](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/nodes.md)
- [Kubernetes Pod](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/pods.md)
- [Kubernetes 服务](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/services.md)
- [Kubernetes 部署](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/deployments.md)
- [Kubernetes Ingress](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/ingresses.md)
- [Kubernetes 工作](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/jobs.md)
- [Kubernetes CronJob](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-api-machinery/cronjobs.md)

## 结论

在本文中，我们了解了 CRD 的工作原理以及如何使用它们来扩展 Kubernetes API。我们还探讨了 CRD 的一些用例，并查看了社区开发的一些 CRD 示例。