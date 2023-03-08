---
title: 调试 Kubernetes 应用程序：了解事件和日志
description: 
published: true
date: 2023-02-17T18:16:19.882Z
tags: 
editor: markdown
dateCreated: 2023-01-31T00:43:18.512Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Debugging Kubernetes Applications: Understanding Events and Logs***English** version of this document is available*](/en/Knowledge-base/Kubernetes/debugging-kubernetes-applications-understanding-events-and-logs)
{.links-list}


# 调试 Kubernetes 应用程序：了解事件和日志

Kubernetes 是一个强大的编排工具，但调试在其上运行的应用程序可能很棘手。在本文中，我们将介绍两个用于调试 Kubernetes 应用程序的重要工具：事件和日志。

## 活动

事件是了解 Kubernetes 集群内部发生的事情的好方法。要查看事件，请使用 `kubectl` 命令：

```
kubectl get events
```

这将返回集群中所有事件的列表，以及它们的时间戳、类型等。

事件可以按标签过滤，所以如果你只想查看与特定 pod 相关的事件，你可以使用 `--selector` 标志：

```
kubectl get events --selector=app=nginx
```

也可以查看特定命名空间的事件：

```
kubectl get events --namespace=default
```

最后，您可以使用 `--since` 标志仅获取自特定时间以来发生的事件：

```
kubectl get events --since=2019-01-01T00:00:00Z
```

## 日志

除了事件之外，日志是调试 Kubernetes 应用程序的另一个重要工具。要获取 pod 的日志，请使用 `kubectl` 命令：

```
kubectl logs POD_NAME
```

将 `POD_NAME` 替换为您要获取其日志的 Pod 的名称。

也可以获取部署中所有 pod 的日志：

```
kubectl logs DEPLOYMENT_NAME
```

将 `DEPLOYMENT_NAME` 替换为您要为其获取日志的部署的名称。

最后，您可以使用 `--since` 标志仅获取自特定时间以来生成的日志：

```
kubectl logs --since=2019-01-01T00:00:00Z
```

## 结论

在本文中，我们了解了两个用于调试 Kubernetes 应用程序的重要工具：事件和日志。事件是了解 Kubernetes 集群内部发生的事情的好方法，日志可用于解决应用程序的问题。