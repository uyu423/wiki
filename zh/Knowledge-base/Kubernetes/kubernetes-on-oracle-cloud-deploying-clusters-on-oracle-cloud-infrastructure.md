---
title: Oracle 云上的 Kubernetes：在 Oracle 云基础设施上部署集群
description: 
published: true
date: 2023-02-01T11:57:50.415Z
tags: 
editor: markdown
dateCreated: 2023-02-01T11:57:46.961Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Kubernetes on Oracle Cloud: Deploying Clusters on Oracle Cloud Infrastructure***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-oracle-cloud-deploying-clusters-on-oracle-cloud-infrastructure)
{.links-list}


# Oracle 云上的 Kubernetes：在 Oracle 云基础设施上部署集群

Kubernetes 是一种流行的开源容器编排平台，可用于大规模部署和管理容器化应用程序。 Oracle Cloud Infrastructure (OCI) 是一个云计算平台，提供一系列服务，包括计算、存储和网络。

在本文中，我们将向您展示如何在 Oracle Cloud Infrastructure 上部署 Kubernetes 集群。我们将涵盖以下主题：

- 创建 Oracle Cloud Infrastructure 帐户
- 创建 Kubernetes 集群
- 在 Kubernetes 集群上部署示例应用程序

## 创建 Oracle 云基础设施帐户

如果您没有 Oracle Cloud Infrastructure 帐户，可以免费创建一个。创建一个帐户：

1. 前往[Oracle Cloud Infrastructure 注册页面](https://cloud.oracle.com/en_US/tryit)。
2. 输入您的信息并点击**创建账户**。
3. 按照说明验证您的帐户。

一旦您的帐户通过验证，您就可以登录到 [Oracle Cloud Infrastructure 控制台](https://console.us-ashburn-1.oraclecloud.com/a/billing)。

## 创建 Kubernetes 集群

 Oracle Cloud Infrastructure Container Engine for Kubernetes 是一项托管服务，可以轻松地在 Oracle Cloud Infrastructure 上部署和管理 Kubernetes 集群。使用 Container Engine for Kubernetes，您可以在几分钟内创建 Kubernetes 集群。

创建 Kubernetes 集群：

1. 登录[Oracle Cloud Infrastructure 控制台](https://console.us-ashburn-1.oraclecloud.com/a/billing)。
2. 在导航菜单中，单击 **Containers**，然后单击 **Container Clusters**。
3. 单击**创建集群**。
4. 输入以下信息：

- **名称**：输入集群的名称。
- **Kubernetes 版本**：选择您要使用的 Kubernetes 版本。
- **网络选项**：
  - **虚拟云网络**：创建一个新的虚拟云网络或选择一个现有的。
  - **子网**：创建新子网或选择现有子网。
  - **公共 IP 地址**：创建新的公共 IP 地址或选择现有 IP 地址。
- **节点池**：
  - **名称**：输入节点池的名称。
  - **Kubernetes 版本**：选择您要使用的 Kubernetes 版本。
  - **图像类型**：选择您要使用的图像类型。
  - **形状**：选择您要使用的形状。
  - **初始节点**：输入要创建的节点数。
  - **最大节点数**：输入您要允许的最大节点数。
  - **最小节点数**：输入您要允许的最小节点数。
- **存储选项**：
  - **存储类别**：选择您要使用的存储类别。
  - **大小 (GB)**：输入您要使用的存储大小。
- **节点元数据**：
  - **标签**：输入您要使用的任何标签。
  - **注释**：输入您要使用的任何注释。
- **节点污点**：输入您要使用的任何污点。
- **服务帐户**：输入您要使用的任何服务帐户。
- **RBAC**：选择您要使用的 RBAC 选项。

5. 单击**创建集群**。

创建集群需要几分钟时间。集群启动并运行后，您可以单击 **View Cluster** 以查看集群的详细信息。

## 在 Kubernetes 集群上部署示例应用程序

现在您已经启动并运行了 Kubernetes 集群，您可以在该集群上部署示例应用程序。要部署示例应用程序：

1. 登录[Oracle Cloud Infrastructure 控制台](https://console.us-ashburn-1.oraclecloud.com/a/billing)。
2. 在导航菜单中，单击 **Containers**，然后单击 **Container Clusters**。
3. 单击要部署应用程序的集群的名称。
4. 单击**部署应用程序**。
5. 输入以下信息：

- **应用程序类型**：选择您要部署的应用程序类型。
- **应用程序名称**：输入应用程序的名称。
- **图像名称**：输入您要使用的图像的名称。
- **图片标签**：输入您要使用的图片的标签。
- **镜像拉取策略**：选择您要使用的镜像拉取策略。
- **命令**：输入您要使用的命令。
- **参数**：输入您要使用的参数。
- **环境变量**：输入您要使用的环境变量。
- **工作目录**：输入您要使用的工作目录。
- **端口**：输入您要使用的端口。
- **服务帐户**：输入您要使用的服务帐户。
- **标签**：输入您要使用的标签。
- **注释**：输入您要使用的注释。
- **限制**：输入您要使用的限制。
- **请求**：输入您要使用的请求。

6. 单击**部署**。

部署应用程序需要几分钟时间。部署应用程序后，您可以单击**查看应用程序**以查看应用程序的详细信息。

## 结论

在本文中，我们向您展示了如何在 Oracle 云基础设施上部署 Kubernetes 集群。我们还向您展示了如何在 Kubernetes 集群上部署示例应用程序。