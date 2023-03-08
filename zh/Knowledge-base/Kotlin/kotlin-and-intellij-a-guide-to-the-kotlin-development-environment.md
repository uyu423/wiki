---
title: Kotlin 和 IntelliJ：Kotlin 开发环境指南
description: 
published: true
date: 2023-02-01T12:23:40.941Z
tags: 
editor: markdown
dateCreated: 2023-02-01T12:23:37.504Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Kotlin and IntelliJ: A Guide to the Kotlin Development Environment***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-intellij-a-guide-to-the-kotlin-development-environment)
{.links-list}



# Kotlin 和 IntelliJ：Kotlin 开发环境指南

Kotlin 是一种静态类型的编程语言，运行在 Java 虚拟机上，可用于开发 Android 应用程序。 IntelliJ IDEA 是用于开发 Kotlin 应用程序的流行 IDE。在本指南中，我们将向您展示如何使用 IntelliJ IDEA 设置 Kotlin 开发环境。

## 安装 IntelliJ IDEA

首先，您需要[下载](https://www.jetbrains.com/idea/download/) 并安装 IntelliJ IDEA。我们推荐 Ultimate Edition，它包含 Kotlin 开发所需的所有功能。

安装 IntelliJ IDEA 后，您需要安装 Kotlin 插件。为此，请打开 IntelliJ IDEA 并转到_Configure > Plugins_。在 _Marketplace_ 选项卡中，搜索 `Kotlin` 并安装插件。

## 创建一个新的 Kotlin 项目

要创建新的 Kotlin 项目，请打开 IntelliJ IDEA 并选择_File > New > Project_。在 _New Project_ 向导中，选择 _Kotlin > JVM > Kotlin/JVM Project_ 并单击 _Next_。

![新 Kotlin/JVM 项目](https://kotlinlang.org/assets/images/tools/intellij/new-kotlin-project-2.png)

在 _Project Settings_ 页面上，指定项目名称和位置。我们建议使用项目 SDK 和 Kotlin 版本的默认设置。

![项目设置](https://kotlinlang.org/assets/images/tools/intellij/new-kotlin-project-3.png)

在 _Libraries_ 页面上，选择 _Java SDK_ 并单击 _Next_。

![库](https://kotlinlang.org/assets/images/tools/intellij/new-kotlin-project-4.png)

在 _Framework Selection_ 页面上，选择 _Kotlin DSL_ 并单击 _Finish_。

![框架选择](https://kotlinlang.org/assets/images/tools/intellij/new-kotlin-project-5.png)

## 配置 Kotlin 编译器

默认情况下，Kotlin 编译器使用 _Java 1.6_ 字节码级别。我们建议将其更改为 _Java 8_，这是某些 Kotlin 功能所必需的，例如 lambda。为此，请打开_Project Structure_ 对话框（_File > Project Structure_）并转到_Project Settings > Modules > Sources_。在 _Kotlin Compiler_ 部分，将 _Target bytecode version_ 更改为 _1.8_ 并单击 _Apply_。

![项目结构](https://kotlinlang.org/assets/images/tools/intellij/project-structure-1.png)

## 配置 Kotlin 风格

我们建议您遵循 Kotlin 的一套[风格指南](https://kotlinlang.org/docs/reference/coding-conventions.html)。 IntelliJ IDEA 可以通过提供代码检查和快速修复来帮助您遵循这些准则。要启用这些功能，请转到_File > Settings > Editor > Inspections_ 并选择_Kotlin_ inspection profile。

![检查](https://kotlinlang.org/assets/images/tools/intellij/inspections-1.png)

## 使用 Kotlin REPL

Kotlin REPL（Read-Eval-Print-Loop）是一个用于快速测试 Kotlin 代码的便捷工具。要启动 Kotlin REPL，请打开 _Tools_ 菜单并选择 _Kotlin > Kotlin REPL_。

![Kotlin REPL](https://kotlinlang.org/assets/images/tools/intellij/repl-1.png)

## 结论

在本指南中，我们向您展示了如何使用 IntelliJ IDEA 设置 Kotlin 开发环境。我们还介绍了一些可用的基本配置选项和功能。