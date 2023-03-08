---
title: AWS 和 Azure 上的持续集成和持续部署
description: 
published: true
date: 2023-02-04T16:55:55.241Z
tags: 
editor: markdown
dateCreated: 2023-02-04T16:55:49.803Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Continuous Integration and Continuous Deployment on AWS and Azure***English** document is available*](/en/Knowledge-base/Cloud/continuous-integration-and-continuous-deployment-on-aws-and-azure)
{.links-list}


# 在 AWS 和 Azure 上持续集成和持续部署

AWS 和 Azure 等云平台为开发人员提供了许多好处，包括快速扩展资源的能力以及使用各种编程语言和工具的灵活性。这些平台还可以轻松设置持续集成 (CI) 和持续部署 (CD) 管道。

在本文中，我们将了解如何在 AWS 和 Azure 上设置 CI/CD 管道。我们还将讨论将这些平台用于 CI/CD 的一些好处和挑战。

## 什么是持续集成？

持续集成 (CI) 是在代码更改时自动构建和测试代码更改的做法。这使开发人员能够快速检测和修复错误，并有助于确保代码库始终处于可部署状态。

 CI 管道通常由代码提交触发，它们通常包括以下步骤：

- 代码是自动构建和测试的。
- 运行自动化测试以检查错误。
- 如果测试通过，代码将部署到暂存环境。
- 如果测试失败，则不部署代码并通知开发人员。

## 什么是持续部署？

持续部署 (CD) 是将代码更改自动部署到生产环境的做法。这使开发人员能够尽快为用户提供新功能和修复。

CD 管道通常包括以下步骤：

- 代码是自动构建和测试的。
- 如果测试通过，则将代码部署到生产环境。
- 如果测试失败，则不部署代码并通知开发人员。

## 在 AWS 上设置 CI/CD 管道

AWS 提供了许多可用于设置 CI/CD 管道的服务。在本节中，我们将了解如何使用 AWS CodePipeline 和 AWS CodeBuild 设置简单的 CI/CD 管道。

### 先决条件

在开始之前，您需要具备以下条件：

- 一个 AWS 账户
- 一个 GitHub 帐户
- GitHub 中的代码存储库

### 设置 AWS CodePipeline

AWS CodePipeline 是一项服务，可用于自动执行构建、测试和部署代码更改的过程。

要使用 CodePipeline 设置 CI 管道，您需要创建一个新的 CodePipeline 管道。为此，请登录 AWS 控制台并导航至 CodePipeline 服务。

单击“创建管道”按钮开始。

在“选择管道设置”页面上，为您的管道命名并选择一个区域。然后，单击“下一步”按钮。

在“添加源”页面上，选择“GitHub”作为源提供者。然后，选择要用于管道的存储库和分支。最后，单击“下一步”按钮。

在“添加构建阶段”页面上，选择“AWS CodeBuild”作为构建提供程序。然后，为您的构建阶段选择一个名称并单击“下一步”按钮。

在“Configure Build Stage”页面上，选择“Linux, Ubuntu”操作系统和“Standard”运行时。然后，选择“aws/codebuild/standard:4.0”图像。

在“EnvironmentVariables”部分，添加以下环境变量：

- “名称”：“REPOSITORY_NAME”
- "Value": "你的 GitHub 仓库名称"

在“BuildSpec”部分，输入以下构建命令：

- “版本：0.2”
- “阶段：”
- “pre_build：”
- “命令：”
- “echo 正在登录 GitHub……”
- "${{git-credential}} 填写"
- “建造：”
- “命令：”
- “echo Build 于 `date` 开始”
——《回声建筑工地……》
- “雨果”
- “post_build：”
- “命令：”
- “echo 构建于 `date` 完成”

单击“保存构建项目”按钮以保存您的构建项目。

在“添加部署阶段”页面上，选择“AWS CodeDeploy”作为部署提供程序。然后，为您的部署阶段选择一个名称并单击“下一步”按钮。

在“Configure Deploy Stage”页面上，选择“EC2/on-premises”实例类型和“Default”部署类型。然后，输入以下部署配置：

- “应用程序名称”：“您的 GitHub 存储库名称”
- "Deployment Group Name": "你的GitHub仓库名称-deploy"
- “服务角色 ARN”：“arn:aws:iam::aws:policy/service-role/AWSCodeDeployRole”

单击“保存部署组”按钮以保存您的部署组。

在“审查”页面上，审查您的管道设置，然后单击“创建管道”按钮。

您的 CI 管道现在可以使用了。每当您将代码更改提交到 GitHub 存储库时，CodePipeline 都会自动构建和部署您的代码。

## 在 Azure 上设置 CI/CD 管道

Azure 提供了许多可用于设置 CI/CD 管道的服务。在本节中，我们将了解如何使用 Azure DevOps 和 Azure Pipelines 设置简单的 CI/CD 管道。

### 先决条件

在开始之前，您需要具备以下条件：

- 一个 Azure 帐户
- 一个 GitHub 帐户
- GitHub 中的代码存储库

### 设置 Azure DevOps

Azure DevOps 是一种服务，可用于自动执行构建、测试和部署代码更改的过程。

要使用 Azure DevOps 设置 CI 管道，您需要创建一个新的 Azure DevOps 项目。为此，请登录到 Azure 门户并导航到 Azure DevOps 服务。

单击“新建项目”按钮开始。

为您的项目命名，然后单击“创建”按钮。

您的 Azure DevOps 项目现在可以使用了。

### 设置 Azure 管道

Azure Pipelines 是一种服务，可用于自动执行构建、测试和部署代码更改的过程。

要使用 Azure Pipelines 设置 CI 管道，您需要创建一个新的 Azure Pipeline。为此，请登录到 Azure 门户并导航到 Azure Pipelines 服务。

单击“新建管道”按钮开始。

在“选择源”页面上，选择“GitHub”作为源提供者。然后，选择要用于管道的存储库和分支。最后，单击“继续”按钮。

在“Select a Template”页面上，选择“Starter pipeline”模板并单击“Continue”按钮。

在“配置您的管道”页面上，输入以下 YAML 代码：

- 扳机：
- 分支机构：
- 包括：
- 掌握
- 小路： /
- 自述文件.md
- 阶段：
- - 阶段：构建
- 工作：
- - 工作：建造
- 脚步：
- - 结帐：自己
- - 任务：UseDotNet@2
- 输入：
- 包类型：sdk
- 版本：3.1.100
- - 任务：DotNetCoreCLI@2
- 输入：
- 命令：构建
- 参数：--配置发布
- - 阶段：测试
- 工作：
- - 工作：测试
- 脚步：
- - 结帐：自己
- - 任务：DotNetCoreCLI@2
- 输入：
- 命令：测试
- 参数：--no-build --configuration Release
- - 阶段：部署
- 工作：
- - 工作：部署
- 脚步：
- - 结帐：自己
- - 任务：CopyFiles@2
- 输入：
- SourceFolder: '$(Pipeline.Workspace)'
- 内容： '**/*'
- 目标文件夹：'$(Build.ArtifactStagingDirectory)'
- - 任务：PublishBuildArtifacts@1
- 输入：
- PathtoPublish：'$(Build.ArtifactStagingDirectory)'
- 工件名称：'drop'
- 发布位置：'容器'

单击“保存并运行”按钮以保存您的管道并运行它。

您的 CI 管道现在可以使用了。每当您将代码更改提交到 GitHub 存储库时，Azure Pipelines 都会自动构建和部署您的代码。

## 结论

在本文中，我们了解了如何在 AWS 和 Azure 上设置 CI/CD 管道。我们还讨论了将这些平台用于 CI/CD 的一些好处和挑战。