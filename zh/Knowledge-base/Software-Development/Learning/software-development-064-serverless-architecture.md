---
title: 软件开发 064：无服务器架构
description: 
published: true
date: 2023-02-16T17:55:54.358Z
tags: 
editor: markdown
dateCreated: 2023-02-16T17:55:52.724Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Software Development 064: Serverless Architecture***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-064-serverless-architecture)
{.links-list}


# 软件开发 064：无服务器架构

“无服务器”一词最近引起了广泛关注，但它到底是什么意思呢？

在传统的Web应用中，应用代码部署在服务器上，服务器负责处理来自客户端的请求。然而，在无服务器应用程序中，应用程序代码部署在“云中”并响应事件执行。

使用无服务器架构有很多好处，包括：

- 减少运营开销：由于无需管理服务器，无服务器应用程序更易于维护。

- 可扩展性：由于应用程序代码是响应事件而执行的，因此它可以自动扩展以满足需求。

- 经济高效：由于无需配置和维护服务器，无服务器应用程序可以非常经济高效。

在本文中，我们将了解什么是无服务器架构以及如何开始开发无服务器应用程序。

## 什么是无服务器架构？

在传统的Web应用中，应用代码部署在服务器上，服务器负责处理来自客户端的请求。然而，在无服务器应用程序中，应用程序代码部署在“云中”并响应事件执行。

使用无服务器架构有很多好处，包括：

- 减少运营开销：由于无需管理服务器，无服务器应用程序更易于维护。

- 可扩展性：由于应用程序代码是响应事件而执行的，因此它可以自动扩展以满足需求。

- 经济高效：由于无需配置和维护服务器，无服务器应用程序可以非常经济高效。

## 开始使用无服务器

有许多不同的平台可让您开发无服务器应用程序，但在本文中，我们将重点介绍 AWS Lambda。

AWS Lambda 是一个允许您在云中运行代码而无需预置或管理服务器的平台。 Lambda 函数是为响应事件而执行的，例如 HTTP 请求或文件上传。

要开始开发 Lambda 函数，您首先需要创建一个 AWS 账户。完成此操作后，您可以使用 AWS 控制台创建 Lambda 函数。

创建 Lambda 函数时，您需要指定名称和描述，以及函数将执行的代码。 Lambda 函数可以用任何受支持的语言编写，包括 Node.js、Python 和 Java。

创建 Lambda 函数后，您可以通过事件调用它来测试它。例如，如果您使用的是 Node.js，则可以使用以下事件调用您的函数：

```javascript
{
  "key1": "value1",
  "key2": "value2",
  "key3": "value3"
}
```

如果您的函数是用 Python 编写的，则可以使用以下事件调用它：

```python
{
  "key1": "value1",
  "key2": "value2",
  "key3": "value3"
}
```

测试 Lambda 函数后，您可以通过创建 AWS Lambda 函数来部署它。

## 结论

在本文中，我们了解了什么是无服务器架构以及如何开始开发无服务器应用程序。无服务器应用程序是降低运营开销和成本的好方法，并且可以自动扩展以满足需求。

如果您有兴趣了解有关无服务器架构的更多信息，请查看以下资源：

- [什么是无服务器？](https://serverless.com/learn/what-is-serverless/)

- [开始使用 AWS 上的无服务器](https://aws.amazon.com/getting-started/projects/build-serverless-applications/)

- [无服务器架构](https://martinfowler.com/articles/serverless.html)