---
title: 带有 Istio 的 Kubernetes：为您的应用程序实施服务网格
description: 
published: true
date: 2023-02-02T05:44:02.961Z
tags: 
editor: markdown
dateCreated: 2023-02-02T05:43:58.533Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes with Istio: Implementing Service Mesh for Your Applications***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-istio-implementing-service-mesh-for-your-applications)
{.links-list}


# Kubernetes with Istio：为您的应用程序实施服务网格

Kubernetes 是一个开源系统，用于自动管理容器化应用程序。 Istio 是一个用于连接、管理和保护微服务的开放平台。

服务网格是微服务应用程序的可配置基础设施层，它使服务之间的通信可靠、快速和安全。服务网格通常由数据平面和控制平面组成。数据平面由一组调节微服务之间通信的智能代理组成。控制平面管理和配置代理。

Istio 是 Kubernetes 的服务网格。它由数据平面和控制平面组成。数据平面由一组调节微服务之间通信的智能代理组成。控制平面管理和配置代理。

带有 Istio 的 Kubernetes 可用于为您的应用程序实施服务网格。在本文中，我们将向您展示如何在 Kubernetes 集群上安装和配置 Istio，以及如何部署示例微服务应用程序。

## 在 Kubernetes 上安装 Istio

Istio 可以使用 Helm 包管理器安装在 Kubernetes 集群上。 Helm 是用于管理 Kubernetes 应用程序的工具。

要安装 Istio，您需要先安装 Helm 并添加 Istio Helm 存储库。

### 安装头盔

从 [Helm 网站](https://helm.sh/docs/using_helm/# installing-helm) 下载 Helm 二进制文件。

提取 helm 二进制文件并将其添加到您的 PATH 中。

```
tar xzf helm-v2.16.5-linux-amd64.tar.gz
sudo mv linux-amd64/helm /usr/local/bin/
```

初始化 Helm 并安装 Tiller，这是 Helm 的服务器端组件。

```
helm init
```

### 添加 Istio Helm 存储库

添加 Istio Helm 存储库。

```
helm repo add istio.io https://storage.googleapis.com/istio-release/releases/1.5.2/charts/
```

更新 Helm 存储库。

```
helm repo update
```

## 部署示例微服务应用程序

我们将部署一个包含四个服务的示例微服务应用程序：

- 用 Node.js 编写的前端服务
- 用 Golang 编写的后端服务
- 数据库服务
- 负载均衡器服务

前端和后端服务将部署在不同的 pod 中。数据库服务将部署在一个单独的 pod 中。负载均衡器服务将部署在一个单独的 pod 中。

前端服务将向后端服务发出请求。后端服务将向数据库服务发出请求。负载均衡器服务会将流量路由到前端和后端服务。

我们将使用 Istio Helm chart 部署应用程序。

### 安装 Istio Helm Chart

使用以下命令安装 Istio Helm chart：

```
helm install --name istio-system -f /path/to/custom-values.yaml istio.io/istio
```

Istio Helm chart 安装在 istio-system 命名空间中。

### 部署前端服务

为前端服务创建一个 pod。

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: frontend
  labels:
    app: frontend
spec:
  containers:
  - name: frontend
    image: node:12-alpine
    ports:
    - containerPort: 3000
```

部署吊舱。

```
kubectl apply -f /path/to/frontend-pod.yaml
```

### 部署后端服务

为后端服务创建一个 pod。

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: backend
  labels:
    app: backend
spec:
  containers:
  - name: backend
    image: golang:1.14-alpine
    ports:
    - containerPort: 3000
```

部署吊舱。

```
kubectl apply -f /path/to/backend-pod.yaml
```

### 部署数据库服务

为数据库服务创建一个 pod。

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: database
  labels:
    app: database
spec:
  containers:
  - name: database
    image: mysql:5.7
    ports:
    - containerPort: 3306
```

部署吊舱。

```
kubectl apply -f /path/to/database-pod.yaml
```

### 部署负载均衡器服务

为负载均衡器服务创建一个 pod。

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: load-balancer
  labels:
    app: load-balancer
spec:
  containers:
  - name: load-balancer
    image: nginx:1.17.9-alpine
    ports:
    - containerPort: 80
```

部署吊舱。

```
kubectl apply -f /path/to/load-balancer-pod.yaml
```

### 测试应用程序

为了测试应用程序，我们将向负载均衡器服务发送请求。负载均衡器服务会将请求路由到前端服务。前端服务将向后端服务发出请求。后端服务将向数据库服务发出请求。

首先，我们需要获取负载均衡器服务的 IP 地址。

```
kubectl get svc
```

输出应如下所示：

```
NAME            TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
frontend        ClusterIP      10.108.1.194     <none>        3000/TCP         1m
backend         ClusterIP      10.96.247.199    <none>        3000/TCP         1m
database        ClusterIP      10.111.142.247   <none>        3306/TCP         1m
load-balancer   LoadBalancer   10.102.129.251   <pending>     80:32000/TCP     1m
```

负载均衡器服务的“ClusterIP”为“10.102.129.251”，“PORT”为“80:32000”。

我们现在可以向负载均衡器服务发送请求。

```
curl -v http://10.102.129.251:80
```

输出应如下所示：

```
*   Trying 10.102.129.251:80...
* TCP_NODELAY set
* Connected to 10.102.129.251 (10.102.129.251) port 80 (#0)
> GET / HTTP/1.1
> Host: 10.102.129.251:80
> User-Agent: curl/7.64.1
> Accept: */*
>
< HTTP/1.1 200 OK
< Content-Type: text/html
< Content-Length: 28
<
<html>
<body>
Hello, World!
</body>
</html>
* Connection #0 to host 10.102.129.251 left intact
```

请求被路由到前端服务并返回响应。

## 结论

在本文中，我们向您展示了如何在 Kubernetes 集群上安装和配置 Istio，以及如何部署示例微服务应用程序。 Istio 可用于为您的应用程序实施服务网格。