---
title: Kubernetes 命名空间：隔离多租户集群中的资源
description: 
published: true
date: 2023-02-08T23:32:18.990Z
tags: 
editor: markdown
dateCreated: 2023-02-08T23:32:17.378Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes Namespaces: Isolating Resources in Multi-Tenant Clusters***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-namespaces-isolating-resources-in-multi-tenant-clusters)
{.links-list}


# Kubernetes 命名空间：隔离多租户集群中的资源

Kubernetes 命名空间提供了一种简单但功能强大的方式来隔离共享集群中的资源。通过为每个租户创建单独的命名空间，您可以控制哪些用户可以访问哪些资源，并限制资源在租户之间的可见性。

## 创建命名空间

您可以通过运行 kubectl create namespace 命令来创建命名空间。例如，要为名为 acme 的租户创建命名空间，您可以运行：

```
kubectl create namespace acme
```

## 将资源分配给命名空间

创建命名空间后，您可以使用 `--namespace` 标志和 `kubectl` 命令为其分配资源。例如，要在 acme 命名空间中创建一个 pod，您可以运行：

```
kubectl create pod --namespace acme ...
```

## 查看命名空间中的资源

默认情况下，`kubectl` 命令只会显示`default` 命名空间中的资源。要查看不同命名空间中的资源，您可以将 `--namespace` 标志与 `kubectl get` 命令一起使用。例如，要查看 acme 命名空间中的所有 pod，您可以运行：

```
kubectl get pods --namespace acme
```

## 在命名空间之间切换

如果您发现自己经常在特定命名空间中运行命令，则可以使用 kubectl config set-context 命令在命名空间之间切换。例如，要切换到 acme 命名空间，您可以运行：

```
kubectl config set-context $(kubectl config current-context) --namespace=acme
```

## 删除命名空间

您可以通过运行 kubectl delete namespace 命令删除命名空间。例如，要删除 `acme` 命名空间，您可以运行：

```
kubectl delete namespace acme
```

## 结论

Kubernetes 命名空间提供了一种简单但功能强大的方式来隔离共享集群中的资源。通过为每个租户创建单独的命名空间，您可以控制哪些用户可以访问哪些资源，并限制资源在租户之间的可见性。