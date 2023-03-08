---
title: Kubernetes Autoscaling：适应不断变化的负载
description: 
published: true
date: 2023-02-08T18:32:37.150Z
tags: 
editor: markdown
dateCreated: 2023-02-08T18:32:30.791Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kubernetes Autoscaling: Adapting to Changing Loads***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-autoscaling-adapting-to-changing-loads)
{.links-list}


# Kubernetes Autoscaling：适应不断变化的负载

随着组织转向微服务架构，容器化部署变得越来越流行。 Kubernetes 是最流行的容器编排平台之一，被各种规模的组织所使用。

Kubernetes 的关键特性之一是它能够根据不断变化的负载向上或向下扩展部署。这称为自动缩放，在许多情况下都很有用，例如发布新功能时或在流量高峰期间。

在本文中，我们将了解自动缩放在 Kubernetes 中的工作原理以及如何使用它来适应不断变化的负载。

## 什么是自动缩放？

自动缩放是根据不断变化的条件动态扩展或缩小系统的过程。在 Kubernetes 的上下文中，这通常意味着向上或向下扩展部署中的副本数量。

自动缩放可用于缩放部署以响应 CPU 使用率、内存使用率或其他自定义指标的变化。 Kubernetes 还可以配置为根据挂起的 Pod 数量或可用磁盘空间量进行扩展。

## 自动缩放在 Kubernetes 中是如何工作的？

Kubernetes 中的自动缩放是通过使用复制控制器或部署来实现的。复制控制器负责为给定部署维护所需数量的副本。

启用自动缩放后，复制控制器将根据需要向上或向下扩展部署以维持所需数量的副本。副本数可以手动指定，也可以根据 CPU 利用率或内存使用率等条件自动调整。

## 什么时候应该使用自动缩放？

自动缩放可用于需要动态调整副本数量的多种情况。

自动缩放的一些常见用例包括：

- 根据流量变化扩大或缩小部署
- 根据 CPU 利用率的变化向上或向下扩展部署
- 根据内存使用情况的变化向上或向下扩展部署

## 如何在 Kubernetes 中启用自动缩放

通过指定所需的副本数，可以为给定的部署启用自动缩放。这可以使用“kubectl”命令行工具或通过编辑部署的 YAML 文件来完成。

要使用 `kubectl` 启用自动缩放，您可以使用 `kubectl scale` 命令。例如，以下命令会将部署所需的副本数设置为 3：

```
kubectl scale --replicas=3 deployment/my-deployment
```

要通过编辑部署的 YAML 文件启用自动缩放，您需要将 `replicas` 键添加到 `spec` 部分。例如：

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: my-image
        ports:
        - containerPort: 8080
```

## 结论

在本文中，我们了解了自动缩放在 Kubernetes 中的工作原理以及如何使用它来适应不断变化的负载。自动缩放可用于根据流量、CPU 利用率或内存使用情况的变化向上或向下扩展部署。

如果您有兴趣了解有关 Kubernetes 的更多信息，请查看以下资源：

- Kubernetes 官方文档：https://kubernetes.io/docs/
- Kubernetes 社区 Slack 频道：https://kubernetes.slack.com/
- CNCF 最终用户社区调查结果：https://www.cncf.io/blog/2019/03/12/cncf-end-user-community-survey-results/