---
title: 私有云上的 Kubernetes：在您自己的基础设施上部署集群
description: 
published: true
date: 2023-02-14T07:32:42.017Z
tags: 
editor: markdown
dateCreated: 2023-02-14T07:32:40.467Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes on Private Clouds: Deploying Clusters on Your Own Infrastructure***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-private-clouds-deploying-clusters-on-your-own-infrastructure)
{.links-list}


# 私有云上的 Kubernetes：在您自己的基础设施上部署集群

Kubernetes 是一种开源容器编排工具，近年来因其能够自动部署、扩展和管理容器化应用程序而广受欢迎。

虽然 Kubernetes 可以部署在亚马逊网络服务 (AWS)、谷歌云平台 (GCP) 和微软 Azure 等公共云上，但出于安全、成本或数据主权等原因，许多组织更愿意在自己的私有基础设施上运行 Kubernetes。

本文将概述 Kubernetes 容器编排工具，并向您展示如何在您自己的基础设施上部署 Kubernetes 集群，无论是在本地还是在私有云中。

## 什么是 Kubernetes？

Kubernetes 是一个可移植、可扩展的开源平台，用于管理容器化工作负载和服务，可促进声明式配置和自动化。它有一个庞大的、快速发展的生态系统。 Kubernetes 服务、支持和工具广泛可用。

Kubernetes 最初由 Google 设计，现在由 Cloud Native Computing Foundation 维护。

## Kubernetes 的特点

Kubernetes 的一些关键特性包括：

- 容器化应用程序的自动部署和扩展
- 负载均衡和服务发现
- 存储编排
- 自我修复
- 秘密和配置管理

## Kubernetes 的好处

使用 Kubernetes 有很多好处，包括：

- 提高效率：通过自动化容器化应用程序的部署、扩展和管理，Kubernetes 可以帮助您提高开发和运营团队的效率。
- 提高正常运行时间：Kubernetes 的自我修复能力可以通过自动重启崩溃的容器和复制失败的容器来帮助您提高应用程序的正常运行时间。
- 提高敏捷性：Kubernetes 的声明式配置和自动化可以让您快速部署和更新应用程序，从而帮助您提高开发过程的敏捷性。
- 降低运营成本：通过自动化容器化应用程序的管理，Kubernetes 可以帮助您降低基础架构的运营成本。

## Kubernetes 架构

Kubernetes 是一个包含各种组件的复杂系统。以下是 Kubernetes 架构的高级概述：

- 主节点是 Kubernetes 集群的核心。它负责管理集群并维护集群状态的记录。主节点由以下组件组成：
  - API 服务器是 Kubernetes 集群的中心通信点。它负责暴露 Kubernetes API 和处理 API 请求。
  - Scheduler 负责调度 pod 在集群中的节点上运行。
  - Controller Manager 负责管理集群的状态。
- Worker Nodes 是 Kubernetes 集群中实际部署 pod 的节点。集群中的每个 pod 都部署在一个 Worker Node 上。

## Kubernetes 组件

Kubernetes 由许多组件组成，每个组件在 Kubernetes 集群的运行中都扮演着特定的角色。以下是 Kubernetes 组件的简要概述：

- API 服务器是 Kubernetes 集群的中心通信点。它负责暴露 Kubernetes API 和处理 API 请求。
- Scheduler 负责调度 pod 在集群中的节点上运行。
- Controller Manager 负责管理集群的状态。
- Etcd组件负责存储Kubernetes集群的配置数据。
- Kubelet 负责在 Kubernetes 集群中的节点上运行 pod。
- Kube-Proxy 负责将流量路由到 Kubernetes 集群中的正确 Pod。

## 在您自己的基础设施上部署 Kubernetes

有多种方法可以在您自己的基础设施上部署 Kubernetes。以下是一些最流行的方法：

- 使用特定于 Kubernetes 的解决方案，例如 Canonical 的 MicroK8s、Red Hat OpenShift 或 VMware Tanzu Kubernetes Grid Integrated Edition (TKGI)。
- 使用与云无关的解决方案，例如 Hashicorp Terraform、Puppet 或 Ansible。
- 使用特定于云的解决方案，例如 Amazon Web Services (AWS) CloudFormation、Google Cloud Platform (GCP) Deployment Manager 或 Azure Resource Manager (ARM) Templates。

## 结论

Kubernetes 是一个强大的容器编排工具，可以帮助您提高开发和运营团队的效率和敏捷性。 Kubernetes 可以部署在 AWS、GCP 和 Azure 等公共云上，也可以部署在您自己的私有基础设施上。

本文概述了 Kubernetes 容器编排工具，并向您展示了如何在您自己的基础架构上部署 Kubernetes 集群。