---
title: Kotlin and IntelliJ: A Guide to the Kotlin Development Environment
description: 
published: true
date: 2023-02-01T12:23:38.993Z
tags: 
editor: markdown
dateCreated: 2023-02-01T12:23:37.497Z
---

- [Kotlin 및 IntelliJ: Kotlin 개발 환경 가이드***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/kotlin-and-intellij-a-guide-to-the-kotlin-development-environment)
{.links-list}
- [Kotlin 和 IntelliJ：Kotlin 开发环境指南***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/kotlin-and-intellij-a-guide-to-the-kotlin-development-environment)
{.links-list}



# Kotlin and IntelliJ: A Guide to the Kotlin Development Environment

Kotlin is a statically typed programming language that runs on the Java Virtual Machine and can be used to develop Android apps. IntelliJ IDEA is a popular IDE for developing Kotlin applications. In this guide, we will show you how to set up a Kotlin development environment using IntelliJ IDEA.

## Installing IntelliJ IDEA

First, you need to [download](https://www.jetbrains.com/idea/download/) and install IntelliJ IDEA. We recommend the Ultimate Edition, which includes all the features you need for Kotlin development.

Once you have installed IntelliJ IDEA, you need to install the Kotlin plugin. To do this, open IntelliJ IDEA and go to _Configure > Plugins_. In the _Marketplace_ tab, search for `Kotlin` and install the plugin.

## Creating a New Kotlin Project

To create a new Kotlin project, open IntelliJ IDEA and select _File > New > Project_. In the _New Project_ wizard, select _Kotlin > JVM > Kotlin/JVM Project_ and click _Next_.

![New Kotlin/JVM Project](https://kotlinlang.org/assets/images/tools/intellij/new-kotlin-project-2.png)

On the _Project Settings_ page, specify the project name and location. We recommend using the default settings for the project SDK and Kotlin version.

![Project Settings](https://kotlinlang.org/assets/images/tools/intellij/new-kotlin-project-3.png)

On the _ Libraries_ page, select the _Java SDK_ and click _Next_.

![Libraries](https://kotlinlang.org/assets/images/tools/intellij/new-kotlin-project-4.png)

On the _Framework Selection_ page, select _Kotlin DSL_ and click _Finish_.

![Framework Selection](https://kotlinlang.org/assets/images/tools/intellij/new-kotlin-project-5.png)

## Configuring the Kotlin Compiler

By default, the Kotlin compiler uses the _Java 1.6_ bytecode level. We recommend changing this to _Java 8_, which is required for some Kotlin features, such as lambdas. To do this, open the _Project Structure_ dialog ( _File > Project Structure_) and go to _Project Settings > Modules > Sources_. In the _Kotlin Compiler_ section, change the _Target bytecode version_ to _1.8_ and click _Apply_.

![Project Structure](https://kotlinlang.org/assets/images/tools/intellij/project-structure-1.png)

## Configuring Kotlin Style

Kotlin has a set of [style guidelines](https://kotlinlang.org/docs/reference/coding-conventions.html) that we recommend following. IntelliJ IDEA can help you follow these guidelines by providing code inspections and quick-fixes. To enable these features, go to _File > Settings > Editor > Inspections_ and select the _Kotlin_ inspection profile.

![Inspections](https://kotlinlang.org/assets/images/tools/intellij/inspections-1.png)

## Using the Kotlin REPL

The Kotlin REPL (Read-Eval-Print-Loop) is a handy tool for quickly testing Kotlin code. To launch the Kotlin REPL, open the _Tools_ menu and select _Kotlin > Kotlin REPL_.

![Kotlin REPL](https://kotlinlang.org/assets/images/tools/intellij/repl-1.png)

## Conclusion

In this guide, we have shown you how to set up a Kotlin development environment using IntelliJ IDEA. We have also covered some of the basic configuration options and features that are available.