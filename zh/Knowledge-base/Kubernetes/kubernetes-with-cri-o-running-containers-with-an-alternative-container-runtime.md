---
title: 带有 CRI-O 的 Kubernetes：使用替代容器运行时运行容器
description: 
published: true
date: 2023-02-14T09:32:29.308Z
tags: 
editor: markdown
dateCreated: 2023-02-14T09:32:22.068Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes with CRI-O: Running Containers with an Alternative Container Runtime***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-cri-o-running-containers-with-an-alternative-container-runtime)
{.links-list}


# 带有 CRI-O 的 Kubernetes：使用替代容器运行时运行容器

## 什么是 CRI-O？

CRI-O 是 Kubernetes 的替代容器运行时。它被设计为轻量级且占用空间最小，非常适合在 Kubernetes 上运行容器。 CRI-O 使用开放容器倡议 (OCI) 运行时规范，并与 Kubernetes CRI（容器运行时接口）兼容。

## 为什么要将 CRI-O 与 Kubernetes 一起使用？

您可能希望将 CRI-O 与 Kubernetes 结合使用的原因有以下几个：

- CRI-O 设计为重量轻且占地面积最小。这使得它非常适合在 Kubernetes 上运行容器。
- CRI-O 使用开放容器倡议 (OCI) 运行时规范。这意味着它与 Kubernetes CRI（容器运行时接口）兼容。
- CRI-O 与 Kubernetes 容器网络接口 (CNI) 插件集成。这使得为在 Kubernetes 上运行的容器设置网络变得容易。

## 如何在 Kubernetes 中使用 CRI-O

将 CRI-O 与 Kubernetes 一起使用很容易。您可以直接使用 CRI-O 容器运行时，也可以使用 CRI-O Kubernetes 集成。

### 直接使用CRI-O容器运行时

要直接使用 CRI-O 容器运行时，需要在启动 Kubernetes `kubelet` 时设置 `--runtime` 标志：

```
$ kubelet --runtime=cri-o
```

### 使用 CRI-O Kubernetes 集成

要使用 CRI-O Kubernetes 集成，您需要在启动 Kubernetes `kubelet` 时设置 `--container-runtime` 标志：

```
$ kubelet --container-runtime=cri-o
```

您还需要设置 `--feature-gates` 标志以启用 CRI-O Kubernetes 集成：

```
$ kubelet --feature-gates=CRIO=true
```

## 结论

CRI-O 是 Kubernetes 的一个很好的替代容器运行时。它被设计为轻量级且占用空间最小，非常适合在 Kubernetes 上运行容器。 CRI-O 使用开放容器倡议 (OCI) 运行时规范，并与 Kubernetes CRI（容器运行时接口）兼容。 CRI-O 还集成了 Kubernetes 容器网络接口 (CNI) 插件。这使得为在 Kubernetes 上运行的容器设置网络变得容易。