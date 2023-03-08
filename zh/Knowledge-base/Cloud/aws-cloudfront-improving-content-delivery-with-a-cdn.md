---
title: AWS CloudFront：使用 CDN 改进内容交付
description: 
published: true
date: 2023-02-01T14:17:42.967Z
tags: 
editor: markdown
dateCreated: 2023-02-01T14:17:41.535Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [AWS CloudFront: Improving Content Delivery with a CDN***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-cloudfront-improving-content-delivery-with-a-cdn)
{.links-list}


  包括文章的开头和结尾句。

# AWS CloudFront：使用 CDN 改进内容交付

如果您希望提高网站或 Web 应用程序的性能，首先要考虑的地方之一就是您的内容分发网络 (CDN)。 CDN 可以通过在世界各地的位置缓存内容来帮助提高内容的加载速度，以便用户可以更快地访问它。

最受欢迎的 CDN 之一是 Amazon CloudFront，这是一项位于亚马逊 AWS 基础设施之上的服务。 CloudFront 是一个全球 CDN，可通过边缘位置网络交付您的内容。它易于设置和配置，并且与其他 AWS 服务集成。

在本文中，我们将了解如何使用 CloudFront 改进内容交付。我们将涵盖以下主题：

- 设置 CloudFront
- 配置 CloudFront
- 将 CloudFront 与其他 AWS 服务结合使用

## 设置 CloudFront

要开始使用 CloudFront，您需要创建一个分配。分配是用于交付您的内容的 AWS 资源的集合。要创建分配，您需要指定以下内容：

- 您的内容来源。这可以是 Amazon S3 存储桶、Amazon Elastic Compute Cloud (EC2) 实例或 HTTP 服务器。
- 发行版的配置。这包括分发的缓存行为和其他设置。
- 分配的价格等级。这将根据用户访问内容的区域来确定分发的定价。

创建分发后，您需要等待它被部署。这最多可能需要 15 分钟。部署分配后，您将能够通过 CloudFront URL 访问您的内容。

## 配置 CloudFront

设置 CloudFront 分配后，您需要对其进行配置以使用您的网站或 Web 应用程序。您需要做的第一件事是创建缓存行为。缓存行为决定了 CloudFront 如何处理您的内容请求。

有两种类型的缓存行为：默认和自定义。默认缓存行为适用于您分配中的所有文件，除非您为特定文件或文件夹指定自定义缓存行为。自定义缓存行为应用于特定文件或文件夹，并优先于默认缓存行为。

要创建缓存行为，您需要指定以下内容：

- 缓存行为适用的路径模式。这可以是特定文件或文件夹，或通配符模式。
- 缓存行为适用的来源。这是 CloudFront 将从中获取内容的来源。
- 缓存行为的默认 TTL（生存时间）。这是 CloudFront 缓存内容的时间。
- 缓存行为的最大 TTL。这是 CloudFront 缓存内容的最长时间。
- 缓存行为的最小 TTL。这是 CloudFront 缓存内容的最短时间。

创建缓存行为后，您可以指定其他设置，例如：

- 允许的 HTTP 方法。这决定了 CloudFront 允许缓存行为的 HTTP 方法。
- 缓存的 HTTP 方法。这决定了 CloudFront 将为缓存行为缓存哪些 HTTP 方法。
- 转发的标题。这决定了 CloudFront 将哪些标头转发到缓存行为的源。

## 将 CloudFront 与其他 AWS 服务结合使用

CloudFront 可以与其他 AWS 服务一起使用，以提高您的网站或 Web 应用程序的性能。例如，您可以将 CloudFront 与 Amazon S3 结合使用以从 S3 存储桶传送内容。

为此，您需要创建一个存储桶，然后将 CloudFront 配置为使用该存储桶作为源。您可以通过为存储桶创建缓存行为来执行此操作。

完成此操作后，您可以使用 CloudFront 将存储桶中的内容交付给用户。 CloudFront 会将内容缓存在世界各地的边缘位置，以便用户可以更快地访问它。

您还可以将 CloudFront 与 Amazon EC2 结合使用，以从 EC2 实例传送内容。为此，您需要创建一个实例，然后将 CloudFront 配置为使用该实例作为源。您可以通过为实例创建缓存行为来完成此操作。

完成此操作后，您可以使用 CloudFront 将内容从实例交付给用户。 CloudFront 会将内容缓存在世界各地的边缘位置，以便用户可以更快地访问它。

## 结论

在本文中，我们研究了如何使用 CloudFront 改进内容交付。我们涵盖了以下主题：

- 设置 CloudFront
- 配置 CloudFront
- 将 CloudFront 与其他 AWS 服务结合使用

如果您希望提高网站或 Web 应用程序的性能，CloudFront 是一个不错的选择。它易于设置和配置，并且与其他 AWS 服务集成。