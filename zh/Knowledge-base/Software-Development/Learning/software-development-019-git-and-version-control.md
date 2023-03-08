---
title: 软件开发 019：Git 和版本控制
description: 
published: true
date: 2023-02-13T08:56:32.776Z
tags: 
editor: markdown
dateCreated: 2023-02-13T08:56:31.060Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Software Development 019: Git and Version Control***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-019-git-and-version-control)
{.links-list}


# 软件开发 019：Git 和版本控制

## 什么是 Git？

Git 是一个免费的开源分布式版本控制系统，旨在快速高效地处理从小型项目到大型项目的所有内容。

## 什么是版本控制？

版本控制是一个系统，它记录一个文件或一组文件随时间的变化，以便您以后可以调用特定版本。例如，当您正在开发一款软件时，您可能希望在工作时保存不同版本的代码。版本控制系统允许您这样做。

## 为什么使用 Git？

使用 Git 进行版本控制的原因有很多。 Git 速度快、可扩展，并且拥有庞大的用户社区。 Git 也很容易学习并且有很好的文档。

## 如何使用 Git

Git 是一个命令行工具，但有许多图形用户界面 (GUI) 提供 Git 工作流的图形表示。我们将在本教程中使用命令行，但如果您愿意，也可以随意使用 GUI。

## 安装 Git

Git 适用于所有主要操作系统。访问[Git网站](https://git-scm.com/)下载并安装Git。

## 配置 Git

在使用 Git 之前，您需要对其进行配置。运行以下命令来设置您的用户名：

```
git config --global user.name "Your Name"
```

将“您的姓名”替换为您的真实姓名。

接下来，设置您的电子邮件地址：

```
git config --global user.email "your_email@example.com"
```

将“your_email@example.com”替换为您的实际电子邮件地址。

最后，设置您的默认文本编辑器：

```
git config --global core.editor nano
```

您可以用您喜欢的文本编辑器替换“nano”。

## 创建一个 Git 仓库

Git 存储库是文件的集合以及这些文件的更改历史记录。您可以使用 `git init` 命令创建一个新的 Git 存储库。

## 克隆一个 Git 仓库

如果您想使用现有的 Git 存储库，可以使用 `git clone` 命令克隆它。克隆存储库会创建远程存储库的本地副本。

## Git 基础知识

现在您已经有了一个 Git 存储库，您可以开始使用它了。

### 将文件添加到存储库

您可以使用 `git add` 命令将文件添加到 Git 存储库。此命令将文件添加到暂存区，暂存区是更改的临时保存区。

### 提交更改

添加完所有要提交的文件后，您可以使用 `git commit` 命令将它们提交到存储库。此命令将您的更改保存到 Git 历史记录中。

### 查看提交历史

您可以使用 `git log` 命令查看提交历史记录。此命令显示当前分支中所有提交的列表，从最近的提交开始。

### 检查文件的状态

您可以使用 `git status` 命令检查 Git 存储库中文件的状态。此命令显示自上次提交以来已修改的所有文件的列表。

### 查看差异

您可以使用 `git diff` 命令查看文件的当前版本与 Git 存储库中的版本之间的差异。此命令对于在提交文件之前查看您对文件所做的更改很有用。

## Git 分支

Git 分支用于创建隔离的开发环境。您可以将分支视为单独的开发线。

### 创建分支

您可以使用 `git branch` 命令创建一个新分支。

### 切换分支

您可以使用 `git checkout` 命令在分支之间切换。

### 合并分支

您可以使用 `git merge` 命令合并两个分支。

## Git 远程

Git remote 用于管理远程仓库。远程存储库是不在本地计算机上的存储库。

### 添加远程

您可以使用 `git remote add` 命令添加远程存储库。

### 从远程获取

您可以使用 `git fetch` 命令从远程存储库中获取更改。

### 推送到远程

您可以使用 `git push` 命令将更改推送到远程存储库。

## Git 标签

Git 标签用于标记 Git 历史记录中的特定点。标签通常用于标记发布点。

### 创建标签

您可以使用 `git tag` 命令创建标签。

### 推送标签

您可以使用 `git push` 命令将标签推送到远程存储库。

## Git 别名

Git 别名用于为 Git 命令创建快捷方式。

您可以使用 `git config` 命令创建别名。例如，要为 `git status` 命令创建别名，您可以运行以下命令：

```
git config --global alias.st status
```

您现在可以使用 `git st` 命令来运行 `git status` 命令。

## Git 钩子

Git 挂钩是当 Git 存储库中发生某些事件时自动运行的脚本。 Git 钩子对于自动化任务很有用。

Git 钩子存储在 .git/hooks 目录中。

## Gitignore

Gitignore 用于忽略不应被 Git 跟踪的文件。例如，您可能希望忽略临时文件或日志文件。

您可以在 Git 存储库的根目录中创建一个 .gitignore 文件。 `.gitignore` 文件应该包含要忽略的模式列表。

## Git 流程

Git 流程是一组用于管理 Git 存储库中的分支的约定。 Git flow 旨在简化分支的工作。

## GitLab

GitLab 是一个基于 Web 的 Git 存储库管理器。 GitLab 提供了一个用于管理 Git 存储库的 Web 界面。 GitLab 还提供问题跟踪、持续集成和代码审查的功能。

## GitHub

GitHub 是一个基于 Web 的 Git 存储库托管服务。 GitHub 提供了一个用于管理 Git 存储库的 Web 界面。 GitHub 还提供问题跟踪、持续集成和代码审查的功能。

## 比特桶

Bitbucket 是一种基于 Web 的 Git 存储库托管服务。 Bitbucket 提供了一个用于管理 Git 存储库的 Web 界面。 Bitbucket 还提供问题跟踪、持续集成和代码审查功能。

## 外部资源

- [Git 文档](https://git-scm.com/doc)
- [Pro Git 书籍](https://git-scm.com/book/en/v2)
- [学习 Git 分支](https://learngitbranching.js.org/)