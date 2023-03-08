---
title: 使用 apt 和 yum 进行 Linux 包管理
description: 
published: true
date: 2023-02-12T09:32:25.387Z
tags: 
editor: markdown
dateCreated: 2023-02-12T09:32:18.637Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Linux Package Management with apt and yum***English** document is available*](/en/Knowledge-base/Linux/linux-package-management-with-apt-and-yum)
{.links-list}



# 使用 apt 和 yum 管理 Linux 包

包管理是任何 Linux 发行版的重要组成部分。它允许您从系统中安装、更新和删除软件包。在本文中，我们将了解两种最流行的包管理工具：apt 和 yum。

## 贴切

apt（高级包工具）是 Debian 和 Ubuntu 系统的默认包管理器。它是一个强大的工具，可用于从系统中安装、更新和删除软件包。 apt 还能够解决依赖关系，因此您不必担心为特定软件包手动安装所有必需的依赖关系。

要使用 apt 安装软件包，可以使用以下命令：

```
sudo apt install {package-name}
```

例如，要安装“vim”文本编辑器，您可以使用以下命令：

```
sudo apt install vim
```

如果要更新系统上的所有软件包，可以使用以下命令：

```
sudo apt update
```

要将系统上的所有软件包升级到最新版本，可以使用以下命令：

```
sudo apt upgrade
```

如果要从系统中删除软件包，可以使用以下命令：

```
sudo apt remove {package-name}
```

例如，要删除“vim”文本编辑器，您可以使用以下命令：

```
sudo apt remove vim
```

## 百胜

yum (Yellowdog Updater Modified) 是 Red Hat 和 CentOS 系统的默认包管理器。它是一个强大的工具，可用于从系统中安装、更新和删除软件包。 yum 还能够解决依赖关系，因此您不必担心为特定软件包手动安装所有必需的依赖关系。

要使用 yum 安装软件包，可以使用以下命令：

```
sudo yum install {package-name}
```

例如，要安装“vim”文本编辑器，您可以使用以下命令：

```
sudo yum install vim
```

如果要更新系统上的所有软件包，可以使用以下命令：

```
sudo yum update
```

要将系统上的所有软件包升级到最新版本，可以使用以下命令：

```
sudo yum upgrade
```

如果要从系统中删除软件包，可以使用以下命令：

```
sudo yum remove {package-name}
```

例如，要删除“vim”文本编辑器，您可以使用以下命令：

```
sudo yum remove vim
```

## 结论

在本文中，我们了解了两种最流行的包管理工具：apt 和 yum。这两个工具都非常强大，可用于管理系统上的软件包。