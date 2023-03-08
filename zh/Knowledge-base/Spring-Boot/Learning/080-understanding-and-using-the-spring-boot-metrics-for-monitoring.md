---
title: 080：了解和使用 Spring Boot 指标进行监控
description: 
published: true
date: 2023-02-05T11:32:25.195Z
tags: 
editor: markdown
dateCreated: 2023-02-05T11:32:19.624Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [080: Understanding and Using the Spring Boot Metrics for Monitoring***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/080-understanding-and-using-the-spring-boot-metrics-for-monitoring)
{.links-list}


# 介绍

监控是任何软件开发过程的关键部分。它允许开发人员识别和诊断他们在生产中的应用程序的问题。

Spring Boot 提供了许多用于监控应用程序的内置指标。在这篇文章中，我们将了解什么是 Spring Boot 指标以及如何使用它们来监控您的应用程序。

# 什么是 Spring Boot 指标？

Spring Boot 指标是一组用于监控基于 Spring 的应用程序的工具。它们提供对应用程序运行时行为的洞察力，可用于识别性能瓶颈。

Spring Boot 指标旨在与各种监控工具一起使用，例如 Prometheus、Graphite 和 StatsD。

# 如何使用 Spring Boot 指标

Spring Boot 提供了多种配置和使用指标的方法。在本节中，我们将了解一些最重要的配置选项。

## 启用指标

默认情况下，在 Spring Boot 中禁用指标。要启用指标，您需要将以下属性添加到应用程序的“application.properties”文件中：

```
spring.metrics.enable=true
```

## 配置指标

Spring Boot 允许您配置指标系统的许多方面。例如，您可以配置默认注册表、指标名称前缀和导出格式。

以下属性可用于配置默认注册表：

```
spring.metrics.default-registry=my-registry
```

以下属性可用于配置指标名称前缀：

```
spring.metrics.prefix=my-prefix
```

以下属性可用于配置导出格式：

```
spring.metrics.export.format=json
```

## 导出指标

Spring Boot 支持多种导出指标的方法。最常见的方法是使用“/metrics”端点。默认情况下，此端点以 Prometheus 格式公开指标。

您还可以使用“/metrics/{name}”端点导出单个指标。例如，以下端点将导出 `jvm.memory.used` 指标：

```
/metrics/jvm.memory.used
```

# 结论

在这篇文章中，我们研究了 Spring Boot 指标以及如何使用它们来监控您的应用程序。我们还了解了如何启用和配置指标，以及如何导出指标以供监控工具使用。