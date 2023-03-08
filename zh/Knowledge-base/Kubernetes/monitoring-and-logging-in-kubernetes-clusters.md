---
title: Kubernetes 集群中的监控和日志记录
description: 
published: true
date: 2023-02-08T19:32:28.322Z
tags: 
editor: markdown
dateCreated: 2023-02-08T19:32:22.529Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Monitoring and Logging in Kubernetes Clusters***English** document is available*](/en/Knowledge-base/Kubernetes/monitoring-and-logging-in-kubernetes-clusters)
{.links-list}


# Kubernetes 集群中的监控和日志记录

在本文中，我们将探讨如何监控和记录 Kubernetes 集群中的活动。我们将从概述通常为监视和日志记录收集的数据类型开始，然后我们将深入探讨可用于收集这些数据的一些特定工具和技术。

## 为监视和记录收集的数据类型

收集用于监视和记录的数据主要有两种类型：系统数据和应用程序数据。

系统数据包括有关 Kubernetes 集群中节点的信息，例如 CPU 和内存使用情况、网络流量和磁盘活动。这些数据通常是使用 Prometheus 等工具收集的。

应用程序数据包括有关在 Kubernetes 集群中运行的应用程序的信息，例如请求和响应时间、错误率和最慢的请求。这些数据通常是使用 Fluentd 等工具收集的。

## 收集系统数据

Prometheus 是一种流行的开源工具，用于收集系统数据。 Prometheus 可用于从任何类型的系统收集数据，但它对 Kubernetes 的支持特别好。

Prometheus 通过从 HTTP 端点抓取指标来收集数据。默认情况下，Kubernetes 在 /metrics 端点上公开了许多 Prometheus 格式的指标。 Prometheus 可以抓取这些指标，以提供有关 Kubernetes 集群的健康状况和性能的宝贵见解。

除了内置指标外，Kubernetes 还公开了一个“/logs”端点，Prometheus 可以抓取该端点以收集日志数据。此数据可用于生成警报或可视化集群中运行的应用程序的健康状况。

## 收集应用程序数据

Fluentd 是一种流行的开源工具，用于收集应用程序数据。 Fluentd 可用于从任何类型的应用程序收集数据，但它对 Kubernetes 的支持特别好。

Fluentd 通过解析日志文件来收集数据。默认情况下，Kubernetes 将所有日志数据写入“/var/log/containers”目录中的文件。 Fluentd 可以配置为监视此目录并解析日志数据以提取有用的信息，例如请求和响应时间、错误率和最慢的请求。

然后可以将此数据存储在数据库中以供进一步分析或用于生成警报。 Fluentd 还支持多种输出格式，因此数据可以轻松地与其他工具和系统集成。

## 结论

在本文中，我们探讨了如何收集系统和应用程序数据以在 Kubernetes 中进行监控和日志记录。我们已经了解了如何使用 Prometheus 收集系统数据，以及如何使用 Fluentd 收集应用程序数据。

这两种工具都是高度可配置的，并支持多种输入和输出格式。这使它们易于与其他工具和系统集成。

## 参考

1. 普罗米修斯：https://prometheus.io/
2.流利的：https://www.fluentd.org/
3. Kubernetes 监控：https://kubernetes.io/docs/concepts/cluster-administration/monitoring/