---
title: Kubernetes 服务：向世界公开您的应用程序
description: 
published: true
date: 2023-02-06T08:55:28.006Z
tags: 
editor: markdown
dateCreated: 2023-02-06T08:55:26.478Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes Services: Exposing Your Applications to the World***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-services-exposing-your-applications-to-the-world)
{.links-list}


# Kubernetes 服务：向世界公开您的应用程序

在传统部署中，当您想要向世界公开一项新服务时，您必须更新防火墙规则以允许流量到达您的新服务。在使用 Kubernetes 的容器化部署中，您可以使用“服务”对象向世界公开您的应用程序。

Kubernetes 中的服务是一种抽象，它定义了一组逻辑 Pod 和访问它们的策略——有时称为微服务。每个服务都分配有一个唯一的 IP 地址（有时称为“集群 IP”），该地址由服务代理（见下文）使用，并且是用于访问服务的任何 URL 的一部分。

Kubernetes 中有两种类型的服务：`ClusterIP` 和 `NodePort`。

`ClusterIP` 服务，默认的 Kubernetes 服务类型，在集群的内部 IP 上公开服务。这种类型使服务只能从集群内访问。

`NodePort` 服务在集群中每个节点的相同端口上公开服务。这种类型使服务可以从集群外部的每个节点的 IP 上的静态端口（“NodePort”）访问。您可以使用 `NodePort` 服务将在 Kubernetes 集群中运行的应用程序公开到互联网。

在本文中，我们将重点关注 `NodePort` 服务。

## 创建服务

假设我们有一个包含两个 Pod 的部署，每个 Pod 在端口 8080 上运行一个简单的 Web 服务器。我们可以使用 `NodePort` 服务向世界公开这些 Pod，如下所示：

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  selector:
    app: my-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080
```

在此示例中，我们定义了一个名为“my-service”的服务，它选择“app”标签设置为“my-app”的 Pod。我们还定义了该服务应公开端口 80（`port`）并将流量转发到所选 Pod 上的端口 8080（`targetPort`）。

## 访问服务

一旦你创建了一个服务，你就可以从集群外部在 `NodePort` 的每个节点的 IP 上访问它：

```
http://<Node IP>:<NodePort>
```

例如，如果我们有一个 NodePort 为 31001 的服务，我们可以通过以下方式访问它：

```
http://<Node IP>:31001
```

## 结论

在本文中，我们了解了如何使用 `NodePort` 服务将在 Kubernetes 集群中运行的应用程序公开到互联网。我们已经了解了如何创建服务以及如何从集群外部访问它。