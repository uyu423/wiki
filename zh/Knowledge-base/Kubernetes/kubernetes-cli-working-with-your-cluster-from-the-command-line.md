---
title: Kubernetes CLI：从命令行使用您的集群
description: 
published: true
date: 2023-02-17T18:16:52.808Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:43:36.182Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Kubernetes CLI: Working with Your Cluster from the Command Line***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-cli-working-with-your-cluster-from-the-command-line)
{.links-list}

    

# Kubernetes CLI：从命令行使用您的集群

Kubernetes 命令行界面 (CLI)，cfssl，是一种使用户能够从命令行操作 Kubernetes 集群的工具。本文概述了如何安装和设置 cfssl 工具，以及如何使用它来管理 Kubernetes 集群。

## 安装 Cfssl 工具

Cfssl 工具可以安装在任何 Linux 或 macOS 系统上。要在 Linux 上安装 cfssl，请使用以下命令：

```
$ curl -LO https://storage.googleapis.com/kubernetes-release/cfssl/cfssl_linux-amd64.tar.gz
$ tar -xzf cfssl_linux-amd64.tar.gz
$ mv cfssl_linux-amd64/bin/cfssl /usr/local/bin/
$ rm -rf cfssl_linux-amd64
```

要在 macOS 上安装 cfssl，请使用以下命令：

```
$ brew install cfssl
```

## 设置 Cfssl 工具

安装 cfssl 工具后，您需要设置环境变量。 CFSSL_CA 环境变量指定 cfssl 使用的 CA 证书的路径。 CFSSL_CERT 环境变量指定 cfssl 使用的客户端证书的路径。 CFSSL_KEY 环境变量指定 cfssl 使用的客户端密钥的路径。

要设置 cfssl 工具，请使用以下命令：

```
$ export CFSSL_CA=/path/to/ca.pem
$ export CFSSL_CERT=/path/to/client.pem
$ export CFSSL_KEY=/path/to/client-key.pem
```

## 创建 Kubernetes 集群

一旦安装并设置了 cfssl 工具，就可以使用它来创建 Kubernetes 集群。要创建 Kubernetes 集群，请使用以下命令：

```
$ cfssl create-cluster -size=3 -server=https://kubernetes.default.svc.cluster.local:443 -ca=ca.pem -ca-key=ca-key.pem
```

此命令创建一个具有三个节点的 Kubernetes 集群。服务器标志指定 Kubernetes API 服务器的 URL。 ca 标志指定 cfssl 使用的 CA 证书的路径。 ca-key 标志指定 cfssl 使用的 CA 密钥的路径。

## 删除 Kubernetes 集群

要删除 Kubernetes 集群，请使用以下命令：

```
$ cfssl delete-cluster -name=my-cluster
```

此命令删除名为 my-cluster 的 Kubernetes 集群。

## 列出 Kubernetes 集群

要列出使用 cfssl 创建的 Kubernetes 集群，请使用以下命令：

```
$ cfssl list-clusters
```

此命令列出了使用 cfssl 创建的所有 Kubernetes 集群。

## 获取集群信息

要获取有关 Kubernetes 集群的信息，请使用以下命令：

```
$ cfssl get-cluster -name=my-cluster
```

此命令获取有关名为 my-cluster 的 Kubernetes 集群的信息。

## 更新 Kubernetes 集群

要更新 Kubernetes 集群，请使用以下命令：

```
$ cfssl update-cluster -name=my-cluster -size=5
```

此命令将名为 my-cluster 的 Kubernetes 集群的大小更新为五个节点。

## 添加节点到 Kubernetes 集群

要将节点添加到 Kubernetes 集群，请使用以下命令：

```
$ cfssl add-node -name=my-cluster -size=3
```

此命令将三个节点添加到 Kubernetes 集群，名称为 my-cluster。

## 从 Kubernetes 集群中删除节点

要从 Kubernetes 集群中删除节点，请使用以下命令：

```
$ cfssl delete-node -name=my-cluster -size=3
```

此命令从名为 my-cluster 的 Kubernetes 集群中删除三个节点。

## 扩展 Kubernetes 集群

要扩展 Kubernetes 集群，请使用以下命令：

```
$ cfssl scale-cluster -name=my-cluster -size=5
```

此命令将名称为 my-cluster 的 Kubernetes 集群扩展到五个节点。

## 调整 Kubernetes 集群的大小

要调整 Kubernetes 集群的大小，请使用以下命令：

```
$ cfssl resize-cluster -name=my-cluster -size=3
```

此命令将名称为 my-cluster 的 Kubernetes 集群调整为三个节点。

## 获取 Kubernetes 集群的状态

要获取 Kubernetes 集群的状态，请使用以下命令：

```
$ cfssl get-status -name=my-cluster
```

此命令获取名为 my-cluster 的 Kubernetes 集群的状态。

## 获得帮助

要获取特定命令的帮助，请使用以下命令：

```
$ cfssl help <command>
```

此命令获取 cfssl 命令的帮助。

## 外部链接

- [Cfssl 文档](https://pkg.go.dev/mod/github.com/cloudflare/cfssl?tab=doc)
- [Kubernetes 文档](https://kubernetes.io/docs/home/)