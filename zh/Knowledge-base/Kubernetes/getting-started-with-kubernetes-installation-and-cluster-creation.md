---
title: Kubernetes 入门：安装和集群创建
description: 
published: true
date: 2023-02-08T17:32:54.390Z
tags: 
editor: markdown
dateCreated: 2023-02-08T17:32:52.667Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Getting Started with Kubernetes: Installation and Cluster Creation***English** document is available*](/en/Knowledge-base/Kubernetes/getting-started-with-kubernetes-installation-and-cluster-creation)
{.links-list}


# Kubernetes 入门：安装和集群创建

Kubernetes 是一个强大的容器编排工具，可以帮助您自动化部署、扩展和管理容器化应用程序。在本文中，我们将向您展示如何在本地机器上安装 Kubernetes 并创建 Kubernetes 集群。

## 先决条件

在开始之前，您需要具备以下条件：

- 运行 Linux 或 Windows 的本地计算机
- [Docker](https://docs.docker.com/install/) 安装并运行
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) 安装
- [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/) 安装

## 安装 Kubernetes

可以使用 Minikube 在本地机器上安装 Kubernetes。 Minikube 是一个轻量级的 Kubernetes 实现，可用于开发和测试目的。

要使用 Minikube 安装 Kubernetes，请运行以下命令：

```
$ minikube start
```

这将启动一个虚拟机并在其上安装 Kubernetes。安装完成后，您可以通过运行以下命令来验证安装：

```
$ kubectl get nodes
```

此命令应列出由 Minikube 创建的节点。

## 创建 Kubernetes 集群

现在 Kubernetes 已启动并运行，您可以创建 Kubernetes 集群。为此，您需要创建一个[部署](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) 和一个[服务](https://kubernetes.io/docs/concepts /服务网络/服务/）。

部署是一个 Kubernetes 对象，它描述了一组 pod 的期望状态。服务是将一组 pod 暴露给外界的 Kubernetes 对象。

要创建部署和服务，您需要创建一个包含以下内容的 [YAML](https://en.wikipedia.org/wiki/YAML) 文件：

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
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
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  ports:
  - port: 80
    nodePort: 30000
  selector:
    app: nginx
```

在这个文件中，我们定义了一个部署，其中包含 [nginx](https://www.nginx.com/) 容器的三个副本，以及一个向外界公开部署的服务。

要创建部署和服务，请运行以下命令：

```
$ kubectl apply -f deployment.yaml
```

这将创建部署和服务。您可以通过运行以下命令来验证部署和服务是否已创建：

```
$ kubectl get deployments
```

```
$ kubectl get services
```

## 访问 Kubernetes 集群

现在已经创建了部署和服务，您可以从本地计算机访问 Kubernetes 集群。为此，您需要获取 Minikube 虚拟机的 IP 地址和服务的节点端口。

要获取 Minikube 虚拟机的 IP 地址，请运行以下命令：

```
$ minikube ip
```

要获取服务的节点端口，请运行以下命令：

```
$ kubectl describe service nginx-service
```

您应该看到以下输出：

```
Name:              nginx-service
Namespace:         default
Labels:            <none>
Annotations:       <none>
Selector:          app=nginx
Type:              NodePort
IP:                10.0.0.1
Port:              <unnamed>  80/TCP
TargetPort:        80/TCP
NodePort:          <unnamed>  30000/TCP
Endpoints:         10.0.0.2:80,10.0.0.3:80,10.0.0.4:80
Session Affinity:  None
External Traffic Policy:  Cluster
Events:            <none>
```

节点端口是 `NodePort` 字段的值。在这种情况下，节点端口是“30000”。

要访问 Kubernetes 集群，请打开 Web 浏览器并转到“http://<minikube-ip>:<node-port>”。在我们的示例中，URL 为“http://10.0.0.1:30000”。

你应该看到默认的 nginx 页面：

![nginx](https://www.nginx.com/wp-content/uploads/2018/08/nginx-logo.png)

## 删除 Kubernetes 集群

要删除 Kubernetes 集群，请运行以下命令：

```
$ minikube delete
```

这将删除 Minikube 虚拟机和在前面的步骤中创建的所有资源。

## 结论

在本文中，我们向您展示了如何在本地计算机上安装 Kubernetes 并创建 Kubernetes 集群。 Kubernetes 是一个强大的工具，可以帮助您自动化容器化应用程序的部署、扩展和管理。