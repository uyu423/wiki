---
title: Kubernetes API：通过 REST 请求与集群交互
description: 
published: true
date: 2023-02-14T03:33:33.231Z
tags: 
editor: markdown
dateCreated: 2023-02-14T03:33:30.961Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes API: Interacting with Your Cluster with REST Requests***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-api-interacting-with-your-cluster-with-rest-requests)
{.links-list}


# Kubernetes API：使用 REST 请求与集群交互

在本文中，我们将了解如何使用 Kubernetes API 与您的 Kubernetes 集群进行交互。我们将介绍向 Kubernetes API 发出 REST 请求的基础知识，并将研究一些最常见的 API 资源和操作。

## 发出 REST 请求

Kubernetes API 是一个 [RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer) API，这意味着您可以使用任何 HTTP 客户端向 API 发出请求。您需要做的就是向适当的 API 端点发送 HTTP 请求，Kubernetes API 将使用请求的数据进行响应。

要向 Kubernetes API 发出请求，您需要知道要调用的 API 端点的 URL，并且需要指定要使用的 HTTP 方法。最常见的 HTTP 方法是“GET”、“POST”、“PUT”和“DELETE”。

例如，要获取命名空间中所有 pod 的列表，您可以向 `/api/v1/namespaces/{namespace}/pods` 端点发出 `GET` 请求。要创建新的 pod，您可以向同一端点发出 POST 请求。

除了 URL 和 HTTP 方法之外，您还需要指定一个名为 `Authorization` 的 [HTTP 标头](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)，其值为 `Bearer {token}`，其中 `{token}` 是有效的 Kubernetes API 令牌。您可以通过运行“kubectl get secrets”命令来获取 Kubernetes API 令牌。

## 通用 API 资源

现在我们已经介绍了向 Kubernetes API 发出 REST 请求的基础知识，让我们来看看一些最常见的 API 资源。

### 豆荚

Pod 是 Kubernetes 中最小的可部署单元，它们总是在同一个节点上共同定位和共同调度。 Pod 表示应用程序的单个实例，它可以包含一个或多个容器。

要获取命名空间中所有 pod 的列表，您可以向 `/api/v1/namespaces/{namespace}/pods` 端点发出 `GET` 请求。要获取特定 pod 的详细信息，您可以向 `/api/v1/namespaces/{namespace}/pods/{name}` 端点发出 `GET` 请求。

要创建新的 pod，您可以向 `/api/v1/namespaces/{namespace}/pods` 端点发出 `POST` 请求。请求正文应该是指定 pod 规范的 [JSON](https://www.json.org/) 或 [YAML](https://yaml.org/) 对象。

以下是 JSON 格式的 pod 规范示例：

```json
{
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "nginx-pod",
    "labels": {
      "app": "nginx"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "nginx",
        "image": "nginx:1.7.9",
        "ports": [
          {
            "containerPort": 80
          }
        ]
      }
    ]
  }
}
```

这是 YAML 中的相同规范：

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.7.9
    ports:
    - containerPort: 80
```

要更新 pod，您可以向 `/api/v1/namespaces/{namespace}/pods/{name}` 端点发出 `PUT` 或 `PATCH` 请求。请求正文应该是指定 pod 规范的 JSON 或 YAML 对象。

要删除 pod，您可以向 `/api/v1/namespaces/{namespace}/pods/{name}` 端点发出 `DELETE` 请求。

### 副本集

副本集是一种 [Kubernetes 资源](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)，可确保指定数量的 pod 副本始终运行。如果一个 pod 被删除或崩溃，副本集将确保创建一个新的 pod 来替换它。

要获取命名空间中所有副本集的列表，您可以向 `/apis/apps/v1/namespaces/{namespace}/replicasets` 端点发出 `GET` 请求。要获取特定副本集的详细信息，您可以向 `/apis/apps/v1/namespaces/{namespace}/replicasets/{name}` 端点发出 `GET` 请求。

要创建新的副本集，您可以向 `/apis/apps/v1/namespaces/{namespace}/replicasets` 端点发出 `POST` 请求。请求正文应该是指定副本集规范的 JSON 或 YAML 对象。

以下是 JSON 格式的副本集规范示例：

```json
{
  "apiVersion": "apps/v1",
  "kind": "ReplicaSet",
  "metadata": {
    "name": "nginx-replicaset",
    "labels": {
      "app": "nginx"
    }
  },
  "spec": {
    "replicas": 3,
    "selector": {
      "matchLabels": {
        "app": "nginx"
      }
    },
    "template": {
      "metadata": {
        "labels": {
          "app": "nginx"
        }
      },
      "spec": {
        "containers": [
          {
            "name": "nginx",
            "image": "nginx:1.7.9",
            "ports": [
              {
                "containerPort": 80
              }
            ]
          }
        ]
      }
    }
  }
}
```

这是 YAML 中的相同规范：

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

要更新副本集，您可以向“/apis/apps/v1/namespaces/{namespace}/replicasets/{name}”端点发出“PUT”或“PATCH”请求。请求正文应该是指定副本集规范的 JSON 或 YAML 对象。

要删除副本集，您可以向 `/apis/apps/v1/namespaces/{namespace}/replicasets/{name}` 端点发出 `DELETE` 请求。

### 部署

[部署](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) 是一种更高级别的资源，用于管理副本集并提供一种声明性方式来指定 Pod 的所需状态。部署定义了一个副本集，并确保指定数量的副本始终在运行。

要获取命名空间中所有部署的列表，您可以向 `/apis/apps/v1/namespaces/{namespace}/deployments` 端点发出 `GET` 请求。要获取特定部署的详细信息，您可以向 `/apis/apps/v1/namespaces/{namespace}/deployments/{name}` 端点发出 `GET` 请求。

要创建新部署，您可以向 `/apis/apps/v1/namespaces/{namespace}/deployments` 端点发出 `POST` 请求。请求正文应该是指定部署规范的 JSON 或 YAML 对象。

以下是 JSON 格式的部署规范示例：

```json
{
  "apiVersion": "apps/v1",
  "kind": "Deployment",
  "metadata": {
    "name": "nginx-deployment",
    "labels": {
      "app": "nginx"
    }
  },
  "spec": {
    "replicas": 3,
    "selector": {
      "matchLabels": {
        "app": "nginx"
      }
    },
    "template": {
      "metadata": {
        "labels": {
          "app": "nginx"
        }
      },
      "spec": {
        "containers": [
          {
            "name": "nginx",
            "image": "nginx:1.7.9",
            "ports": [
              {
                "containerPort": 80
              }
            ]
          }
        ]
      }
    }
  }
}
```

这是 YAML 中的相同规范：

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

要更新部署，您可以向“/apis/apps/v1/namespaces/{namespace}/deployments/{name}”端点发出“PUT”或“PATCH”请求。请求正文应该是指定部署规范的 JSON 或 YAML 对象。

要删除部署，您可以向 `/apis/apps/v1/namespaces/{namespace}/deployments/{name}` 端点发出 `DELETE` 请求。

## 结论

在本文中，我们介绍了使用 REST 请求与 Kubernetes API 交互的基础知识。我们已经查看了一些最常见的 API 资源，并且了解了如何使用 Kubernetes API 来创建、读取、更新和删除这些资源。