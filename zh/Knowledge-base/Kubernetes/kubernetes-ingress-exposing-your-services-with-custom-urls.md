---
title: Kubernetes Ingress：使用自定义 URL 公开您的服务
description: 
published: true
date: 2023-02-08T21:32:18.442Z
tags: 
editor: markdown
dateCreated: 2023-02-08T21:32:16.710Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes Ingress: Exposing Your Services with Custom URLs***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-ingress-exposing-your-services-with-custom-urls)
{.links-list}


# Kubernetes Ingress：使用自定义 URL 公开您的服务

Kubernetes Ingress 是一种向世界公开您的服务的强大方式。使用 Ingress，您可以为您的服务创建自定义 URL，出于多种原因，这可能很有用。

例如，您可能希望为您的服务创建一个易于记忆的 URL，或者您可能希望创建一个特定于特定服务的 URL。

在本文中，我们将了解如何创建 Kubernetes Ingress 资源，我们还将了解使用 Ingress 的一些好处。

## 创建入口资源

创建 Ingress 资源很简单。只需创建一个名为 ingress.yaml 的文件，其中包含以下内容：

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: my-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /my-service
        backend:
          serviceName: my-service
          servicePort: 80
```

在上面的示例中，我们创建了一个 Ingress 资源，它在 URL /my-service 处公开服务 my-service。

## Ingress 的好处

使用 Ingress 有很多好处。

首先，Ingress 允许您为您的服务创建自定义 URL。出于多种原因，这可能很有用。例如，您可能希望为您的服务创建一个易于记忆的 URL，或者您可能希望创建一个特定于特定服务的 URL。

其次，Ingress 允许您在多个服务之间负载均衡流量。如果您有多个服务于同一目的的服务，这会很有用。

第三，Ingress 允许您根据主机名路由流量。如果您想根据主机名将流量路由到不同的服务，这会很有用。

第四，Ingress 允许您根据路径路由流量。如果您想根据路径将流量路由到不同的服务，这会很有用。

最后，Ingress 允许您使用 SSL/TLS 保护您的服务。如果您要确保对您服务的流量进行加密，这会很有用。

## 结论

在本文中，我们研究了如何创建 Kubernetes Ingress 资源，还研究了使用 Ingress 的一些好处。