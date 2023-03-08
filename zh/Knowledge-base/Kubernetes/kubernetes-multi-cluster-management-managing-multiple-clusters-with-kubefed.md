---
title: Kubernetes 多集群管理：使用 kubefed 管理多个集群
description: 
published: true
date: 2023-02-14T04:32:31.679Z
tags: 
editor: markdown
dateCreated: 2023-02-14T04:32:29.982Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes Multi-Cluster Management: Managing Multiple Clusters with kubefed***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-multi-cluster-management-managing-multiple-clusters-with-kubefed)
{.links-list}



# Kubernetes 多集群管理：使用 kubefed 管理多个集群

在生产环境中，拥有多个 Kubernetes 集群的情况并不少见。这可能出于多种原因，包括扩展、高可用性或从事不同项目的不同团队。

管理多个 Kubernetes 集群可能是一个挑战，尤其是在保持它们同步方面。管理多个 Kubernetes 集群有几个选项，但在本文中，我们将重点关注 kubefed。

kubefed 是一个可以用来管理多个 Kubernetes 集群的工具。它是 Kubernetes 项目的一部分，旨在简化创建和维护 Kubernetes 集群联合的过程。

kubefed 有一些依赖项，包括：

-kubectl
- kube-apiserver
- kube-controller-manager

kubefed 还需要一个满足以下要求的 Kubernetes 集群：

- Kubernetes 1.4 或更高版本
- 集群必须启用 RBAC

## 创建一个 kubefed 集群

创建一个 kubefed 集群很容易。首先，我们需要创建一个 ConfigMap 用于存储 kubefed 配置。我们将这个 ConfigMap 称为“kubefed-config”：

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: kubefed-config
  namespace: kube-system
data:
  kubefed.yaml: |
    apiVersion: federation/v1beta1
    kind: Federation
    metadata:
      name: federation
    spec:
      # Add clusters to the federation here.
      clusters:
      - clusterName: cluster1
        serverAddressByClientCIDRs:
        - clientCIDR: 0.0.0.0/0
          serverAddress: https://10.0.1.1:6443
      - clusterName: cluster2
        serverAddressByClientCIDRs:
        - clientCIDR: 0.0.0.0/0
          serverAddress: https://10.0.2.1:6443
    ```

这个 ConfigMap 定义了我们想要添加到我们的联邦的两个 Kubernetes 集群。 “clusters”列表中的“cluster1”和“cluster2”条目是我们要添加的集群的名称。 “serverAddressByClientCIDRs”条目定义了每个集群的 Kubernetes API 服务器的 URL。

接下来，我们需要创建一个 Secret，用于存储每个集群的 kubeconfig 文件。我们将这个 Secret 称为“kubefed-kubeconfig”：

```
apiVersion: v1
kind: Secret
metadata:
  name: kubefed-kubeconfig
  namespace: kube-system
data:
  kubeconfig-cluster1: |
    apiVersion: v1
    kind: Config
    clusters:
    - cluster:
        server: https://10.0.1.1:6443
        name: cluster1
      name: cluster1
    contexts:
    - context:
        cluster: cluster1
        user: admin
      name: cluster1
    current-context: cluster1
    preferences: {}
    users:
    - name: admin
      user:
        token: abcdefg
  kubeconfig-cluster2: |
    apiVersion: v1
    kind: Config
    clusters:
    - cluster:
        server: https://10.0.2.1:6443
        name: cluster2
      name: cluster2
    contexts:
    - context:
        cluster: cluster2
        user: admin
      name: cluster2
    current-context: cluster2
    preferences: {}
    users:
    - name: admin
      user:
        token: hijklmnop
    ```

这个 Secret 包含每个集群的 kubeconfig 文件。 cluster1 的 kubeconfig 文件存储在“kubeconfig-cluster1”键中，cluster2 的 kubeconfig 文件存储在“kubeconfig-cluster2”键中。

有了 ConfigMap 和 Secret，我们现在可以创建 kubefed 集群。我们将使用 kubectl 命令创建 kubefed 集群：

```
kubectl create -f kubefed-configmap.yaml
kubectl create -f kubefed-secret.yaml
kubectl create -f kubefed-cluster.yaml
```

这将创建一个名为“kubefed”的新 Kubernetes 集群。该集群将用于管理我们在 ConfigMap 和 Secret 中定义的另外两个 Kubernetes 集群。

## 添加集群到 kubefed

现在我们有了一个 kubefed 集群，我们可以将其他 Kubernetes 集群添加到其中。我们将使用 kubefed 命令添加集群：

```
kubefed join cluster1 --host-cluster-context=cluster1 --cluster-context=cluster1
kubefed join cluster2 --host-cluster-context=cluster2 --cluster-context=cluster2
```

这会将“cluster1”和“cluster2”Kubernetes 集群添加到 kubefed 集群。 “--host-cluster-context”和“--cluster-context”参数指定用于主机集群 (kubefed) 和正在添加的集群（cluster1 或 cluster2）的 kubeconfig 上下文。

## 管理 kubefed

现在我们已经启动并运行了 kubefed 集群，我们可以开始使用它来管理我们的其他 Kubernetes 集群。

kubefed 命令可用于管理 kubefed 及其管理的 Kubernetes 集群。

要列出 kubefed 正在管理的 Kubernetes 集群，请使用“kubefed list”命令：

```
kubefed list
```

这将列出 kubefed 当前管理的 Kubernetes 集群。

要获取有关特定 Kubernetes 集群的更多信息，请使用“kubefed describe”命令：

```
kubefed describe cluster1
```

这将提供有关“cluster1”Kubernetes 集群的更多信息。

kubefed 命令也可用于扩展 Kubernetes 集群。要扩展集群，请使用“kubefed scale”命令：

```
kubefed scale cluster1 --replicas=3
```

这会将“cluster1”Kubernetes 集群扩展到三个副本。

## 删除一个 kubefed 集群

完成 kubefed 集群后，可以使用“kubefed delete”命令将其删除：

```
kubefed delete cluster1
```

这将从 kubefed 中删除“cluster1”Kubernetes 集群。

## 结论

kubefed 是管理多个 Kubernetes 集群的有用工具。它易于使用，可以帮助您保持集群同步。