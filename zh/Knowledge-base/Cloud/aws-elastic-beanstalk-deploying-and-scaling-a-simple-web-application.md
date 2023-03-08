---
title: AWS Elastic Beanstalk：部署和扩展简单的 Web 应用程序
description: 
published: true
date: 2023-02-09T12:18:12.654Z
tags: 
editor: markdown
dateCreated: 2023-02-09T12:18:10.843Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [AWS Elastic Beanstalk: Deploying and Scaling a Simple Web Application***English** document is available*](/en/Knowledge-base/Cloud/aws-elastic-beanstalk-deploying-and-scaling-a-simple-web-application)
{.links-list}


# AWS Elastic Beanstalk：部署和扩展简单的 Web 应用程序

AWS Elastic Beanstalk 是一种易于使用的服务，用于部署和扩展使用流行的 Web 应用程序框架（例如 Java、.NET、PHP、Node.js、Python、Ruby on Rails 和 AWS 上的 Docker）开发的 Web 应用程序和服务。

Elastic Beanstalk 降低了管理 Web 应用程序底层资源的复杂性，例如 Amazon EC2 实例、负载均衡器和 Auto Scaling 组。它还为监控 Web 应用程序的运行状况和性能提供了统一的体验。

在本文中，我们将向您展示如何在 AWS Elastic Beanstalk 上部署一个简单的 Web 应用程序。我们还将演示横向（通过添加更多 Amazon EC2 实例）和纵向（通过增加 Amazon EC2 实例的大小）扩展您的 Web 应用程序是多么容易。

## 先决条件

在开始之前，您需要具备以下条件：

* AWS 账户。如果您没有，可以 [此处](https://aws.amazon.com/getting-started/) 免费创建一个。
* 可以部署在 Amazon EC2 实例上的 Web 应用程序。对于本文，我们将使用一个简单的 Node.js Web 应用程序。
* 用于存储 Web 应用程序源代码的 Amazon S3 存储桶。

## 在 AWS Elastic Beanstalk 上部署您的 Web 应用程序

要在 AWS Elastic Beanstalk 上部署您的 Web 应用程序，请创建 Elastic Beanstalk 环境并将应用程序的源代码上传到 Amazon S3 存储桶。然后，Elastic Beanstalk 将创建一个 Amazon EC2 实例，在其上加载您的 Web 应用程序，并将其配置为服务流量。

### 创建 Elastic Beanstalk 环境

要创建 Elastic Beanstalk 环境，请打开 Elastic Beanstalk 控制台并单击“创建新应用程序”。

![创建新应用程序](https://i.imgur.com/lpY7B0m.png)

为您的应用程序输入一个名称，然后单击“创建”。

![输入申请名称](https://i.imgur.com/fvqQYxo.png)

在下一页上，选择您要使用的 Web 服务器平台。对于本文，我们将使用“Node.js”。

![选择平台](https://i.imgur.com/LJNcuAO.png)

在下一页上，选择您要使用的 Amazon EC2 实例类型。对于本文，我们将使用“t2.micro”实例类型。

![选择-ec2-实例类型](https://i.imgur.com/VkzM8JZ.png)

在下一页上，选择要用于存储 Web 应用程序源代码的 Amazon S3 存储桶。

![select-s3-bucket](https://i.imgur.com/y4FtJjl.png)

单击“部署”以在 AWS Elastic Beanstalk 上部署您的 Web 应用程序。

![部署应用程序](https://i.imgur.com/BKW738u.png)

Elastic Beanstalk 现在将创建一个 Amazon EC2 实例，在其上加载您的 Web 应用程序，并将其配置为服务流量。

### 将应用程序的源代码上传到 Amazon S3

现在您已经创建了 Elastic Beanstalk 环境，您需要将 Web 应用程序的源代码上传到您选择的 Amazon S3 存储桶。

为此，请打开 Amazon S3 控制台并选择您要使用的存储桶。然后，单击“上传”按钮。

![上传按钮](https://i.imgur.com/TXrQ8oA.png)

在下一页上，选择要上传的文件并单击“上传”。

![选择要上传的文件](https://i.imgur.com/F3gG0CY.png)

您的 Web 应用程序的源代码现在存储在 Amazon S3 存储桶中。

## 访问您的 Web 应用程序

在 AWS Elastic Beanstalk 上部署您的 Web 应用程序后，您可以通过转到环境的 URL 来访问它。

要查找环境的 URL，请打开 Elastic Beanstalk 控制台并单击您创建的环境。然后，单击“概述”选项卡。环境的 URL 显示在页面顶部。

![环境网址](https://i.imgur.com/vzMJO4F.png)

## 扩展您的 Web 应用程序

AWS Elastic Beanstalk 使您可以轻松地水平（通过添加更多 Amazon EC2 实例）和垂直（通过增加 Amazon EC2 实例的大小）扩展您的 Web 应用程序。

要水平扩展您的 Web 应用程序，请打开 Elastic Beanstalk 控制台并单击您创建的环境。然后，单击“配置”选项卡。

![配置选项卡](https://i.imgur.com/J3GfUxz.png)

在下一页上，单击“容量”选项卡。

![容量标签](https://i.imgur.com/pLJgJw6.png)

在下一页上，选择您要使用的 Amazon EC2 实例的数量，然后单击“应用”。

![选择实例数](https://i.imgur.com/X3XWqlr.png)

Elastic Beanstalk 现在会将所需数量的 Amazon EC2 实例添加到您的环境中。

要垂直扩展您的 Web 应用程序，请打开 Elastic Beanstalk 控制台并单击您创建的环境。然后，单击“配置”选项卡。

![配置选项卡](https://i.imgur.com/J3GfUxz.png)

在下一页上，单击“容量”选项卡。

![容量标签](https://i.imgur.com/pLJgJw6.png)

在下一页上，选择您要使用的 Amazon EC2 实例类型，然后单击“应用”。

![选择-ec2-实例类型](https://i.imgur.com/IHLv4jO.png)

Elastic Beanstalk 现在将重新配置您的环境以使用所需的 Amazon EC2 实例类型。

## 监控您的 Web 应用程序

AWS Elastic Beanstalk 提供统一的体验来监控您的 Web 应用程序的运行状况和性能。

要查看 Web 应用程序的运行状况和性能指标，请打开 Elastic Beanstalk 控制台并单击您创建的环境。然后，单击“监视”选项卡。

![监控选项卡](https://i.imgur.com/VxKG0zJ.png)

在下一页上，您将看到一个仪表板，其中包含有关您的 Web 应用程序的各种指标，例如请求计数、响应时间和 CPU 利用率。

![监控仪表板](https://i.imgur.com/ZDGxK5M.png)

您还可以查看 Web 应用程序的访问日志和错误日志。为此，打开 Elastic Beanstalk 控制台并单击您创建的环境。然后，单击“日志”选项卡。

![日志标签](https://i.imgur.com/D4Y4lkO.png)

在下一页上，您将看到 Web 应用程序访问日志和错误日志的列表。

![日志](https://i.imgur.com/rAFwUOI.png)

## 更新您的 Web 应用程序

要更新您的 Web 应用程序，只需将更新版本的 Web 应用程序源代码上传到您正在使用的 Amazon S3 存储桶。 Elastic Beanstalk 将自动检测更改并部署 Web 应用程序的更新版本。

## 删除您的 Web 应用程序

要删除您的 Web 应用程序，请打开 Elastic Beanstalk 控制台并单击您创建的环境。然后，单击“操作”下拉菜单并选择“删除环境”。

![删除环境](https://i.imgur.com/VxJN4jO.png)

在下一页上，输入您要删除的环境的名称，然后单击“删除”。

![输入环境名称](https://i.imgur.com/uvaYG4Y.png)

Elastic Beanstalk 现在将删除您的 Web 应用程序。

## 结论

在本文中，我们向您展示了如何在 AWS Elastic Beanstalk 上部署一个简单的 Web 应用程序。我们还演示了横向（通过添加更多 Amazon EC2 实例）和纵向（通过增加 Amazon EC2 实例的大小）扩展 Web 应用程序是多么容易。最后，我们还向您展示了如何监控 Web 应用程序的健康状况和性能。