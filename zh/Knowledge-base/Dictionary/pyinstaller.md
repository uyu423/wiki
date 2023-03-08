---
title: PyInstaller
description: 
published: true
date: 2023-02-07T04:19:01.489Z
tags: 
editor: markdown
dateCreated: 2023-02-07T04:18:59.643Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [PyInstaller***English** document is available*](/en/Knowledge-base/Dictionary/pyinstaller)
{.links-list}


# 概述
PyInstaller 是一个在 Windows、Mac 和 Linux 下将 Python 程序打包成独立可执行文件的程序。它旨在供需要将应用程序分发给可能安装或未安装 Python 的用户的 Python 开发人员使用。

# 描述
PyInstaller 是一个免费的开源工具，用于将 Python 程序转换为独立的可执行文件。它旨在供需要将应用程序分发给可能安装或未安装 Python 的用户的 Python 开发人员使用。该程序通过分析 Python 程序并收集运行它所需的必要文件和库来工作。然后它将这些文件打包成一个可以在任何机器上运行的可执行文件，无论是否安装了 Python。

PyInstaller 支持 Python 2.7、3.4、3.5、3.6 和 3.7，可以打包适用于 Windows、Mac 和 Linux 的应用程序。它还可以将 Python 程序打包为单个文件可执行文件，这对于在不泄露源代码的情况下分发应用程序非常有用。

# 历史
PyInstaller 于 2005 年首次发布，目前由一组志愿者维护。自首次发布以来，它的受欢迎程度稳步增长，截至 2020 年下载量超过 200 万次。

# 特征
PyInstaller 具有许多对 Python 开发人员有用的功能。这些包括：

- 支持多平台：PyInstaller 可以为 Windows、Mac 和 Linux 打包应用程序。
- 单文件可执行文件：PyInstaller 可以将 Python 程序打包为单文件可执行文件，这对于在不泄露源代码的情况下分发应用程序非常有用。
- 自动依赖检测：PyInstaller 自动检测并打包运行 Python 程序所需的必要文件和库。
- 捆绑的 Python 解释器：PyInstaller 可以将 Python 解释器与应用程序捆绑在一起，允许它在没有安装 Python 的机器上运行。

# 例子
在这个例子中，我们将使用 PyInstaller 将一个简单的 Python 程序打包成一个独立的可执行文件。该程序打印字符串“Hello, world!”到控制台。

首先，我们创建一个名为“hello.py”的文件，内容如下：

```
print("Hello, world!")
```

接下来，我们运行以下命令将程序打包成独立的可执行文件：

```
pyinstaller hello.py
```

PyInstaller 将创建一个名为“dist”的文件夹，其中包含可执行文件。这个文件可以在任何机器上运行，不管是否安装了 Python。

# 优点和缺点
优点

- 易于使用：PyInstaller 易于使用，只需最少的设置。
- 跨平台：PyInstaller 可以为 Windows、Mac 和 Linux 打包应用程序。
- 单文件可执行文件：PyInstaller 可以将 Python 程序打包为单文件可执行文件，这对于在不泄露源代码的情况下分发应用程序非常有用。

缺点

- 有限支持：PyInstaller 仅支持 Python 2.7、3.4、3.5、3.6 和 3.7。
- 无 GUI：PyInstaller 没有 GUI，因此必须从命令行使用。

# 相关技术
PyOxidizer 是另一种将 Python 程序打包成独立可执行文件的工具。它被设计成比 PyInstaller 更健壮、功能更丰富，但仍处于早期开发阶段。