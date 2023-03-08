---
title: 034：将 Nest.js 与 Angular 结合使用
description: 
published: true
date: 2023-02-13T20:17:20.992Z
tags: 
editor: markdown
dateCreated: 2023-02-13T20:17:19.333Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [034: Using Nest.js with Angular***English** document is available*](/en/Knowledge-base/Nest-js/Learning/034-using-nest-js-with-angular)
{.links-list}


# 在 Angular 中使用 Nest.js

Nest.js 是一个用于构建可扩展的服务器端应用程序的 Node.js 框架。它使用 TypeScript（JavaScript 的超集）并与 Angular 集成。

在这篇文章中，我们将看看如何将 Nest.js 与 Angular 一起使用。我们将创建一个简单的待办事项应用程序，并介绍如何将 Nest.js 与 Angular 结合使用的基础知识。

## 先决条件

在我们开始之前，您需要做一些事情才能跟进。

首先，您需要安装 Node.js 和 npm。您可以在 [此处](https://nodejs.org/en/download/) 找到有关如何执行此操作的说明。

接下来，您需要安装 Angular CLI。您可以在 [此处](https://cli.angular.io/) 找到有关如何执行此操作的说明。

最后，您需要安装 Nest.js CLI。您可以在 [此处](https://docs.nestjs.com/cli/overview) 找到有关如何执行此操作的说明。

## 创建一个新的 Nest.js 项目

我们将从创建一个新的 Nest.js 项目开始。我们可以使用 Nest.js CLI 来做到这一点。

要创建一个新的 Nest.js 项目，我们将运行以下命令：

```
nest new project-name
```

将 ```project-name``` 替换为您的项目名称。

这将使用您指定的名称创建一个新的 Nest.js 项目。

## 添加一个 Angular 项目

接下来，我们将向我们的 Nest.js 项目添加一个 Angular 项目。

我们可以使用 Angular CLI 来做到这一点。

要添加 Angular 项目，我们将运行以下命令：

```
ng new angular-project-name
```

将 ```angular-project-name``` 替换为您的 Angular 项目的名称。

这将使用您指定的名称创建一个新的 Angular 项目。

## 集成 Nest.js 和 Angular

现在我们有了一个 Nest.js 项目和一个 Angular 项目，我们需要整合它们。

我们可以使用 Nest.js CLI 来做到这一点。

要集成 Nest.js 和 Angular，我们将运行以下命令：

```
nest g @nestjs/ng-universaluniversal-project-name
```

将 ```universal-project-name``` 替换为通用项目的名称。

这将使用您指定的名称生成一个新的通用项目。

## 运行应用程序

现在我们已经集成了一个 Nest.js 项目和一个 Angular 项目，我们可以运行该应用程序了。

要运行该应用程序，我们将使用 Nest.js CLI。

要运行该应用程序，我们将运行以下命令：

```
nest start
```

这将启动应用程序。

## 结论

在这篇文章中，我们研究了如何将 Nest.js 与 Angular 结合使用。我们创建了一个简单的待办事项应用程序，并介绍了如何将 Nest.js 与 Angular 结合使用的基础知识。