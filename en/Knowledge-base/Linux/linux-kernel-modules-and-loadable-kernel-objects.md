---
title: Linux Kernel Modules and Loadable Kernel Objects
description: 
published: true
date: 2023-02-11T16:32:25.508Z
tags: 
editor: markdown
dateCreated: 2023-02-11T16:32:18.727Z
---

- [Módulos del kernel de Linux y objetos del kernel cargables***Spanish** document is available*](/es/Knowledge-base/Linux/linux-kernel-modules-and-loadable-kernel-objects)
{.links-list}
- [Linux 内核模块和可加载内核对象***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/linux-kernel-modules-and-loadable-kernel-objects)
{.links-list}
- [Linux 커널 모듈 및 로드 가능한 커널 개체***Korean** document is available*](/ko/Knowledge-base/Linux/linux-kernel-modules-and-loadable-kernel-objects)
{.links-list}


# Linux Kernel Modules and Loadable Kernel Objects

## Overview

A Linux kernel module is a piece of object code that can be loaded into the kernel at run-time, without recompiling the kernel. 

Loadable kernel modules provide a mechanism for extending the functionality of the kernel without the need to recompile the kernel or reboot the system. 

 Kernel modules can be used to add device drivers, file systems, and other functionality to the kernel.

## Types of Kernel Modules

There are two types of kernel modules:

1. **Loadable kernel modules**: These are modules that can be loaded and unloaded from the kernel as needed. 
2. **Statically compiled kernel modules**: These are modules that are compiled into the kernel itself.

## Advantages of Loadable Kernel Modules

Loadable kernel modules have a number of advantages over statically compiled kernel modules:

1. They can be loaded and unloaded from the kernel as needed, without the need to reboot the system.
2. They can be used to add or remove functionality from the kernel without the need to recompile the kernel.
3. They provide a mechanism for extending the functionality of the kernel without the need to recompile the kernel or reboot the system.

## Disadvantages of Loadable Kernel Modules

Loadable kernel modules have a number of disadvantages over statically compiled kernel modules:

1. They can introduce security vulnerabilities if they are not properly designed and implemented.
2. They can be difficult to debug and troubleshoot.
3. They can be difficult to maintain and update.

## Kernel Module Loading and Unloading

A kernel module can be loaded into the kernel using the `insmod` command and unloaded from the kernel using the `rmmod` command. 

The `insmod` command takes the name of the kernel module as an argument and loads it into the kernel. The `rmmod` command takes the name of the kernel module as an argument and removes it from the kernel. 

## Creating a Kernel Module

A kernel module is a piece of object code that can be loaded into the kernel at run-time, without recompiling the kernel. Kernel modules are typically written in the C programming language. 

Kernel modules must be compiled with the `-DMODULE` compiler flag. This flag tells the compiler that the code is being compiled as a kernel module. 

Kernel modules must also be compiled with the `-fPIC` compiler flag. This flag tells the compiler to generate position-independent code. Position-independent code can be loaded into memory at any address and executed. 

The `-DMODULE` and `-fPIC` compiler flags can be passed to the compiler using the `CFLAGS` environment variable. 

```
$ export CFLAGS=-DMODULE -fPIC
```

Once the `CFLAGS` environment variable has been set, the kernel module can be compiled using the `make` command. 

```
$ make
```

## Loading a Kernel Module

A kernel module can be loaded into the kernel using the `insmod` command. The `insmod` command takes the name of the kernel module as an argument and loads it into the kernel. 

```
$ insmod hello.ko
```

## Unloading a Kernel Module

A kernel module can be unloaded from the kernel using the `rmmod` command. The `rmmod` command takes the name of the kernel module as an argument and removes it from the kernel. 

```
$ rmmod hello
```

## References

https://www.kernel.org/doc/Documentation/kmod/modules.txt
https://www.ibm.com/support/knowledgecenter/ssw_aix_71/com.ibm.aix.kernel/loadable_kernel_modules.htm
https://www.ibm.com/support/knowledgecenter/ssw_aix_71/com.ibm.aix.kernel/creating_kernel_modules.htm
https://www.ibm.com/support/knowledgecenter/ssw_aix_71/com.ibm.aix.kernel/loading_unloading_kernel_modules.htm