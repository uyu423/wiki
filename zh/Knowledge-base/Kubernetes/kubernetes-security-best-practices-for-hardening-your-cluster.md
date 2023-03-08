---
title: Kubernetes 安全性：强化集群的最佳实践
description: 
published: true
date: 2023-02-09T01:32:55.630Z
tags: 
editor: markdown
dateCreated: 2023-02-09T01:32:53.978Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes Security: Best Practices for Hardening Your Cluster***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-security-best-practices-for-hardening-your-cluster)
{.links-list}


# Kubernetes 安全性：强化集群的最佳实践

当您采用 Kubernetes 时，您将获得以高度可用的方式部署、扩展和管理容器化应用程序的灵活性。但这种新级别的控制和责任也带来了新的安全挑战。

Kubernetes 是一个复杂的系统，包含许多组件和移动部件，因此默认情况下很难确保其安全。但是，通过遵循一些简单的最佳实践，您可以强化 Kubernetes 集群并保护您的应用程序免受常见威胁。

在本文中，我们将介绍一些最重要的 Kubernetes 安全最佳实践，包括：

* 配置RBAC控制对Kubernetes资源的访问
* 使用 TLS 加密网络流量
* 实施网络策略以限制 pod 之间的通信
* 在最低特权安全上下文中运行容器
* 保护 Kubernetes API 服务器
* 使用图像扫描仪来执行安全策略

## 配置 RBAC 以控制对 Kubernetes 资源的访问

基于角色的访问控制 (RBAC) 是 Kubernetes 的一项功能，可让您精细地控制哪些用户和服务帐户可以访问哪些 Kubernetes 资源。

RBAC 在 Kubernetes 中默认处于禁用状态，因此保护集群的第一步是启用它。您可以通过在启动 Kubernetes 集群时将“--authorization-mode=RBAC”标志传递给“kube-apiserver”二进制文件来执行此操作。

启用 RBAC 后，您可以创建“Role”和“ClusterRole”对象来定义应授予给定用户或服务帐户的权限。例如，您可以创建一个“角色”，允许用户查看和列出命名空间中的所有资源，但不能创建或删除任何资源。

然后，您可以创建一个 `RoleBinding` 或 `ClusterRoleBinding` 以将 `Role` 或 `ClusterRole` 绑定到用户或服务帐户。这将向用户或服务帐户授予指定的权限。

请务必注意，默认情况下，任何经过身份验证的用户都将拥有对 Kubernetes API 的完全访问权限。这意味着，除非您明确限制使用 RBAC 的访问，否则任何可以对您的 Kubernetes 集群进行身份验证的用户都将能够执行任何操作，包括删除集群中的所有资源。

## 使用 TLS 加密网络流量

传输层安全性 (TLS) 是一种协议，可让您加密网络流量以防止窃听和篡改。

Kubernetes 使用 TLS 加密组件之间的所有通信，以及 Kubernetes API 服务器和客户端之间的通信。默认情况下，Kubernetes 会为所有组件生成自签名证书。虽然这对于大多数开发和测试环境来说已经足够了，但您应该在生产环境中使用签名证书以确保流量不会被拦截或篡改。

您可以使用您选择的证书颁发机构 (CA) 生成签名证书，或者您可以使用诸如“kube-ssl”之类的工具为您的 Kubernetes 集群自动生成和部署签名证书。

## 实施网络策略以限制 Pod 之间的通信

网络策略是 Kubernetes 的一项功能，可让您控制允许哪些 Pod 相互通信。默认情况下，Kubernetes 集群中的所有 Pod 都可以相互通信，但这会使您的应用程序面临不必要的风险。

例如，如果您有一个包含敏感数据的 pod，您可能希望将通信限制为仅允许来自受信任的 pod 的通信。或者，如果您有一个包含多个微服务的应用程序，您可能希望将通信限制为仅允许需要相互通信的服务之间进行通信。

网络策略作为 Kubernetes 资源实现，您可以使用它来指定允许哪些 pod 相互通信。例如，以下网络策略将允许 `frontend` 和 `backend` 命名空间中的 pod 之间进行通信，但不允许 `frontend` 命名空间中的 pod 与 `database` 命名空间中的 pod 之间进行通信：

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: frontend-backend
  namespace: frontend
spec:
  podSelector:
    matchLabels:
      app: frontend
  policyTypes:
  - Ingress
  - Egress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: backend
  egress:
  - to:
    - podSelector:
        matchLabels:
          app: backend
```

网络策略是一个复杂的话题，配置它的方法有很多种。我们建议阅读有关网络策略的 Kubernetes 文档以获取更多信息。

## 在最低权限的安全上下文中运行容器

安全上下文是一组可应用于 pod 或容器的与安全相关的选项。这些选项可用于控制允许哪些用户和组访问 pod 或容器，以及允许哪些功能。

默认情况下，Kubernetes 中的容器以“root”用户身份运行，这使容器能够完全访问主机系统。这是一个主要的安全风险，因为恶意容器可能会访问敏感的主机系统数据，甚至接管整个主机系统。

为了减轻这种风险，您应该始终在最低特权的安全上下文中运行容器。这意味着为容器指定一个非根用户来运行，以及指定允许容器使用哪些功能。

例如，以下 `Pod` 定义将以 `nginx` 用户身份运行 `nginx` 容器，并且不允许容器使用任何功能：

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: default
spec:
  securityContext:
    runAsUser: 1000
    fsGroup: 1000
  containers:
  - name: nginx
    image: nginx
    securityContext:
      capabilities: {}
```

以非 root 用户身份运行容器通常是一种很好的安全做法，在 Kubernetes 中尤其重要，因为容器可能会访问敏感的主机系统数据。

## 保护 Kubernetes API 服务器

Kubernetes API 服务器是所有 Kubernetes 组件的中心通信点，它负责处理所有 API 请求。这使得 API 服务器成为 Kubernetes 系统的关键组件，保护它以防止未经授权的访问非常重要。

保护 API 服务器的一种方法是使用 TLS 证书来加密进出 API 服务器的所有流量。正如我们前面提到的，Kubernetes 默认会为所有组件生成自签名证书，但您应该在生产中使用签名证书以确保流量不会被拦截或篡改。

另一种保护 API 服务器的方法是使用身份验证插件。 Kubernetes 包括许多内置的身份验证插件，包括“HTTPBasicAuth”、“Token”、“X509”和“Webhook”。您还可以使用第三方身份验证插件，例如 `OIDC` 或 `LDAP`。

## 使用图像扫描仪执行安全策略

镜像扫描器是帮助您为容器镜像实施安全策略的工具。例如，您可以使用图像扫描仪来检查图像中的已知漏洞，或者执行要求图像由受信任的权威机构签名的策略。

Kubernetes 包含一个名为“Clair”的内置图像扫描器，可用于扫描图像以查找已知漏洞。 Clair 是一个开源项目，您可以在项目网站上找到有关它的更多信息。

除了 Clair 之外，还有许多其他图像扫描仪可用，既有开源的也有商业的。我们建议您进行一些研究，以找到满足您特定需求的图像扫描仪。

## 结论

在本文中，我们介绍了一些最重要的 Kubernetes 安全最佳实践。通过遵循这些最佳实践，您可以强化 Kubernetes 集群并保护您的应用程序免受常见威胁。