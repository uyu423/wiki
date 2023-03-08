---
title: AWS WAF：使用防火墙规则保护 Web 应用程序
description: 
published: true
date: 2023-01-31T15:57:42.786Z
tags: 
editor: markdown
dateCreated: 2023-01-31T15:57:39.167Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [AWS WAF: Securing Web Applications with Firewall Rules***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-waf-securing-web-applications-with-firewall-rules)
{.links-list}



# AWS WAF：使用防火墙规则保护 Web 应用程序

Web 是一个不断发展的平台，每天都会出现新技术和威胁。因此，保护 Web 应用程序已成为任何组织网络安全战略的重要组成部分。

保护 Web 应用程序安全的最有效方法之一是使用 Web 应用程序防火墙 (WAF)。 WAF 是一款位于您的 Web 应用程序和互联网之间的软件，用于过滤进出您的应用程序的流量。

AWS WAF 是一种基于云的 WAF，可保护在 AWS 上运行的 Web 应用程序。 AWS WAF 让您可以控制允许哪些流量到达您的应用程序，使其成为抵御常见 Web 攻击的有效工具。

在本文中，我们将了解如何使用 AWS WAF 来保护 Web 应用程序。我们将涵盖以下主题：

- 什么是 AWS WAF？
- AWS WAF 是如何工作的？
- 设置 AWS WAF
- 创建 WAF 规则
- 将 WAF 规则应用于 Web 应用程序

## 什么是 AWS WAF？

AWS WAF 是一种基于云的 WAF，可保护在 AWS 上运行的 Web 应用程序。 AWS WAF 让您可以控制允许哪些流量到达您的应用程序，使其成为抵御常见 Web 攻击的有效工具。

AWS WAF 易于设置和管理，并且与其他 AWS 服务集成，例如 Amazon CloudFront、Amazon API Gateway 和 Amazon AWS Lambda。

## AWS WAF 是如何工作的？

AWS WAF 的工作原理是检查进出您的 Web 应用程序的流量并过滤掉不符合您指定规则的流量。

您可以使用 AWS WAF 创建规则，根据源 IP 地址、URL 或请求内容等条件允许或阻止流量。

AWS WAF 还允许您创建规则来限制流量或限制特定用户。这对于防止拒绝服务 (DoS) 攻击很有用。

## 设置 AWS WAF

在您可以使用 AWS WAF 之前，您需要设置一个 AWS 账户并为您的 Web 应用程序创建一个 Amazon CloudFront 分配。

拥有 Amazon CloudFront 分配后，您可以为分配启用 AWS WAF。为此，您需要创建一个 WAF Web ACL 并将其与您的分配相关联。

## 创建 WAF 规则

设置 AWS WAF 后，您可以开始创建规则。可以使用 AWS 管理控制台、AWS WAF API 或 AWS 命令行界面 (CLI) 创建规则。

创建规则时，您需要指定以下内容：

- 规则名称
- 触发规则时采取的操作（允许或阻止）
- 触发规则的条件

## 将 WAF 规则应用于 Web 应用程序

创建 WAF 规则后，您需要将其应用到您的 Web 应用程序。这可以使用 AWS 管理控制台、AWS WAF API 或 AWS 命令行界面 (CLI) 来完成。

将规则应用于 Web 应用程序时，您需要指定以下内容：

- Web ACL 的名称
- Web ACL 的 ARN
- 规则名称
- 规则的优先级

将 WAF 规则应用于 Web 应用程序将导致所有进出该应用程序的流量都由 WAF 检查。这会影响应用程序的性能，因此在将规则应用于生产流量之前对其进行测试非常重要。

## 结论

在本文中，我们了解了如何使用 AWS WAF 来保护 Web 应用程序。我们涵盖了以下主题：

- 什么是 AWS WAF？
- AWS WAF 是如何工作的？
- 设置 AWS WAF
- 创建 WAF 规则
- 将 WAF 规则应用于 Web 应用程序

如果您希望保护您的 Web 应用程序，AWS WAF 是一个值得考虑的强大工具。