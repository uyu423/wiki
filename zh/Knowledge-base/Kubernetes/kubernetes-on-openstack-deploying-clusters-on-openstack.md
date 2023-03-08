---
title: OpenStack 上的 Kubernetes：在 OpenStack 上部署集群
description: 
published: true
date: 2023-02-14T06:32:48.790Z
tags: 
editor: markdown
dateCreated: 2023-02-14T06:32:47.087Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes on OpenStack: Deploying Clusters on OpenStack***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-openstack-deploying-clusters-on-openstack)
{.links-list}


# OpenStack 上的 Kubernetes：在 OpenStack 上部署集群

OpenStack 是一种云操作系统，可控制整个数据中心的大型计算、存储和网络资源池，所有这些资源均通过仪表板进行管理，使管理员能够进行控制，同时使用户能够通过 Web 界面配置资源。

Kubernetes 是一个开源系统，用于自动部署、扩展和管理容器化应用程序。

本文的目的是向您展示如何在 OpenStack 上部署 Kubernetes 集群。我们将涵盖以下主题：

- 先决条件
- 创建 Kubernetes 集群
- 在集群上部署应用程序

## 先决条件

为了遵循本指南，您需要具备以下条件：

- 具有以下内容的 OpenStack 云：
  - 一个网络
  - 路由器
  - 一个子网
  - 一个安全组
  - 一对密钥
  - 至少3个计算节点
- 安装并配置了 OpenStack CLI
- 安装并配置了 Kubernetes CLI

## 创建 Kubernetes 集群

我们将使用“kube-up.sh”脚本来部署 Kubernetes 集群。该脚本将在 OpenStack 上创建所有必要的资源，包括计算实例、网络和负载平衡器。

首先，克隆 Kubernetes 存储库：

```
git clone https://github.com/kubernetes/kubernetes.git
```

接下来，切换到 `kubernetes/cluster/openstack` 目录：

```
cd kubernetes/cluster/openstack
```

然后，创建一个名为“cloud-config.yaml”的文件，其中包含以下内容：

```yaml
#cloud-config

write_files:
- owner: root:root
  path: /etc/kubernetes/kube-up-config.yaml
  content: |
    CLOUD_PROVIDER=openstack
    OPENSTACK_AUTH_URL=https://identity.example.com:5000/v3
    OPENSTACK_USERNAME=admin
    OPENSTACK_PASSWORD=admin
    OPENSTACK_TENANT_NAME=admin
    OPENSTACK_REGION=regionOne
    OPENSTACK_CLUSTER_NAME=kubernetes
    OPENSTACK_CLUSTER_SIZE=3
    OPENSTACK_MASTER_FLAVOR=m1.small
    OPENSTACK_MASTER_IMAGE=ubuntu-16.04-x86_64-20170119
    OPENSTACK_WORKER_FLAVOR=m1.small
    OPENSTACK_WORKER_IMAGE=ubuntu-16.04-x86_64-20170119
    OPENSTACK_NETWORK_NAME=kubernetes
    OPENSTACK_MASTER_OS_DISTRIBUTION=ubuntu
    OPENSTACK_WORKER_OS_DISTRIBUTION=ubuntu
```

将此文件中的值替换为您自己的 OpenStack 凭据和设置。

现在，您可以通过运行“kube-up.sh”脚本来部署集群：

```
./kube-up.sh
```

这将需要几分钟才能完成。完成后，您应该会在 OpenStack 仪表板中看到 3 个计算实例，以及一个网络、路由器和负载均衡器。

## 在集群上部署应用

现在我们已经在 OpenStack 上启动并运行了一个 Kubernetes 集群，让我们在上面部署一个简单的应用程序。我们将为“Hello, World”Web 应用程序使用预构建的容器映像。

首先，我们需要创建一个名为“hello-world.yaml”的文件，其中包含以下内容：

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
  labels:
    app: hello-world
spec:
  replicas: 3
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: tutum/hello-world
        ports:
        - containerPort: 80
```

此文件定义了一个名为“hello-world”的部署，其中包含 3 个副本 pod。 Pod 将从“tutum/hello-world”容器镜像创建，这是一个简单的“Hello, World”Web 应用程序。 Pod 将暴露在端口 80 上。

我们现在可以通过运行以下命令来部署此应用程序：

```
kubectl create -f hello-world.yaml
```

这将需要几秒钟来创建 pod。一旦它们启动并运行，我们就可以通过创建服务将它们暴露给外界：

```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-world
  labels:
    app: hello-world
spec:
  type: LoadBalancer
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: hello-world
```

将此文件保存为“hello-world-service.yaml”并使用以下命令部署它：

```
kubectl create -f hello-world-service.yaml
```

这将创建一个负载均衡器并在端口 80 上公开服务。您可以通过运行以下命令找到负载均衡器的公共 IP 地址：

```
kubectl get service hello-world
```

您应该会看到类似于以下内容的输出：

```
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP       PORT(S)        AGE
hello-world  LoadBalancer   10.0.0.1        1.2.3.4           80:31527/TCP   1m
```

您现在可以通过在 Web 浏览器中访问负载均衡器的公共 IP 地址来访问“Hello, World”Web 应用程序。

## 结论

在本文中，我们向您展示了如何在 OpenStack 上部署 Kubernetes 集群。我们还向您展示了如何在集群上部署一个简单的 Web 应用程序。

如需进一步阅读，请查看以下资源：

- [OpenStack 上的 Kubernetes：参考架构](https://www.openstack.org/assets/pdf/kubernetes-on-openstack-a-reference-architecture.pdf)
- [在 OpenStack 上部署 Kubernetes](https://www.mirantis.com/blog/deploying-kubernetes-on-openstack/)
- [Kubernetes 困难之路](https://github.com/kelseyhightower/kubernetes-the-hard-way)