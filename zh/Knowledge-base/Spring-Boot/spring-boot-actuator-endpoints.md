---
title: Spring Boot 执行器端点
description: 
published: true
date: 2023-02-07T06:32:15.490Z
tags: 
editor: markdown
dateCreated: 2023-02-07T06:32:13.915Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot Actuator Endpoints***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-actuator-endpoints)
{.links-list}


# Spring Boot 执行器端点

Spring Boot 执行器端点允许我们监控和管理我们的 Spring Boot 应用程序。在本文中，我们将了解这些端点是什么以及我们如何使用它们。

## 什么是执行器端点？

执行器端点是由 Spring Boot 应用程序公开的 URL，可用于监视和管理应用程序。这些端点提供有关应用程序的信息，例如应用程序的健康状况、应用程序的版本等。

## 端点

Spring Boot 中有几个可用的执行器端点。其中一些端点是：

### /信息

此端点提供有关应用程序的信息。此信息在“application.properties”文件中配置。

### /健康

此端点提供有关应用程序运行状况的信息。此信息由在应用程序中注册的 HealthIndicator bean 收集。

### /指标

此端点提供有关应用程序指标的信息。此信息由在应用程序中注册的 Metrics bean 收集。

### /痕迹

此端点提供有关应用程序跟踪的信息。此信息由在应用程序中注册的 TraceRepository bean 收集。

## 启用执行器端点

Actuator Endpoints 在 Spring Boot 中默认不启用。我们可以通过将 spring-boot-actuator 依赖项添加到我们的项目来启用它们。

## 安全

我们可以通过将 Spring Security 添加到我们的项目来保护我们的执行器端点。我们可以通过将 spring-boot-starter-security 依赖项添加到我们的项目中来做到这一点。

## 结论

在本文中，我们了解了什么是 Spring Boot Actuator Endpoints 以及我们如何使用它们。我们还了解了如何启用和保护这些端点。