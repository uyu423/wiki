---
title: 如何使用 Git 和 GitHub 进行版本控制
description: 
published: true
date: 2023-02-02T06:29:37.212Z
tags: 
editor: markdown
dateCreated: 2023-02-02T06:23:35.069Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [How to Use Git and GitHub for Version Control***English** document is available*](/en/Knowledge-base/Common/how-to-use-git-and-github-for-version-control)
{.links-list}


# 如何使用 Git 和 GitHub 进行版本控制

Git 是开发人员的强大工具，允许他们跟踪代码更改、与他人合作开展协作项目以及与世界共享他们的代码。 GitHub 是一种流行的在线服务，用于托管和管理 Git 存储库。在本文中，我们将向您展示如何使用 Git 和 GitHub 进行版本控制。

## 什么是版本控制？

版本控制是一个跟踪文件随时间变化的系统。这对开发人员很有用，因为它允许他们撤消更改、试验新功能以及在代码项目上与其他人协作。

## 什么是 Git？

Git 是一个版本控制系统，由 Linux 操作系统的创建者 Linus Torvalds 创建。 Git 是一种免费的开源工具，被开发人员广泛使用。

## 什么是 GitHub？

GitHub 是一种流行的在线服务，用于托管和管理 Git 存储库。 GitHub 使代码项目协作和跟踪代码更改变得容易。

## 如何使用 Git 和 GitHub 进行版本控制

在本节中，我们将向您展示如何使用 Git 和 GitHub 进行版本控制。

### 如何安装 Git

Git 是一款免费的开源工具，可从 [Git 网站](https://git-scm.com/) 下载。要安装 Git，请按照适用于您的操作系统的说明进行操作：

- [视窗](https://git-scm.com/downloads/windows)
- [macOS](https://git-scm.com/downloads/mac)
- [Linux](https://git-scm.com/downloads/linux)

### 如何创建 Git 存储库

Git 存储库是由 Git 跟踪的文件集合。要创建新的 Git 存储库，请使用 `git init` 命令：

```
$ git init
```

### 如何将文件添加到 Git 存储库

创建 Git 存储库后，您可以使用 `git add` 命令向其中添加文件。要将文件添加到 Git 存储库，请使用 `git add` 命令，后跟文件路径：

```
$ git add filename
```

您还可以使用带有“-A”选项的“git add”命令将目录中所有已修改和未跟踪的文件添加到 Git 存储库：

```
$ git add -A
```

### 如何提交对 Git 存储库的更改

将文件添加到 Git 存储库后，您可以使用 `git commit` 命令将这些更改提交到存储库。要将更改提交到 Git 存储库，请使用 `git commit` 命令，后跟一条描述更改的消息：

```
$ git commit -m "message"
```

### 如何将更改推送到远程 Git 存储库

将更改提交到 Git 存储库后，您可以使用 `git push` 命令将这些更改推送到远程存储库。要将更改推送到远程 Git 存储库，请使用 `git push` 命令，后跟远程存储库的名称：

```
$ git push origin
```

### 如何创建 GitHub 存储库

GitHub 是一种流行的在线服务，用于托管和管理 Git 存储库。要创建新的 GitHub 存储库，请注册一个 GitHub 帐户，然后从 GitHub 网站创建一个新的存储库。

### 如何将现有的 Git 存储库推送到 GitHub

如果您有现有的 Git 存储库，则可以使用 `git push` 命令将其推送到 GitHub。要将现有的 Git 存储库推送到 GitHub，请使用 `git push` 命令，后跟 `-u` 选项和远程存储库的名称：

```
$ git push -u origin
```

### 如何从远程 Git 存储库中拉取更改

如果您有远程 Git 存储库，则可以使用 `git pull` 命令从该存储库中拉取更改。要从远程 Git 存储库中拉取更改，请使用 `git pull` 命令，后跟远程存储库的名称：

```
$ git pull origin
```

## 结论

在本文中，我们向您展示了如何使用 Git 和 GitHub 进行版本控制。 Git 是开发人员的强大工具，允许他们跟踪代码更改、与他人合作开展协作项目以及与世界共享他们的代码。 GitHub 是一种流行的在线服务，用于托管和管理 Git 存储库。