---
title: 使用 Jenkins 和 IntelliJ 设置持续集成管道
description: 
published: true
date: 2023-02-13T13:18:15.332Z
tags: 
editor: markdown
dateCreated: 2023-02-13T13:18:08.213Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Setting up a Continuous Integration Pipeline with Jenkins and IntelliJ***English** document is available*](/en/Knowledge-base/Backend/setting-up-a-continuous-integration-pipeline-with-jenkins-and-intellij)
{.links-list}


# 使用 Jenkins 和 IntelliJ 建立持续集成管道

## 介绍

持续集成 (CI) 是一种开发实践，要求开发人员每天多次将代码集成到共享存储库中。然后通过自动构建验证每次签入，使团队能够及早发现问题。

设置 CI 管道可能是一项艰巨的任务，但使用正确的工具可以相对简单。在本文中，我们将向您展示如何使用 Jenkins 和 IntelliJ 设置 CI 管道。

## 你需要什么

- 一个 GitHub 帐户
- 詹金斯服务器
- IntelliJ IDEA

## 第 1 步：创建 GitHub 存储库

第一步是为您的项目创建一个 GitHub 存储库。为此，请前往 GitHub 并创建一个新的存储库。

![创建一个新的 GitHub 存储库](https://i.imgur.com/EuU8GtO.png)

命名您的存储库并单击“创建存储库”。

![为您的存储库命名](https://i.imgur.com/VNcuCY5.png)

## 第 2 步：创建 Jenkins 作业

接下来，我们需要创建一个 Jenkins 作业。 Jenkins 作业是 Jenkins 可以执行的任务。在我们的例子中，Jenkins 作业将从 GitHub 检出我们的代码，构建它，并运行我们的测试。

要创建 Jenkins 作业，请转到您的 Jenkins 服务器并单击“新建作业”。

![詹金斯新工作](https://i.imgur.com/pLJnV1N.png)

为您的工作命名并选择“Freestyle project”。

![詹金斯工作名称](https://i.imgur.com/lGZm4z3.png)

单击“确定”。

在下一页上，向下滚动到“源代码管理”部分并选择“Git”。

![Jenkins 源代码管理](https://i.imgur.com/Lg4U4jf.png)

在“存储库 URL”字段中，输入 GitHub 存储库的 URL。

![Jenkins 存储库 URL](https://i.imgur.com/VkzM0cw.png)

向下滚动到“构建”部分，然后单击“添加构建步骤”。选择“执行外壳”。

![Jenkins 构建部分](https://i.imgur.com/KJ3fZUO.png)

在“命令”字段中，输入以下命令：

```
mvn clean install
```

此命令将清理我们的项目、安装任何依赖项并运行我们的测试。

向下滚动到“构建后操作”部分，然后单击“添加构建后操作”。选择“发布JUnit测试结果报告”。

![Jenkins 构建后操作](https://i.imgur.com/NDYaTGi.png)

在“测试报告 XML”字段中，输入以下内容：

```
**/target/surefire-reports/*.xml
```

这将告诉 Jenkins 发布我们的测试结果。

单击“保存”。

## 第 3 步：设置 IntelliJ

现在我们已经设置了 Jenkins 作业，我们需要配置我们的 IDE。在本节中，我们将向您展示如何设置 IntelliJ 以在我们更改代码时触发 Jenkins 服务器上的构建。

打开 IntelliJ 并导航到“文件”菜单。选择“设置”。

![IntelliJ 设置](https://i.imgur.com/mEUDKjK.png)

在“设置”窗口中，导航至“构建、执行、部署”>“持续集成”。选择“詹金斯”。

![IntelliJ 詹金斯](https://i.imgur.com/VkzM0cw.png)

在“Jenkins URL”字段中，输入您的 Jenkins 服务器的 URL。

![IntelliJ Jenkins 网址](https://i.imgur.com/dc9gKbD.png)

在“项目名称”字段中，输入您的 Jenkins 作业的名称。

![IntelliJ 项目名称](https://i.imgur.com/P0zM0cw.png)

单击“确定”。

## 第 4 步：触发构建

现在我们的 Jenkins 作业已经设置好并且我们的 IDE 已经配置好了，我们准备好触发构建了。为此，请更改您的代码并将其推送到 GitHub。

![IntelliJ 推送到 GitHub](https://i.imgur.com/VkzM0cw.png)

将代码推送到 GitHub 后，Jenkins 将自动检测更改、签出代码、构建代码并运行测试。

![詹金斯构建](https://i.imgur.com/u4JnV1N.png)

您可以通过单击“构建历史”部分中的“构建”链接来查看构建结果。

![Jenkins 构建历史](https://i.imgur.com/VkzM0cw.png)

## 结论

在本文中，我们向您展示了如何使用 Jenkins 和 IntelliJ 设置 CI 管道。虽然这是一个简单的管道，但它可以轻松扩展以包含其他步骤，例如部署到暂存或生产环境。