---
title: 软件开发 069：事件溯源和 CQRS
description: 
published: true
date: 2023-02-02T21:57:25.733Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:57:21.114Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Software Development 069: Event Sourcing and CQRS***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-069-event-sourcing-and-cqrs)
{.links-list}


# 软件开发 069：事件溯源和 CQRS

## 什么是事件溯源？

事件溯源是一种软件开发方法，其中对应用程序状态的所有更改都存储为一系列事件。这一系列事件称为事件日志。

## 事件溯源的好处是什么？

使用事件溯源有很多好处，包括：

- 对应用程序状态的所有更改都存储在事件日志中，这使得调试问题和跟踪更改变得容易。

- 事件日志可用于重播事件并重新创建应用程序的状态，这对于测试和开发目的很有用。

- 事件溯源可用于实现撤消/重做功能。

- 事件日志可用于生成报告和分析。

## 什么是 CQRS？

CQRS 是一种软件开发方法，它将应用程序的读取和写入操作分为两个独立的模型。

## CQRS 有什么好处？

使用 CQRS 有很多好处，包括：

- 读写操作可以独立缩放，从而提高性能。

- 可以使用不同的技术实现读写模型，这可以提高灵活性。

- CQRS 可以简化复杂应用程序的开发。

## 什么是事件溯源 + CQRS？

Event Sourcing + CQRS 是一种结合了 Event Sourcing 和 CQRS 优势的软件开发方法。

## Event Sourcing + CQRS 有什么好处？

使用 Event Sourcing + CQRS 有很多好处，包括：

- 对应用程序状态的所有更改都存储在事件日志中，这使得调试问题和跟踪更改变得容易。

- 事件日志可用于重播事件并重新创建应用程序的状态，这对于测试和开发目的很有用。

- 事件溯源可用于实现撤消/重做功能。

- 事件日志可用于生成报告和分析。

- 读写操作可以独立缩放，从而提高性能。

- 可以使用不同的技术实现读写模型，这可以提高灵活性。

- CQRS 可以简化复杂应用程序的开发。