---
title: Kubernetes 资源管理：为您的 Pod 设置限制和请求
description: 
published: true
date: 2023-02-05T20:17:22.162Z
tags: 
editor: markdown
dateCreated: 2023-02-05T20:17:20.631Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes Resource Management: Setting Limits and Requests for Your Pods***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-resource-management-setting-limits-and-requests-for-your-pods)
{.links-list}


# Kubernetes 资源管理：为您的 Pod 设置限制和请求

在生产环境中，您需要能够控制应用程序使用的资源。这在像 Kubernetes 这样的容器化环境中尤为重要，因为许多应用程序可以在同一个集群上运行。

在 Kubernetes 中有两种主要方法可以做到这一点：设置限制和请求。限制定义了 pod 可以使用的最大资源量，而请求定义了 pod 需要的最小资源量。

在本文中，我们将了解如何为您的广告连播设置限制和请求。我们还将了解使用这些设置的一些最佳实践。

## 如何设置限制和请求

限制和请求被设置为 pod 上的注释。您可以在创建 pod 时设置它们，也可以稍后使用 kubectl annotate 命令设置它们。

以下是创建 Pod 时如何设置限制和请求的示例：

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
  annotations:
    "limits.cpu": "1",
    "requests.cpu": "0.5"
spec:
  containers:
  - name: mycontainer
    image: myimage
```

在此示例中，我们设置 1 个 CPU 的限制和 0.5 个 CPU 的请求。

您还可以使用 kubectl annotate 命令设置这些注释：

```
kubectl annotate pod mypod "limits.cpu=1" "requests.cpu=0.5"
```

## 最佳实践

在设置限制和请求时，请牢记一些最佳实践：

* 为每个资源设置限制和请求。如果你只设置一个限制，Kubernetes 不会强制执行。
* 确保您的请求少于您的限制。如果不是，则不会安排您的广告连播。
* 尝试将您的请求和限制设置得尽可能接近。这将有助于确保您的 pod 获得所需的资源。
* 请注意集群设置的默认限制。如果您不设置限制和请求，您的广告连播将使用这些默认值。

## 结论

在本文中，我们研究了如何为您的广告连播设置限制和请求。我们还查看了使用这些设置的一些最佳实践。通过遵循这些最佳实践，您可以确保您的 pod 获得所需的资源，而不会使用不必要的资源。