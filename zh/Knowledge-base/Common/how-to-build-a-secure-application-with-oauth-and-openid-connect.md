---
title: 如何使用 OAuth 和 OpenID Connect 构建安全应用程序
description: 
published: true
date: 2023-02-03T16:17:25.484Z
tags: 
editor: markdown
dateCreated: 2023-02-03T16:17:23.892Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [How to Build a Secure Application with OAuth and OpenID Connect***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-secure-application-with-oauth-and-openid-connect)
{.links-list}


# 如何使用 OAuth 和 OpenID Connect 构建安全应用程序

现代网络就是从各种不同的来源访问数据和服务。但是，如果操作不当，这可能会带来安全风险。在本文中，我们将向您展示如何使用 OAuth 和 OpenID Connect 构建安全的应用程序。

## 什么是 OAuth？

OAuth 是一种开放的授权标准，允许您安全地访问来自各种不同来源的数据和服务。它的工作原理是允许您指定要访问的数据和服务，然后授权您访问这些资源。

## 什么是 OpenID 连接？

OpenID Connect 是一种建立在 OAuth 之上的身份验证协议。它允许您通过各种不同的提供商（例如 Facebook 或 Google）对用户进行身份验证。

## 如何使用 OAuth 和 OpenID 连接

为了使用 OAuth 和 OpenID Connect，您需要向提供商注册您的应用程序。每个提供商都有自己的流程，因此我们不会在这里详细介绍。

注册应用程序后，您需要指定要访问的数据和服务。这是通过为您的应用程序创建一个“范围”来完成的。范围只是您向提供商请求的权限列表。

例如，如果您正在构建一个待办事项列表应用程序，您可能会请求以下范围：

- 读取和写入用户的待办事项列表
- 读取访问用户的个人资料信息

创建范围后，您需要将用户发送到提供商的授权端点。这是提供商将用于授权您访问用户数据的 URL。

授权端点将要求用户登录，然后要求他们授予您的应用程序访问您在范围内指定的数据和服务的权限。

一旦用户授予您的应用程序访问权限，提供商将使用授权代码将用户重定向回您的应用程序。然后可以将该代码交换为访问令牌，该令牌可用于访问用户的数据。

## 如何保护您的应用程序

获得访问令牌后，您需要采取一些预防措施以确保安全使用它。

首先，您永远不应该以纯文本形式存储访问令牌。相反，您应该以加密格式存储它。

其次，您应该只通过加密连接（例如 HTTPS）发送访问令牌。

第三，您应该确保访问令牌仅用于其预期的数据和服务。例如，如果您的应用程序只需要对用户的待办事项列表进行读取访问，那么访问令牌应该只用于该目的。

## 结论

在本文中，我们向您展示了如何使用 OAuth 和 OpenID Connect 构建安全的应用程序。通过采取本文中概述的预防措施，您可以确保您的应用程序安全并且您的用户数据受到保护。