---
title: 使用 AWS 和 Azure 构建混合云
description: 
published: true
date: 2023-02-17T18:12:15.133Z
tags: 
editor: markdown
dateCreated: 2023-01-30T19:04:19.548Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Building Hybrid Clouds with AWS and Azure***English** version of this document is available*](/en/Knowledge-base/Cloud/building-hybrid-clouds-with-aws-and-azure)
{.links-list}




# 使用 AWS 和 Azure 构建混合云

随着最近发布的 Azure Stack 和 AWS Outposts，现在可以构建跨越 Azure 和 AWS 的混合云。在本文中，我们将了解如何执行此操作，以及这样做的一些优点和缺点。

## 什么是混合云？

混合云是一种混合使用本地资源和基于云的资源的云计算。这可以是公共云和私有云的混合，也可以是不同云提供商的混合。

混合云的一个常见用例是将云用于计算和存储资源，同时出于安全或监管原因将数据保留在本地。

另一个常见的用例是使用云进行开发和测试，同时将生产保持在本地。这样做可以出于成本原因，或者将生产数据保存在更安全的网络上。

## Azure Stack 和 AWS Outposts

Azure Stack 是 Azure 的本地版本，可用于构建混合云。它包括与 Azure 相同的所有计算、存储和网络资源，并且可以使用相同的 Azure 门户进行管理。

AWS Outposts 是 AWS 的本地版本，可用于构建混合云。它包括与 AWS 相同的所有计算、存储和网络资源，并且可以使用相同的 AWS 控制台进行管理。

## 构建混合云

使用 Azure 和 AWS 构建混合云主要有两种方式：

### 选项 1：使用 Azure Stack 进行计算，使用 AWS Outposts 进行存储

在此选项中，您将为所有计算资源使用 Azure Stack，为所有存储资源使用 AWS Outposts。您的数据将存储在 Outposts 上的 S3 存储桶中，您可以从 Azure Stack 上运行的应用程序访问它。

此选项的一个好处是您只需要管理一组资源。您的所有计算都将在 Azure 门户中进行管理，而您的所有存储都将在 AWS 控制台中进行管理。

此选项的缺点是无法利用 Azure 的 blob 存储或 AWS 的 EBS 卷。您还需要将 Outposts 安装在与 Azure Stack 部署相同的位置。

### 选项 2：使用 Azure Stack 进行存储，使用 AWS Outposts 进行计算

在此选项中，您将为所有存储资源使用 Azure Stack，为所有计算资源使用 AWS Outposts。您的数据将存储在 Azure Stack 上的 blob 存储中，您可以从 AWS Outposts 上运行的应用程序访问它。

此选项的一个好处是您可以利用 Azure 的 blob 存储。这可用于不经常访问的数据，或需要存储在安全位置的数据。

此选项的缺点是无法利用 AWS 的 EBS 卷。您还需要将 Outposts 安装在与 Azure Stack 部署相同的位置。

## 结论

使用 Azure 和 AWS 构建混合云是充分利用两全其美的好方法。 Azure Stack 和 AWS Outposts 让您可以轻松部署和管理混合云。