---
title: DigitalOcean 上的 Kubernetes：在 DigitalOcean 上部署集群
description: 
published: true
date: 2023-02-17T18:03:01.336Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:26:55.617Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Kubernetes on DigitalOcean: Deploying Clusters on DigitalOcean***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-digitalocean-deploying-clusters-on-digitalocean)
{.links-list}


# Kubernetes on DigitalOcean：在 DigitalOcean 上部署集群

Kubernetes 是一个开源容器编排平台，可自动部署、扩展和管理容器化应用程序。它具有可移植性和可扩展性，为构建集群管理解决方案提供了基础。

DigitalOcean 是一个云计算平台，提供虚拟专用服务器 (VPS) 和其他云服务。它是托管 Web 应用程序和微服务的流行选择。

本文概述了在 DigitalOcean 上部署 Kubernetes 集群。它涵盖供应资源、配置网络和部署应用程序。

## 配置资源

DigitalOcean 提供了 Kubernetes 服务，可以轻松配置资源和部署 Kubernetes 集群。第一步是创建一个 Kubernetes 集群。这可以通过控制面板或 API 完成。

创建集群后，您需要向其添加节点。可以手动或自动添加节点。自动节点供应可用于具有三个或更多节点的集群。

## 配置网络

DigitalOcean 上的 Kubernetes 集群默认部署在私有网络中。该网络与公共 Internet 隔离，只能从集群内部访问。

要访问 Internet 上的服务，您需要配置网关。这可以通过 Kubernetes 仪表板或 API 完成。

如果您需要访问本地服务，则需要配置 VPN。 DigitalOcean 提供可用于连接到本地资源的 IPsec VPN 服务。

## 部署应用程序

要在 Kubernetes 集群上部署应用程序，您需要创建部署。这可以通过 Kubernetes 仪表板或 API 完成。

创建部署后，您需要指定要使用的容器映像和要公开的端口。您还可以指定环境变量和其他选项。

创建部署后，您将需要创建服务。这会将部署暴露给外界。该服务可以通过 Kubernetes 仪表板或 API 创建。

创建服务后，您需要指定服务类型（LoadBalancer、ClusterIP 或 NodePort）以及要公开的端口。您还可以指定其他选项，例如服务名称。

## 结论

本文涵盖了在 DigitalOcean 上部署 Kubernetes 集群的基础知识。它展示了如何供应资源、配置网络和部署应用程序。