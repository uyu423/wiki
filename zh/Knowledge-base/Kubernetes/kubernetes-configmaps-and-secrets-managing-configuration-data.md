---
title: Kubernetes ConfigMaps 和秘密：管理配置数据
description: 
published: true
date: 2023-02-01T17:43:45.728Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:43:43.776Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Kubernetes ConfigMaps and Secrets: Managing Configuration Data***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-configmaps-and-secrets-managing-configuration-data)
{.links-list}



# Kubernetes ConfigMaps 和秘密：管理配置数据

Kubernetes 提供了两种存储和管理配置数据和机密的机制：ConfigMaps 和 Secrets。在本文中，我们将了解它们分别是什么、它们如何工作以及如何在您的 Kubernetes 应用程序中有效地使用它们。

## 什么是 ConfigMap？

ConfigMap 是一种 Kubernetes 资源，它以键值对的形式存储配置数据。应用程序可以根据需要使用此数据进行读取和使用。例如，您可以将数据库连接字符串、API 密钥或其他机密存储在 ConfigMap 中。

ConfigMap 存储在 etcd 中，与 Kubernetes 存储其集群状态的位置相同。这意味着它们具有高可用性，可以被集群中的任何节点使用。

## 什么是秘密？

Secret 是一种 Kubernetes 资源，用于存储敏感信息，例如密码、API 密钥或证书。秘密是加密的，只能由需要使用它们的节点解密。这意味着 Secret 比 ConfigMap 更安全，但也更难管理。

 秘密也存储在 etcd 中，但它们是静态加密的。

## 创建配置映射

创建 ConfigMap 很简单。我们只需要用配置数据创建一个 YAML 文件。例如，让我们为数据库连接字符串创建一个 ConfigMap：

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  database-connection-string: "user:password@host:port/database"
```

然后我们可以使用 kubectl 命令行工具创建 ConfigMap：

```
$ kubectl create -f my-config.yaml
configmap/my-config created
```

## 创建秘密

创建 Secret 类似于创建 ConfigMap。我们只需要用配置数据创建一个 YAML 文件。例如，让我们为 API 密钥创建一个 Secret：

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  api-key: "Zm9vYmFy"
```

Secret 中的数据必须是 base64 编码的。然后我们可以使用 kubectl 命令行工具创建 Secret：

```
$ kubectl create -f my-secret.yaml
secret/my-secret created
```

## 使用 ConfigMap 和 Secrets

现在我们已经创建了 ConfigMap 和 Secret，让我们看看如何在我们的应用程序中使用它们。

在 Kubernetes 中使用 ConfigMaps 和 Secrets 有两种方式：环境变量和卷。

### 环境变量

我们可以使用环境变量将 ConfigMap 和 Secret 中的数据注入到我们的应用程序中。为此，我们只需要将以下注释添加到我们的 ConfigMap 和 Secret 中：

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
  annotations:
    "configmap.kubernetes.io/env": "MY_CONFIG"
data:
  database-connection-string: "user:password@host:port/database"
```

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
  annotations:
    "secret.kubernetes.io/env": "MY_SECRET"
type: Opaque
data:
  api-key: "Zm9vYmFy"
```

注释将使 Kubernetes 将我们的 ConfigMap 和 Secret 中的数据注入到我们应用程序 pod 的环境中。数据将在环境变量 MY_CONFIG 和 MY_SECRET 中可用。

### 卷

我们还可以使用卷将 ConfigMap 和 Secret 中的数据装载到我们的应用程序中。为此，我们只需要将以下注释添加到我们的 ConfigMap 和 Secret 中：

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
  annotations:
    "configmap.kubernetes.io/volume": "my-config-volume"
data:
  database-connection-string: "user:password@host:port/database"
```

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
  annotations:
    "secret.kubernetes.io/volume": "my-secret-volume"
type: Opaque
data:
  api-key: "Zm9vYmFy"
```

注释将使 Kubernetes 为我们的 ConfigMap 和 Secret 创建卷。这些卷将在我们的应用程序 pod 中可用，路径为 /etc/config/my-config-volume 和 /etc/config/my-secret-volume。

## 结论

ConfigMaps 和 Secrets 是 Kubernetes 中管理配置数据和机密的两个重要工具。它们都存储在 etcd 中，可以被集群中的任何节点使用。

ConfigMap 不如 Secrets 安全，但更易于管理。秘密更安全，但更难管理。

我们可以使用环境变量或卷将 ConfigMap 和 Secret 中的数据注入到我们的应用程序中。