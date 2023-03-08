---
title: Linux System Startup and Initialization
description: 
published: true
date: 2023-02-11T04:55:18.048Z
tags: 
editor: markdown
dateCreated: 2023-02-11T04:55:11.376Z
---

- [Inicio e inicialización del sistema Linux***Spanish** document is available*](/es/Knowledge-base/Linux/linux-system-startup-and-initialization)
{.links-list}
- [Linux系统启动和初始化***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/linux-system-startup-and-initialization)
{.links-list}
- [Linux 시스템 시작 및 초기화***Korean** document is available*](/ko/Knowledge-base/Linux/linux-system-startup-and-initialization)
{.links-list}


# Linux System Startup and Initialization

Whenever a Linux system is booted, a number of processes are started to initialize the system. This process is known as system startup or initialization, and it typically happens in the following order:

1. ** BIOS **
2. ** Master boot record (MBR)**
3. ** Boot loader **
4. ** Kernel **
5. ** Init process **
6. ** User space **

## BIOS

The Basic Input/Output System (BIOS) is the first thing that runs when a computer is turned on. It is responsible for booting the computer by reading the boot sector of the hard drive, which contains the boot loader.

## Master boot record (MBR)

The MBR is a small piece of code that is responsible for loading the boot loader. It is typically located on the first sector of the hard drive.

## Boot loader

The boot loader is a program that is responsible for loading the operating system kernel. The most common boot loader used on Linux systems is GRUB (Grand Unified Bootloader).

## Kernel

The kernel is the core of the operating system and is responsible for managing the system's resources, such as memory, devices, and processes.

## Init process

The init process is the first process that is started by the kernel. It is responsible for starting all other processes on the system.

## User space

After the init process has started all other necessary processes, the system is said to be in user space. This is where normal users can login and run programs.