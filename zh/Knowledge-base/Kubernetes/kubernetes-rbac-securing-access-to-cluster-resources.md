---
title: Kubernetes RBAC：保护对集群资源的访问
description: 
published: true
date: 2023-02-09T00:32:28.906Z
tags: 
editor: markdown
dateCreated: 2023-02-09T00:32:27.328Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes RBAC: Securing Access to Cluster Resources***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-rbac-securing-access-to-cluster-resources)
{.links-list}


# Kubernetes RBAC：保护对集群资源的访问

基于角色的访问控制 (RBAC) 是一种调节对计算机系统、应用程序和数据的访问的方法。它是任何企业环境中安全的基本组成部分。

在 Kubernetes 中，RBAC 用于控制对 Kubernetes API 的访问。任何需要访问 Kubernetes API 的用户、组或服务帐户都必须被赋予一个角色，该角色定义了他们拥有的访问级别。

Kubernetes 中的角色分为三类：

- **ClusterRole**：ClusterRole 定义了一组可以应用于集群中所有命名空间的权限。
- **角色**：角色只能应用于单个命名空间。
- **ServiceAccount**：ServiceAccount 定义了一组可应用于服务帐户的权限。

可以使用 `kubectl` 命令行工具创建角色。例如，要创建一个名为 my-cluster-role 的 ClusterRole，您可以使用以下命令：

```
kubectl create clusterrole my-cluster-role --verb=get,list,watch
```

这将为“my-cluster-role”授予集群中“get”、“list”和“watch”资源的权限。

也可以使用 YAML 文件创建角色。以下是 ClusterRole 的示例 YAML 文件：

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: my-cluster-role
rules:
- apiGroups: [""] # "" indicates the core API group
  resources: ["pods"]
  verbs: ["get", "list", "watch"]
```

可以使用“RoleBinding”或“ClusterRoleBinding”将角色绑定到用户、组或服务帐户。例如，以下命令将为 `my-user` 赋予 `my-cluster-role`：

```
kubectl create clusterrolebinding my-cluster-role-binding --clusterrole=my-cluster-role --user=my-user
```

这将为 `my-user` 提供 `my-cluster-role` 中定义的权限。

 也可以使用 YAML 文件创建绑定。以下是 ClusterRoleBinding 的示例 YAML 文件：

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: my-cluster-role-binding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: my-cluster-role
subjects:
- kind: User
  name: my-user
  apiGroup: rbac.authorization.k8s.io
```

这将为“my-user”提供“my-cluster-role”。

RBAC 可用于控制任何用户、组或服务帐户对 Kubernetes API 的访问。它是任何 Kubernetes 集群中安全的基本组成部分。