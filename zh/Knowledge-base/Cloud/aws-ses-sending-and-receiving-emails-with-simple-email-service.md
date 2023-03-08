---
title: AWS SES：使用简单的电子邮件服务发送和接收电子邮件
description: 
published: true
date: 2023-02-17T18:14:53.110Z
tags: 
editor: markdown
dateCreated: 2023-01-30T21:57:30.666Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [AWS SES: Sending and Receiving Emails with Simple Email Service***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-ses-sending-and-receiving-emails-with-simple-email-service)
{.links-list}


# AWS SES：使用简单的电子邮件服务发送和接收电子邮件

欢迎来到 IT 开发学习博客。在本文中，我们将讨论如何使用 AWS Simple Email Service 发送和接收电子邮件。

## 什么是 AWS 简单电子邮件服务？

AWS Simple Email Service (SES) 是一种经济高效且灵活的发送和接收电子邮件的方式。这是一种基于云的电子邮件服务，使您能够使用自己的域名发送和接收电子邮件，并且它支持个人和公司用例。

AWS SES 是一种可靠且可扩展的电子邮件服务，可与其他 AWS 服务集成。它提供按需付费的定价模式，无需前期费用，而且易于设置和使用。

## 使用 AWS SES 发送电子邮件

要使用 AWS SES 发送电子邮件，您需要拥有 AWS 账户和经过验证的电子邮件地址或域。如果您还没有 AWS 账户，可以在[此处](https://aws.amazon.com/) 创建一个。

拥有 AWS 账户后，您可以[验证电子邮件地址](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-email-addresses.html) 或[域](https:/ /docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-domains.html）与 AWS SES。验证电子邮件地址或域后，您可以开始发送电子邮件。

您可以使用 AWS SES 控制台、AWS SES API 或 AWS 命令行界面 (CLI) 发送电子邮件。在本文中，我们将使用 AWS SES 控制台发送电子邮件。

首先，转到 AWS SES 控制台并从菜单中选择 **Email Addresses**。然后，选择 **Verify a New Email Address** 并输入您要验证的电子邮件地址。

![验证电子邮件地址](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/01-verify-email-address.png)

AWS SES 将向您输入的地址发送一封验证电子邮件。按照验证电子邮件中的说明完成验证过程。

现在您已经验证了您的电子邮件地址，您可以发送第一封电子邮件了。转到 **AWS SES 控制台**，然后选择 **发送一封电子邮件**。

![发送一封电子邮件](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/02-send-email.png)

在 **Send a Single Email** 页面上，输入以下信息：

* **发件人**：输入您要用于发送电子邮件的经过验证的电子邮件地址。
* **收件人**：输入收件人的电子邮件地址。
* **主题**：输入电子邮件的主题。
* **消息**：输入电子邮件的正文。您可以使用 **可视化编辑器** 或 **HTML 编辑器** 来格式化电子邮件。

完成后，选择 **发送电子邮件**。

![发送电子邮件](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/03-send-email.png)

电子邮件发送成功后，您应该会收到一封来自 AWS SES 的确认电子邮件。

## 使用 AWS SES 接收电子邮件

除了发送电子邮件，您还可以使用 AWS SES 接收电子邮件。您可以使用 AWS SES 在您的邮箱中接收电子邮件或将传入的电子邮件路由到其他 AWS 服务，例如 Amazon S3 或 Amazon Lambda。

要设置电子邮件接收，您首先需要在AWS SES中[设置规则集](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/receiving-email-getting-started.html)安慰。规则集包含一个或多个规则，这些规则决定 AWS SES 如何处理传入的电子邮件。

![规则集](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/04-rule-sets.png)

要设置规则集，请从菜单中选择 **Rule Sets**，然后选择 **Create a Rule Set**。在 **Create a Rule Set** 页面上，输入规则集的名称并选择 **Create Rule Set**。

![创建规则集](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/05-create-rule-set.png)

创建规则集后，您可以向其中添加规则。规则由一组条件和一个操作组成。当传入的电子邮件满足规则的条件时，将执行操作。

要向规则集中添加规则，请选择 **添加规则** 并输入以下信息：

* **名称**：输入规则的名称。
* **描述**：输入规则的描述。
* **范围**：选择规则是适用于所有电子邮件还是仅适用于满足特定条件的电子邮件。
* **收件人**：输入您要接收电子邮件的电子邮件地址。
* **操作**：选择您希望 AWS SES 在触发规则时执行的操作。您可以选择将电子邮件保存到 Amazon S3 存储桶、将其发送到 Amazon Lambda 函数或将其转发到另一个电子邮件地址。

完成后，选择 **创建规则**。

![创建规则](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/06-create-rule.png)

现在您已经创建了一个规则集并向其中添加了一个规则，您就可以接收电子邮件了。要测试您的设置，请向您在规则中指定的电子邮件地址发送电子邮件。您应该会在您的邮箱或您指定的 Amazon S3 存储桶中收到电子邮件。

## 结论

在本文中，我们讨论了如何使用 AWS Simple Email Service 发送和接收电子邮件。我们还展示了如何设置规则集来处理传入的电子邮件。

AWS SES 是一种经济高效且可扩展的电子邮件发送和接收方式。它易于设置和使用，并且与其他 AWS 服务集成。如果您需要在应用程序中发送或接收电子邮件，我们建议使用 AWS SES。

## 其他资源

如果您想了解有关 AWS SES 的更多信息，我们推荐以下资源：

* [AWS SES 开发人员指南](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/Welcome.html)
* [使用 Amazon SES 发送电子邮件](https://aws.amazon.com/ses/sending-email/)
* [使用 Amazon SES 接收电子邮件](https://aws.amazon.com/ses/receiving-email/)