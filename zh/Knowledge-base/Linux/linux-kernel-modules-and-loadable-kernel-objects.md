---
title: Linux 内核模块和可加载内核对象
description: 
published: true
date: 2023-02-11T16:32:20.351Z
tags: 
editor: markdown
dateCreated: 2023-02-11T16:32:18.723Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Linux Kernel Modules and Loadable Kernel Objects***English** document is available*](/en/Knowledge-base/Linux/linux-kernel-modules-and-loadable-kernel-objects)
{.links-list}


# Linux 内核模块和可加载内核对象

## 概述

Linux 内核模块是一段目标代码，可以在运行时加载到内核中，而无需重新编译内核。

可加载内核模块提供了一种无需重新编译内核或重新启动系统即可扩展内核功能的机制。

 内核模块可用于向内核添加设备驱动程序、文件系统和其他功能。

## 内核模块的类型

有两种类型的内核模块：

1. **可加载内核模块**：这些是可以根据需要从内核加载和卸载的模块。
2. **静态编译内核模块**：这些是编译到内核本身的模块。

## 可加载内核模块的优点

与静态编译的内核模块相比，可加载内核模块有许多优点：

1. 它们可以根据需要从内核中加载和卸载，无需重启系统。
2. 它们可用于在内核中添加或删除功能，而无需重新编译内核。
3. 它们提供了一种无需重新编译内核或重启系统即可扩展内核功能的机制。

## 可加载内核模块的缺点

与静态编译的内核模块相比，可加载内核模块有许多缺点：

1. 如果设计和实施不当，它们可能会引入安全漏洞。
2. 它们可能难以调试和排除故障。
3. 它们可能难以维护和更新。

## 内核模块加载和卸载

可以使用 insmod 命令将内核模块加载到内核中，并使用 rmmod 命令从内核中卸载。

`insmod` 命令将内核模块的名称作为参数并将其加载到内核中。 `rmmod` 命令将内核模块的名称作为参数并将其从内核中删除。

## 创建内核模块

内核模块是一段目标代码，可以在运行时加载到内核中，而无需重新编译内核。内核模块通常用 C 编程语言编写。

内核模块必须使用“-DMODULE”编译器标志进行编译。这个标志告诉编译器代码被编译为内核模块。

内核模块也必须使用“-fPIC”编译器标志进行编译。该标志告诉编译器生成与位置无关的代码。与位置无关的代码可以加载到内存中的任何地址并执行。

可以使用 CFLAGS 环境变量将“-DMODULE”和“-fPIC”编译器标志传递给编译器。

```
$ export CFLAGS=-DMODULE -fPIC
```

一旦设置了 CFLAGS 环境变量，就可以使用 make 命令编译内核模块。

```
$ make
```

## 加载内核模块

可以使用 insmod 命令将内核模块加载到内核中。 `insmod` 命令将内核模块的名称作为参数并将其加载到内核中。

```
$ insmod hello.ko
```

## 卸载内核模块

可以使用 rmmod 命令从内核中卸载内核模块。 `rmmod` 命令将内核模块的名称作为参数并将其从内核中删除。

```
$ rmmod hello
```

## 参考

https://www.kernel.org/doc/Documentation/kmod/modules.txt
https://www.ibm.com/support/knowledgecenter/ssw_aix_71/com.ibm.aix.kernel/loadable_kernel_modules.htm
https://www.ibm.com/support/knowledgecenter/ssw_aix_71/com.ibm.aix.kernel/creating_kernel_modules.htm
https://www.ibm.com/support/knowledgecenter/ssw_aix_71/com.ibm.aix.kernel/loading_unloading_kernel_modules.htm