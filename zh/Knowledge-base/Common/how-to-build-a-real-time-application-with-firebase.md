---
title: 如何使用 Firebase 构建实时应用程序
description: 
published: true
date: 2023-02-01T13:23:46.112Z
tags: 
editor: markdown
dateCreated: 2023-02-01T13:23:44.589Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [How to Build a Real-Time Application with Firebase***English** version of this document is available*](/en/Knowledge-base/Common/how-to-build-a-real-time-application-with-firebase)
{.links-list}



# 如何使用 Firebase 构建实时应用程序

Firebase 是一个用于构建实时应用程序的强大平台。它提供了一组丰富的功能，包括 NoSQL 数据库、用户身份验证、静态托管等。

在本文中，我们将向您展示如何使用 Firebase 构建实时应用程序。我们将使用 NoSQL 数据库来存储数据，使用用户身份验证来保护我们的应用程序，并使用静态托管来部署我们的应用程序。

## 设置 Firebase

您需要做的第一件事是创建一个 Firebase 帐户并创建一个新项目。

![Firebase 控制台](https://i.imgur.com/aVORi4k.png)

创建项目后，您将被带到项目仪表板。在这里，您可以找到您的项目 ID 和项目 URL。稍后您将需要这些。

![Firebase 项目仪表板](https://i.imgur.com/5bF9IyG.png)

## 创建一个 NoSQL 数据库

Firebase 提供了一个强大的 NoSQL 数据库来存储数据。要创建数据库，请转到 Firebase 控制台中的“数据库”选项卡，然后单击“创建数据库”按钮。

![Firebase 控制台](https://i.imgur.com/pZhCkYE.png)

系统会要求您为数据库选择安全规则。对于这个例子，我们将选择“锁定模式”，这将阻止任何人访问我们的数据库，除非他们经过身份验证。

![Firebase 控制台](https://i.imgur.com/W0zJgwc.png)

创建数据库后，就可以开始向其中添加数据。为此，请单击“添加数据”按钮。

![Firebase 控制台](https://i.imgur.com/V0CgqEH.png)

您现在可以将数据添加到数据库中。对于此示例，我们将添加一条消息。

![Firebase 控制台](https://i.imgur.com/TGiuk72.png)

## 验证用户

Firebase 提供了一个强大的身份验证系统来保护您的应用程序。要设置身份验证，请转到 Firebase 控制台中的“身份验证”选项卡，然后单击“登录方法”选项卡。

![Firebase 控制台](https://i.imgur.com/3vHKTGi.png)

单击“电子邮件/密码”登录方法并启用它。

![Firebase 控制台](https://i.imgur.com/ZU6kCbJ.png)

现在登录方法已启用，您可以创建用户。为此，转到“用户”选项卡并单击“添加用户”按钮。

![Firebase 控制台](https://i.imgur.com/XgbG0z7.png)

输入用户的电子邮件和密码，然后单击“添加用户”按钮。

![Firebase 控制台](https://i.imgur.com/V0CgqEH.png)

用户现在可以登录您的应用程序。

## 部署你的应用

Firebase 为部署您的应用程序提供静态托管服务。要设置托管，请转到 Firebase 控制台中的托管选项卡，然后单击“开始”按钮。

![Firebase 控制台](https://i.imgur.com/7DpjkZI.png)

Firebase 现在将引导您完成设置托管的过程。首先，您需要安装 Firebase CLI。

![Firebase 控制台](https://i.imgur.com/l0G9UO4.png)

安装 CLI 后，您可以部署您的应用程序。为此，请从项目目录的根目录运行以下命令。

```
firebase deploy
```

这会将您的应用程序部署到 Firebase 的服务器。

## 结论

在本文中，我们向您展示了如何使用 Firebase 构建实时应用程序。我们使用 NoSQL 数据库来存储数据，使用用户身份验证来保护我们的应用程序，并使用静态托管来部署我们的应用程序。