---
title: 带有 CNI 的 Kubernetes：为您的集群配置网络
description: 
published: true
date: 2023-02-05T14:17:33.180Z
tags: 
editor: markdown
dateCreated: 2023-02-05T14:17:26.761Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes with CNI: Configuring Networking for Your Clusters***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-cni-configuring-networking-for-your-clusters)
{.links-list}


# 带有 CNI 的 Kubernetes：为您的集群配置网络

Kubernetes 是一个强大的容器管理系统，使开发人员能够在云原生环境中部署和管理可扩展的应用程序。为了运行 Kubernetes 集群，开发人员需要为他们的应用程序配置网络。这可以使用容器网络接口 (CNI) 来完成。

CNI 是一个提供 API 的库，用于简化容器网络接口的配置。它旨在与 Kubernetes 等容器运行时一起使用，为开发人员提供一致的网络配置体验。 CNI 提供可移植和可扩展的网络配置解决方案，可以与任何容器运行时一起使用。

在本文中，我们将向您展示如何使用 CNI 为 Kubernetes 集群配置网络。我们将涵盖以下主题：

- 什么是 CNI？
- CNI 是如何工作的？
- 如何使用 CNI 为 Kubernetes 配置网络？

## 什么是 CNI？

CNI 是一个提供 API 的库，用于简化容器网络接口的配置。它旨在与 Kubernetes 等容器运行时一起使用，为开发人员提供一致的网络配置体验。 CNI 提供可移植和可扩展的网络配置解决方案，可以与任何容器运行时一起使用。

## CNI 是如何工作的？

CNI 通过为每个容器创建一个网络命名空间来工作。网络名称空间是一个虚拟环境，包含其自己的网络配置。这使每个容器都有自己的 IP 地址和网络配置。然后 CNI 使用插件为每个容器配置网络接口。

有两种类型的 CNI 插件：

- **网络**插件：这些插件为容器配置网络接口。
- **IPAM** 插件：这些插件为容器分配 IP 地址。

## 如何使用 CNI 为 Kubernetes 配置网络？

Kubernetes 使用 CNI 为容器配置网络。为了在 Kubernetes 中使用 CNI，您需要安装一个 CNI 插件。有许多可用的 CNI 插件，例如 flannel、Weave Net 和 Calico。

在本节中，我们将向您展示如何安装和配置 flannel CNI 插件。

### 安装法兰绒 CNI 插件

Flannel CNI 插件可从 CNI GitHub 存储库获得。要安装该插件，您需要下载二进制文件并将其放在 `$PATH` 中。

```
$ wget https://github.com/containernetworking/cni/releases/download/v0.6.0/cni-amd64-v0.6.0.tgz
$ tar -xvzf cni-amd64-v0.6.0.tgz -C /usr/local/bin/
```

### 配置法兰绒 CNI 插件

安装 flannel CNI 插件后，您需要对其进行配置。 flannel CNI 插件使用配置文件来配置网络。配置文件为JSON格式，包含以下字段：

- `name`：网络的名称。
- `type`：网络的类型。 flannel CNI 插件支持 `flannel` 类型。
- `delegate`：要使用的委托 CNI 插件。 flannel CNI 插件默认使用 `bridge` 委托。
- `bridge`：要使用的网桥的名称。默认情况下，flannel CNI 插件会创建一个名为“cni0”的网桥。
- `isGateway`：指定网桥是否是网络的网关。 flannel CNI 插件默认将其设置为“true”。
- `ipMasq`: 指定是否启用 IP 伪装。 flannel CNI 插件默认将其设置为“true”。
- `mtu`：网络的 MTU。 flannel CNI 插件默认将其设置为“1500”。
- `hairpinMode`: 指定是否启用发夹模式。 flannel CNI 插件默认将其设置为“true”。

下面是一个示例 flannel CNI 插件配置：

```json
{
    "name": "my-network",
    "type": "flannel",
    "delegate": {
        "bridge": "cni0"
    },
    "isGateway": true,
    "ipMasq": true,
    "mtu": 1500,
    "hairpinMode": true
}
```

将配置文件保存为“my-network.json”并将其放在“/etc/cni/net.d/”目录中。

### 创建法兰绒 CNI 网络

安装并配置 flannel CNI 插件后，您可以使用 `cni-add` 命令创建网络。 `cni-add` 命令将配置文件的路径作为参数。

```
$ sudo cni-add my-network.json
```

这将创建一个名为“my-network”的网络。网络将使用“my-network.json”文件中的设置进行配置。

### 删除 flannel CNI 网络

要删除 flannel CNI 网络，可以使用 `cni-del` 命令。 `cni-del` 命令将配置文件的路径作为参数。

```
$ sudo cni-del my-network.json
```

这将删除名为“my-network”的网络。

## 结论

在本文中，我们向您展示了如何使用 CNI 为 Kubernetes 集群配置网络。我们涵盖了以下主题：

- 什么是 CNI？
- CNI 是如何工作的？
- 如何使用 CNI 为 Kubernetes 配置网络？

如果您对为 Kubernetes 配置网络有任何疑问，请在下方发表评论。