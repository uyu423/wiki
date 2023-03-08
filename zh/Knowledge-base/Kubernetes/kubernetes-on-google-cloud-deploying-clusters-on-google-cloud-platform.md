---
title: Google Cloud 上的 Kubernetes：在 Google Cloud Platform 上部署集群
description: 
published: true
date: 2023-02-14T05:33:12.838Z
tags: 
editor: markdown
dateCreated: 2023-02-14T05:33:05.640Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes on Google Cloud: Deploying Clusters on Google Cloud Platform***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-google-cloud-deploying-clusters-on-google-cloud-platform)
{.links-list}


# Google Cloud 上的 Kubernetes：在 Google Cloud Platform 上部署集群

Kubernetes 是一个开源系统，用于自动化容器化应用程序的部署、扩展和管理。它将构成应用程序的容器分组为逻辑单元，以便于管理和发现。 Kubernetes 托管在谷歌云平台 (GCP) 上，用于编排和管理部署在 GCP 上的容器。

GCP 上的 Kubernetes 是一种可扩展、可靠且经济高效的容器化应用部署方式。与其他云提供商相比，GCP 具有许多优势，包括即用即付定价、按分钟计费以及无预付费用。您还可以使用 GCP 上的 Kubernetes 来管理本地工作负载。

在本文中，我们将向您展示如何在 GCP 上部署 Kubernetes 集群。我们还将向您展示如何在 Kubernetes 集群上部署一个简单的应用程序。

## 先决条件

- 一个谷歌云账户
- 在 Google Cloud Console 中创建的项目
- 安装在本地计算机上的 gcloud 命令行工具
- Kubernetes 基础知识

## 创建 Kubernetes 集群

Kubernetes 集群由一组节点组成，每个节点都是运行 Kubernetes 组件的物理机或虚拟机。 Kubernetes 集群中有两种类型的节点：

- **主节点**：这些节点负责管理 Kubernetes 集群。它们提供 API 服务器、调度程序和控制器管理器组件。
- **工作节点**：这些节点运行部署在 Kubernetes 集群上的应用程序。

在本节中，我们将向您展示如何创建具有三个节点的 Kubernetes 集群：一个主节点和两个工作节点。

### 创建主节点

1. 登录 Google Cloud Console 并转到 **Compute Engine** > **VM instances** 页面。
2. 单击**创建实例**按钮。
3. 在**名称**字段中，输入**kubernetes-master**。
4. 在**区域**字段中，选择一个靠近您所在位置的区域。
5. 在**机器类型**字段中，选择**n1-standard-1**。
6. 在**启动磁盘**部分，单击**更改**。
7. 在 **Boot disk** 部分，从 **Operating system** 下拉列表中选择 **Ubuntu 16.04 LTS**。
8. 在**启动磁盘类型**下拉列表中，选择**SSD（永久磁盘）**。
9. 在**引导磁盘大小**字段中，输入**10GB**。
10. 单击**选择**按钮。
11. 在 **防火墙** 部分，选中 **允许 HTTP 流量** 复选框。
12. 单击**创建**按钮。

现在应该创建您的主节点。

### 创建工作节点

1. 登录 Google Cloud Console 并转到 **Compute Engine** > **VM instances** 页面。
2. 单击**创建实例**按钮。
3. 在**名称**字段中，输入**kubernetes-worker-1**。
4. 在 **Zone** 字段中，选择您为主节点选择的相同区域。
5. 在**机器类型**字段中，选择**n1-standard-1**。
6. 在**启动磁盘**部分，单击**更改**。
7. 在 **Boot disk** 部分，从 **Operating system** 下拉列表中选择 **Ubuntu 16.04 LTS**。
8. 在**启动磁盘类型**下拉列表中，选择**SSD（永久磁盘）**。
9. 在**引导磁盘大小**字段中，输入**10GB**。
10. 单击**选择**按钮。
11. 在 **防火墙** 部分，选中 **允许 HTTP 流量** 复选框。
12. 单击**创建**按钮。

重复上述步骤创建第二个工作节点，但使用 **kubernetes-worker-2** 作为第二个节点的名称。

现在应该创建您的工作节点。

## 安装 Kubernetes

在本节中，我们将向您展示如何在主节点上安装 Kubernetes。

1. 使用 SSH 登录到您的主节点。
2. 运行以下命令添加Kubernetes apt仓库：

```
$ sudo apt-get install -y apt-transport-https
3. Run the following command to add the Kubernetes GPG key:

```
$ curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key 添加 -
4. 运行以下命令添加 Kubernetes 存储库：

```
$ sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
5. Update the package list:

```
$ sudo apt-get 更新
6. 安装 Kubernetes：

```
$ sudo apt-get install -y kubelet kubeadm kubectl
7. Once the installation is complete, run the following command to start the Kubernetes master node:

```
$ 须藤 kubeadm 初始化
8. 运行以下命令配置 kubectl：

```
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config
9. Your Kubernetes master node should now be up and running.

## Joining Worker Nodes to the Cluster

In this section, we will show you how to join your worker nodes to the Kubernetes cluster.

1. Log in to your master node using SSH.
2. Run the following command to get the join command:

```
$ sudo kubeadm token create --print-join-command
3. 使用 SSH 登录到您的工作程序节点。
4. 在每个工作节点上运行您在上一步中获得的加入命令。
5. 您的工作节点现在应该加入 Kubernetes 集群。

## 部署应用程序

在本节中，我们将向您展示如何在 Kubernetes 集群上部署一个简单的应用程序。

1. 使用 SSH 登录到您的主节点。
2. 创建一个名为 **nginx-deployment.yaml** 的文件，内容如下：

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
3. Run the following command to deploy the application:

```
$ kubectl create -f nginx-deployment.yaml
4. 运行以下命令列出已部署的 pod：

```
$ kubectl get pods
5. Run the following command to expose the deployment:

```
$ kubectl 公开部署 nginx-deployment --type=LoadBalancer --port=80 --target-port=80
6. 运行以下命令获取服务 URL：

```
$ kubectl get service nginx-deployment
7. Access the application using the service URL. You should see the default Nginx page.

Your application is now deployed on your Kubernetes cluster.

## Deleting the Cluster

In this section, we will show you how to delete the Kubernetes cluster.

1. Log in to your master node using SSH.
2. Run the following command to delete the cluster:

```
$ 须藤 kubeadm 重置
3.删除主节点：

```
$ gcloud compute instances delete kubernetes-master
4. Delete the worker nodes:

```
$ gcloud 计算实例删除 kubernetes-worker-1
$ gcloud 计算实例删除 kubernetes-worker-2
5. 现在应该删除您的 Kubernetes 集群。

## 结论

在本文中，我们向您展示了如何在 GCP 上部署 Kubernetes 集群。我们还向您展示了如何在 Kubernetes 集群上部署一个简单的应用程序。