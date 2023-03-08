---
title: Linux系统启动和初始化
description: 
published: true
date: 2023-02-11T04:55:12.973Z
tags: 
editor: markdown
dateCreated: 2023-02-11T04:55:11.368Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Linux System Startup and Initialization***English** document is available*](/en/Knowledge-base/Linux/linux-system-startup-and-initialization)
{.links-list}


# Linux系统启动和初始化

每当启动 Linux 系统时，都会启动许多进程来初始化系统。此过程称为系统启动或初始化，通常按以下顺序发生：

1. ** BIOS **
2. **主引导记录（MBR）**
3. **引导加载程序**
4.**内核**
5. **初始化进程**
6.**用户空间**

## BIOS

基本输入/输出系统 (BIOS) 是计算机启动时首先运行的系统。它负责通过读取包含引导加载程序的硬盘驱动器的引导扇区来引导计算机。

## 主引导记录 (MBR)

MBR是一小段代码，负责加载boot loader。它通常位于硬盘驱动器的第一个扇区。

## 引导装载程序

引导加载程序是负责加载操作系统内核的程序。 Linux 系统上最常用的引导加载程序是 GRUB（Grand Unified Bootloader）。

## 核心

内核是操作系统的核心，负责管理系统的资源，如内存、设备和进程。

## 初始化进程

init 进程是内核启动的第一个进程。它负责启动系统上的所有其他进程。

## 用户空间

在 init 进程启动了所有其他必要的进程后，系统就进入了用户空间。这是普通用户可以登录和运行程序的地方。