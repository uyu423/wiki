---
title: Kubernetes 网络策略：在 Pod 之间执行通信规则
description: 
published: true
date: 2023-02-09T02:32:30.867Z
tags: 
editor: markdown
dateCreated: 2023-02-09T02:32:29.221Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes Network Policies: Enforcing Communication Rules Between Pods***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-network-policies-enforcing-communication-rules-between-pods)
{.links-list}


# Kubernetes 网络策略：在 Pod 之间执行通信规则

Kubernetes 网络策略提供了一种在 pod 之间强制执行通信规则的方法。默认情况下，Kubernetes 集群中的所有 Pod 都可以相互通信。但是，在某些情况下，可能希望将通信限制为仅某些 pod。例如，您可能希望允许 Web 服务器和数据库服务器之间进行通信，但不允许 Web 服务器和应用程序服务器之间进行通信。

网络策略可用于通过指定允许哪些 pod 相互通信来实现此目的。网络策略作为 Kubernetes 资源实现，可以使用 YAML 或 JSON 定义。

下面是一个示例网络策略，它允许 Web 服务器和数据库服务器之间进行通信，但不允许 Web 服务器和应用程序服务器之间进行通信：

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-web-db
spec:
  podSelector:
    matchLabels:
      role: web
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: db
    ports:
    - protocol: TCP
      port: 3306
```

通过在 /etc/kubernetes/manifests 目录中创建名为 allow-web-db.yaml 的文件，可以将此网络策略应用于命名空间。

网络策略也可用于拒绝某些 pod 之间的通信。例如，以下网络策略拒绝 Web 服务器和应用程序服务器之间的所有通信：

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-web-app
spec:
  podSelector:
    matchLabels:
      role: web
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: app
    ports:
    - protocol: TCP
      port: 80
```

通过在“/etc/kubernetes/manifests”目录中创建名为“deny-web-app.yaml”的文件，可以将此网络策略应用于命名空间。

也可以允许某些 pod 之间的通信，同时拒绝其他 pod 之间的通信。例如，以下网络策略允许 Web 服务器和数据库服务器之间的通信，但拒绝 Web 服务器和应用程序服务器之间的通信：

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-web-db-deny-web-app
spec:
  podSelector:
    matchLabels:
      role: web
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: db
    ports:
    - protocol: TCP
      port: 3306
  - from:
    - podSelector:
        matchLabels:
          role: app
    ports:
    - protocol: TCP
      port: 80
```

通过在“/etc/kubernetes/manifests”目录中创建一个名为“allow-web-db-deny-web-app.yaml”的文件，可以将此网络策略应用于命名空间。

网络策略可以非常强大，可以用来实现 pod 之间复杂的通信规则。但是，请务必注意，网络策略仅在 pod 已正确标记时才有效。有关如何标记 pod 的更多信息，请参阅 Kubernetes 文档。

## 外部资源

- [Kubernetes 网络策略](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
- [标记 Pod](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)