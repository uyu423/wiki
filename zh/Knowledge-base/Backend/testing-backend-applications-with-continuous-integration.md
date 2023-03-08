---
title: 通过持续集成测试后端应用程序
description: 
published: true
date: 2023-01-31T03:17:30.881Z
tags: 
editor: markdown
dateCreated: 2023-01-31T03:17:27.510Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Testing Backend Applications with Continuous Integration***English** version of this document is available*](/en/Knowledge-base/Backend/testing-backend-applications-with-continuous-integration)
{.links-list}


# 通过持续集成测试后端应用程序

作为后端开发人员，您有责任确保您正在开发的应用程序稳定且无错误。如果您在持续集成 (CI) 服务器上工作，这一点尤其重要，因为每个代码更改都需要在部署到生产环境之前进行验证。

测试您的代码对于避免破坏生产至关重要，但它可能非常耗时且难以正确执行。在这篇文章中，我们将讨论如何设置一个 CI 服务器来自动测试你的代码，并在任何错误时给你反馈。我们还将向您展示如何使用名为 Jenkins 的工具来自动化您的测试过程。

## 什么是持续集成？

持续集成是每天多次将所有开发人员工作副本与共享主线合并的做法。 CI 是现代软件开发过程的重要组成部分。它帮助开发人员避免在需要将来自不同开发人员的代码合并在一起时可能发生的“集成地狱”。

 CI 还有一个额外的好处，就是可以更轻松地查找和修复错误。通过更频繁地合并代码，您不太可能进行可能引入错误的大量代码更改。而且，如果错误确实进入了系统，则更容易确定是哪个代码更改引入了错误。这可以节省数小时甚至数天的开发时间。

## 设置 CI 服务器

有许多不同的 CI 服务器可用，但我们将专注于设置 Jenkins。 Jenkins 是一种流行的开源 CI 服务器，易于设置和使用。

在我们开始之前，您需要在您的服务器上安装 Jenkins。您可以在 Jenkins 网站上找到执行此操作的说明。

安装 Jenkins 后，您将需要创建一个新作业。为此，转到 Jenkins 仪表板并单击“创建新作业”。

为您的工作命名并选择“构建一个自由风格的软件项目”。然后，单击“确定”。

在下一个屏幕上，您需要配置您的作业。在“源代码管理”部分，选择“Git”选项。然后，在“存储库 URL”字段中输入 Git 存储库的 URL。

在“构建触发器”部分，选择“轮询 SCM”选项。这将告诉 Jenkins 每隔几分钟检查一次 Git 存储库是否有更改。如果愿意，您也可以选择手动触发构建。

在“Build”部分，选择“Execute Shell”选项。这将允许您在构建过程中运行 shell 命令。

在“Post-build Actions”部分，选择“Publish JUnit test result report”选项。这会将您的测试结果发布到 Jenkins，以便您稍后查看。

单击“保存”以保存您的作业配置。

## 编写测试

现在您的 CI 服务器已设置，您需要编写一些测试。测试是用一种称为 JUnit 的语言编写的，它是一种基于 Java 的测试框架。

下面是一个简单的测试，用于验证计算器类的 add 方法是否返回正确的结果：

```java
public void testAdd() {
Calculator calculator = new Calculator();
int result = calculator.add(1, 2);
assertEquals(3, result);
}
```

如果 add 方法没有返回正确的结果，这个测试就会失败。

您可以通过阅读 JUnit 文档了解有关编写测试的更多信息。

## 运行测试

一旦编写了一些测试，就需要运行它们。为此，请转到 Jenkins 仪表板并单击您的作业名称。

在作业页面上，单击“立即构建”链接。这将触发您的工作构建，它将运行您的测试。

构建完成后，您可以通过单击“构建历史”链接查看结果。这将向您显示所有已运行构建的列表。

单击最新构建以查看详细信息。在“构建输出”部分，您将看到测试结果。

## 结论

在本文中，我们讨论了如何设置 CI 服务器来自动测试您的代码。我们还向您展示了如何使用 JUnit 测试框架编写和运行测试。

通过设置 CI 服务器，您可以节省时间并减少代码中的错误数量。