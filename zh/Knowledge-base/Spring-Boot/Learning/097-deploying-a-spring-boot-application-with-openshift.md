---
title: 097：使用 OpenShift 部署 Spring Boot 应用程序
description: 
published: true
date: 2023-02-04T18:17:23.834Z
tags: 
editor: markdown
dateCreated: 2023-02-04T18:17:18.459Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [097: Deploying a Spring Boot Application with OpenShift***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/097-deploying-a-spring-boot-application-with-openshift)
{.links-list}


## 介绍

OpenShift 是 Red Hat 的平台即服务 (PaaS) 产品。它是一个本地应用程序平台，允许开发人员在云环境中快速开发、托管和扩展应用程序。

OpenShift 基于 Kubernetes 之上，提供了一组工具来帮助开发人员进行应用程序部署、管理和扩展。

在本文中，我们将学习如何在 OpenShift 上部署 Spring Boot 应用程序。我们还将学习如何使用 OpenShift 工具管理和扩展应用程序。

## 先决条件

在我们开始之前，我们需要做一些事情：

- 一个 OpenShift 帐户。如果您没有，可以在 [此处](https://www.openshift.com/pricing/index.html) 注册免费试用。
- 一个 Spring Boot 应用程序。如果您没有，可以使用 [Spring Initializr](https://start.spring.io/) 创建一个简单的。
- OpenShift 的 [oc](https://docs.openshift.com/container-platform/3.11/cli_reference/get_started_cli.html# installing-the-oc-command-line-interface) 命令行界面。

## 部署应用程序

我们可以通过两种方式在 OpenShift 上部署 Spring Boot 应用程序：使用 OpenShift Web 控制台或使用 oc 命令行界面。

### 使用 OpenShift Web 控制台进行部署

1. 登录到 OpenShift Web 控制台并单击“创建项目”按钮。

2. 输入项目名称并单击“创建”按钮。

3. 在“Add to Project”页面，选择“Deploy Image”选项，点击“Select Image”按钮。

4. 在“镜像名称”字段中，输入 Spring Boot 应用程序镜像的名称。如果图像不在 OpenShift 注册表中，您可以输入图像的完整 URL。

5. 在“图像配置”部分，指定应用程序的名称、应用程序将运行的端口以及应用程序的 jar 文件的路径。

6. 单击“部署”按钮。

7. 在“概览”页面中，您应该可以看到正在运行的应用程序。单击应用程序名称以转到应用程序页面。

8. 在应用程序页面中，您将看到应用程序的 URL。单击 URL 以在新选项卡中打开应用程序。

### 使用 oc 命令行界面进行部署

1. 使用 oc login 命令登录 OpenShift 集群。

2. 使用 oc new-project 命令创建一个新项目。

3. 使用 oc new-app 命令部署应用程序。指定应用程序的名称、应用程序将在其上运行的端口以及应用程序的 jar 文件的路径。

4. 在“概览”页面中，您应该看到正在运行的应用程序。单击应用程序名称以转到应用程序页面。

5. 在应用程序页面中，您将看到应用程序的 URL。单击 URL 以在新选项卡中打开应用程序。

## 管理应用程序

部署应用程序后，我们可以使用 OpenShift Web 控制台或 oc 命令行界面对其进行管理和扩展。

### 使用 OpenShift Web 控制台进行管理

1. 在 OpenShift Web 控制台中，单击“应用程序”菜单并选择“部署”选项。

2. 在“部署”页面中，您将看到项目中所有部署的列表。单击部署名称以转到部署页面。

3. 在部署页面中，您将看到部署的详细信息，例如副本数、部署策略和推出历史记录。

4. 要扩展部署，单击“扩展”按钮并输入所需的副本数。

5. 要触发新的推出，请单击“推出”按钮。

6. 要删除部署，请单击“删除”按钮。

### 使用 oc 命令行界面进行管理

1. 使用 oc login 命令登录 OpenShift 集群。

2. 要列出项目中的所有部署，请使用 oc get deployments 命令。

3. 要获取部署的详细信息，请使用 oc describe deployment 命令。

4. 要扩展部署，请使用 oc scale deployment 命令。

5. 要触发新推出，请使用 oc rollout latest 命令。

6. 要删除部署，请使用 oc delete deployment 命令。

## 结论

在本文中，我们学习了如何在 OpenShift 上部署 Spring Boot 应用程序。我们还学习了如何使用 OpenShift 工具管理和扩展应用程序。