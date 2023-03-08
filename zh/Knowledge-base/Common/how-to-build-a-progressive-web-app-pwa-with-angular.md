---
title: 如何使用 Angular 构建渐进式 Web 应用程序 (PWA)
description: 
published: true
date: 2023-02-06T07:55:34.123Z
tags: 
editor: markdown
dateCreated: 2023-02-06T07:55:32.528Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [How to Build a Progressive Web App (PWA) with Angular***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-progressive-web-app-pwa-with-angular)
{.links-list}


# 如何使用 Angular 构建渐进式 Web 应用程序 (PWA)

## 什么是 PWA？

渐进式 Web 应用程序 (PWA) 是一种 Web 应用程序，它使用现代 Web 技术为用户提供类似应用程序的体验。 PWA 响应迅速，可以安装在用户的主屏幕上。

## 为什么要构建 PWA？

PWA 与传统网络应用程序相比具有许多优势，包括改进的性能、离线功能和类似应用程序的功能。

## 如何使用 Angular 构建 PWA

Angular 是用于构建 PWA 的流行框架。在本文中，我们将向您展示如何使用 Angular 创建 PWA。

### 1.新建一个Angular项目

首先，您需要创建一个新的 Angular 项目。您可以使用 Angular CLI 执行此操作。

运行以下命令创建一个新的 Angular 项目：

```
ng new my-pwa
```

这将为您的 Angular 项目创建一个名为“my-pwa”的新文件夹。

### 2.添加PWA功能

接下来，您需要将 PWA 功能添加到您的 Angular 项目中。你可以使用 @angular/pwa 包来做到这一点。

首先，安装@angular/pwa 包：

```
npm install @angular/pwa --save
```

接下来，将 PWA 清单添加到您的 index.html 文件中：

```html
<link rel="manifest" href="/manifest.json">
```

最后，生成一个 service worker 文件：

```
ng generate service-worker
```

这将在您的 `src/` 文件夹中创建一个名为 `ngsw-worker.js` 的文件。

### 3. 测试你的 PWA

现在您已将 PWA 功能添加到您的 Angular 项目，您可以测试您的 PWA。

要测试 PWA，您需要运行本地服务器。 Angular CLI 包含一个开发服务器，因此您可以使用它。

运行以下命令启动开发服务器：

```
ng serve
```

现在，打开浏览器并转到 http://localhost:4200/。你应该看到你的 Angular 应用程序正在运行。

要测试 PWA 功能，您需要为 Chrome 安装 [Lighthouse](https://developers.google.com/web/tools/lighthouse/) 扩展程序。

安装 Lighthouse 后，打开扩展程序并单击“生成报告”按钮。

Lighthouse 将分析您的应用程序并提供报告。该报告将告诉您您的应用程序是否通过了 PWA 检查列表。

如果您的应用未通过核对清单，请尝试添加更多 PWA 功能。例如，您可以添加[推送通知](https://developers.google.com/web/fundamentals/getting-started/codelabs/push-notifications/) 或[后台同步](https://developers.google. com/web/fundamentals/getting-started/primers/background-sync）。

## 结论

在本文中，我们向您展示了如何使用 Angular 构建渐进式 Web 应用程序。 PWA 与传统网络应用程序相比具有许多优势，包括改进的性能、离线功能和类似应用程序的功能。使用 Angular，可以轻松地将 PWA 功能添加到您的 Web 应用程序。