---
title: Kubernetes Operators：使用自定义控制器自动化应用程序管理
description: 
published: true
date: 2023-02-09T03:23:44.307Z
tags: 
editor: markdown
dateCreated: 2023-02-09T03:23:42.748Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes Operators: Automating Application Management with Custom Controllers***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-operators-automating-application-management-with-custom-controllers)
{.links-list}


# Kubernetes Operators：使用自定义控制器自动化应用程序管理

在本文中，我们将讨论 Kubernetes Operators。 Kubernetes 是一个用于自动化容器化应用程序的开源系统。 Operator 是一种打包、部署和管理 Kubernetes 应用程序的方法。在本文中，我们将重点介绍什么是 Operator 以及它如何帮助您自动化管理应用程序。

## 什么是运营商？

Operator 是一种打包、部署和管理 Kubernetes 应用程序的方法。 Kubernetes Operators 是 Kubernetes 的软件扩展，用于管理特定类型的应用程序。操作员使用自定义资源来表示应用程序的状态并定义所需的行为。自定义控制器监视对这些自定义资源的更改，并进行必要的更改以保持应用程序按预期运行。

Operator 是使用 Kubernetes API 和最佳实践构建的。这使得它们可以跨 Kubernetes 实现移植，并允许它们轻松扩展。

## 为什么要使用操作员？

Operators 提供了一种声明式的应用程序管理方法。这意味着您可以描述应用程序的所需状态，Operator 将确保应用程序达到并保持该状态。

Operators 还提供了一种方法来自动管理您的应用程序。应用程序可能很复杂，需要正确部署和配置许多不同的组件。这可能是一个耗时且容易出错的过程。操作员可以自动执行此过程，从而更轻松、更快速地部署和管理您的应用程序。

Operator 还可以帮助您管理应用程序的生命周期。这包括升级和降级应用程序以及向上或向下缩放应用程序等任务。

## 如何使用操作员？

Operator 被部署为自定义资源定义 (CRD)。 CRD 是添加到现有 Kubernetes 资源的注解。这允许 Operator 观察资源的变化并采取必要的行动。

Operators 也被部署为 Custom Controllers。自定义控制器是监视自定义资源更改的 Kubernetes 控制器。当检测到更改时，控制器将采取必要的操作以确保资源达到所需状态。

## 写一个操作符

运算符是用 Go 编写的。 Operator SDK 是一个工具包，可以轻松编写、构建和部署 Kubernetes Operator。 SDK 提供 CLI、脚手架和测试工具。

Operator 是使用 Kubernetes API 和最佳实践构建的。这使得它们可以跨 Kubernetes 实现移植，并允许它们轻松扩展。

Operator SDK CLI 可用于为 Operator 生成脚手架。这包括自定义资源定义 (CRD) 和自定义控制器。

生成脚手架后，即可实施 Operator。 Operator 将需要观察自定义资源的变化并采取必要的行动。

可以使用 kubectl 或 Operator SDK CLI 将 Operator 部署到 Kubernetes。

## 结论

在本文中，我们讨论了 Kubernetes Operators。我们已经介绍了什么是 Operator 以及它如何帮助您自动化应用程序的管理。我们还了解了如何编写和部署 Operator。