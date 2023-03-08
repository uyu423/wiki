---
title: 带有 Containerd 的 Kubernetes：使用另一个容器运行时运行容器
description: 
published: true
date: 2023-02-14T10:32:36.204Z
tags: 
editor: markdown
dateCreated: 2023-02-14T10:32:28.852Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes with Containerd: Running Containers with Another Container Runtime***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-containerd-running-containers-with-another-container-runtime)
{.links-list}


# Kubernetes with Containerd：使用另一个容器运行时运行容器

Kubernetes 默认的容器运行时是 Docker，但 Kubernetes 也兼容其他容器运行时。在本文中，我们将了解如何使用 Containerd 运行 Kubernetes。

## 为什么使用 Containerd？

Containerd 是一个行业标准的容器运行时，因其简单性和健壮性而广受欢迎。它也被其他容器编排平台使用，例如 Docker Swarm 和 Apache Mesos。

## 安装容器

要安装 Containerd，您可以使用包管理器，例如 apt 或 yum。

```
sudo apt install containerd
```

## 配置 Kubernetes 以使用 Containerd

安装 Containerd 后，您需要配置 Kubernetes 以将其用作容器运行时。为此，您需要编辑“/etc/kubernetes/manifests/kubelet.yaml”文件并添加以下行：

```
--container-runtime=containerd
```

您还需要编辑“/etc/systemd/system/kubelet.service.d/10-kubelet.conf”文件并添加以下行：

```
Environment="KUBELET_EXTRA_ARGS=--container-runtime=containerd"
```

进行这些更改后，您需要重新启动 `kubelet` 服务。

```
sudo systemctl restart kubelet
```

## 创建容器

现在 Kubernetes 已配置为使用 Containerd，让我们创建一个容器。

首先，我们需要创建一个名为“container.json”的文件，其中包含以下内容：

```json
{
  "id": "container1",
  "runtime": "containerd",
  "image": "nginx:latest"
}
```

接下来，我们需要使用 `ctr` 命令创建容器。

```
sudo ctr create -f container.json
```

## 运行容器

现在我们已经创建了一个容器，让我们运行它。

首先，我们需要创建一个名为 run.json 的文件，其中包含以下内容：

```json
{
  "id": "container1",
  "runtime": "containerd",
  "image": "nginx:latest",
  "command": ["nginx", "-g", "daemon off;"]
}
```

接下来，我们需要使用 `ctr` 命令运行容器。

```
sudo ctr run -f run.json
```

## 删除容器

要删除容器，我们可以使用 `ctr` 命令。

```
sudo ctr delete container1
```

## 结论

在本文中，我们了解了如何将 Kubernetes 与 Containerd 结合使用。我们还了解了如何安装 Containerd、配置 Kubernetes 以使用它，以及如何创建和运行容器。