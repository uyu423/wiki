---
title: 029：将 Nest.js 应用程序部署到生产环境
description: 
published: true
date: 2023-02-09T18:17:35.617Z
tags: 
editor: markdown
dateCreated: 2023-02-09T18:17:33.930Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [029: Deploying Nest.js applications to production***English** document is available*](/en/Knowledge-base/Nest-js/Learning/029-deploying-nest-js-applications-to-production)
{.links-list}


# 将 Nest.js 应用程序部署到生产环境

## 介绍

Nest.js 是一个用于构建服务器端应用程序的 Node.js 框架。它是一个相对较新的框架，并且由于其易用性和可扩展性而越来越受欢迎。

Nest.js 框架基于Express.js 框架，使用JavaScript 的超集TypeScript 进行开发。

Nest.js 应用程序可以部署到各种生产环境，例如本地服务器、基于云的服务器，甚至是无服务器环境。

在这篇文章中，我们将重点介绍如何将 Nest.js 应用程序部署到生产环境。

## 先决条件

在我们开始之前，您需要做一些事情：

- 一个 Nest.js 应用程序。如果您没有，可以使用 Nest.js CLI 创建一个简单的。
- 生产环境。这可以是本地服务器、基于云的服务器或无服务器环境。
- 一个域名。这是可选的，但如果您想让全世界都可以访问您的应用程序，则建议您这样做。

## 部署到生产环境

将 Nest.js 应用程序部署到生产环境有两种主要方式：

- 使用特定于 Nest.js 的工具进行部署，例如 Nest.js CLI 或 Nest.js Deployer。
- 手动部署。

### 使用特定于 Nest.js 的工具进行部署

将 Nest.js 应用程序部署到生产环境的最简单方法是使用特定于 Nest.js 的工具。

有两个主要工具可用于此：Nest.js CLI 和 Nest.js Deployer。

Nest.js CLI 是一个命令行界面，可用于部署 Nest.js 应用程序。它作为全局 Node.js 模块安装，可用于将应用程序部署到各种生产环境，例如本地服务器、基于云的服务器，甚至是无服务器环境。

要使用 Nest.js CLI，您首先需要使用 npm 安装它：

```
npm install -g @nestjs/cli
```

安装 Nest.js CLI 后，您可以使用它来部署 Nest.js 应用程序。

例如，要将 Nest.js 应用程序部署到本地服务器，您可以使用以下命令：

```
nest deploy --server=on-premises
```

这会将您的 Nest.js 应用程序部署到本地服务器。

Nest.js Deployer 是一种工具，可用于将 Nest.js 应用程序部署到各种生产环境，例如本地服务器、基于云的服务器，甚至是无服务器环境。

要使用 Nest.js Deployer，您首先需要使用 npm 安装它：

```
npm install -g @nestjs/deployer
```

安装 Nest.js Deployer 后，您可以使用它来部署 Nest.js 应用程序。

例如，要将 Nest.js 应用程序部署到本地服务器，您可以使用以下命令：

```
deployer deploy --server=on-premises
```

这会将您的 Nest.js 应用程序部署到本地服务器。

### 手动部署

如果您不想使用特定于 Nest.js 的工具来部署您的 Nest.js 应用程序，您可以手动部署它。

要手动部署 Nest.js 应用程序，您需要：

- 构建您的 Nest.js 应用程序。
- 将您的应用程序部署到您的生产环境。

#### 构建你的 Nest.js 应用程序

第一步是构建您的 Nest.js 应用程序。

为此，您需要使用 Nest.js CLI。

Nest.js CLI 是一个命令行界面，可用于构建 Nest.js 应用程序。它作为全局 Node.js 模块安装，可用于为各种生产环境构建应用程序，例如本地服务器、基于云的服务器，甚至无服务器环境。

要使用 Nest.js CLI，您首先需要使用 npm 安装它：

```
npm install -g @nestjs/cli
```

安装 Nest.js CLI 后，您可以使用它来构建 Nest.js 应用程序。

例如，要为本地服务器构建 Nest.js 应用程序，您可以使用以下命令：

```
nest build --server=on-premises
```

这将为本地服务器构建 Nest.js 应用程序。

#### 将您的应用程序部署到您的生产环境

下一步是将应用程序部署到生产环境。

如何部署应用程序将取决于您的生产环境。

例如，如果您要部署到本地服务器，则需要使用 scp 之类的工具将应用程序文件复制到服务器。

如果您要部署到基于云的服务器，则需要使用 AWS Elastic Beanstalk 等工具来部署您的应用程序。

如果要部署到无服务器环境，则需要使用 AWS Lambda 等工具来部署应用程序。

## 结论

在这篇文章中，我们介绍了如何将 Nest.js 应用程序部署到生产环境。

我们已经研究了两种主要的方法来做到这一点：

- 使用特定于 Nest.js 的工具进行部署，例如 Nest.js CLI 或 Nest.js Deployer。
- 手动部署。

无论选择哪种方法，请确保在将应用程序提供给用户之前在生产环境中对其进行全面测试。