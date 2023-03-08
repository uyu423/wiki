---
title: 086：将 Spring Boot 应用程序部署到 Kubernetes
description: 
published: true
date: 2023-02-05T16:32:17.707Z
tags: 
editor: markdown
dateCreated: 2023-02-05T16:32:16.104Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [086: Deploying a Spring Boot Application to Kubernetes***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/086-deploying-a-spring-boot-application-to-kubernetes)
{.links-list}


# 086：将 Spring Boot 应用程序部署到 Kubernetes

Kubernetes 是一个开源系统，用于自动部署、扩展和管理容器化应用程序。

Spring Boot 是一种流行的 Java 框架，用于构建 Web 应用程序和微服务。

在本文中，我们将向您展示如何将 Spring Boot 应用程序部署到 Kubernetes。

## 先决条件

- 一个 Kubernetes 集群
- 一个 Spring Boot 应用程序

## 部署应用程序

1. 为您的应用程序创建 Kubernetes 部署。

   ```
   api版本：应用程序/v1
   种类：部署
   元数据：
     名称：myapp-deployment
   规格：
     复制品：3
     选择器：
       匹配标签：
         应用程序：我的应用程序
     模板：
       元数据：
         标签：
           应用程序：我的应用程序
       规格：
         容器：
         - 名称：myapp-container
           图片：myapp-image
           端口：
           - 容器端口：8080
   ```

2. 为您的应用程序创建一个 Kubernetes 服务。

   ```
   api版本：v1
   种类：服务
   元数据：
     名称：myapp-service
   规格：
     类型：负载均衡器
     端口：
     - 端口：80
       目标端口：8080
     选择器：
       应用程序：我的应用程序
   ```

3. 将部署和服务应用到您的 Kubernetes 集群。

   ```
   kubectl apply -f myapp-deployment.yaml
   kubectl apply -f myapp-service.yaml
   ```

4. 检查部署和服务是否正在运行。

   ```
   kubectl 获取部署
   kubectl 获取服务
   ```

您的应用程序现已部署到 Kubernetes！

## 附加信息

- [Kubernetes 文档](https://kubernetes.io/docs/)
- [Spring Boot 文档](https://spring.io/projects/spring-boot)