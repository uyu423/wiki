---
title: 使用 KVM 和 libvirt 的 Linux 虚拟化
description: 
published: true
date: 2023-02-12T04:32:38.369Z
tags: 
editor: markdown
dateCreated: 2023-02-12T04:32:36.472Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Linux Virtualization with KVM and libvirt***English** document is available*](/en/Knowledge-base/Linux/linux-virtualization-with-kvm-and-libvirt)
{.links-list}


# 使用 KVM 和 libvirt 的 Linux 虚拟化

## 介绍

虚拟化是创建某物（例如操作系统、服务器、存储设备或网络资源）的虚拟版本的过程。它是一项功能强大的技术，用途广泛，包括将多台服务器整合到一台物理服务器上、创建测试和开发环境等。

Linux 长期以来一直是虚拟化领域的领导者，提供了许多不同的虚拟化技术。在本文中，我们将重点关注两个最流行的：KVM 和 libvirt。

## 什么是 KVM？

KVM（基于内核的虚拟机）是 Linux 的完整虚拟化解决方案，自版本 2.6.20 起包含在主线 Linux 内核中。为了使用 KVM，您的 CPU 必须具有硬件虚拟化扩展，例如 Intel VT-x 或 AMD-V。

KVM 是运行在 Linux 内核之上的管理程序，并使用硬件虚拟化扩展提供虚拟化功能。 KVM 包含在主线 Linux 内核中，并被许多 Linux 发行版用作默认虚拟化解决方案。

## 什么是 libvirt？

libvirt 是一个工具包，它提供统一的 API 来管理虚拟化平台，例如 KVM、Xen 等。它被许多虚拟化管理工具使用，例如 virt-manager，也可用作命令行工具。

libvirt 提供了一个功能强大且易于使用的 API，用于管理虚拟机和其他虚拟化资源，例如存储和网络。它可以作为命令行工具使用，也可以作为可供其他程序使用的库使用。

## KVM 和 libvirt 入门

为了使用 KVM 和 libvirt，您需要一个带有硬件虚拟化扩展的 Linux 系统和最新版本的 Linux 内核。 KVM 包含在主线 Linux 内核中，因此如果您使用的是发行版内核的最新版本，获取它应该没有问题。

一旦您拥有一个带有硬件虚拟化扩展和最新内核的 Linux 系统，您就可以使用您的发行版的包管理器安装 KVM 和 libvirt。例如，在 Debian 和 Ubuntu 系统上，您可以使用以下命令安装它们：

```
sudo apt-get install kvm libvirt-bin
```

安装 KVM 和 libvirt 后，您可以使用 virt-manager 工具来管理您的虚拟机。 virt-manager 是一个图形工具，可以轻松创建和管理虚拟机。

## 创建虚拟机

 virt-manager 是一个用于管理虚拟机的图形工具。要启动它，请键入以下命令：

```
virt-manager
```

您将看到图 1 中所示的 virt-manager 窗口。


图 1. virt-manager 窗口

要创建新的虚拟机，请单击“文件”菜单并选择“新建虚拟机”。您将看到如图 2 所示的新建 VM 向导窗口。


图 2. 新建 VM 向导窗口

在向导的第一页，选择本地安装媒体选项并单击转发。在下一页上，选择 ISO 映像选项并单击转发。在下一页上，选择浏览按钮并浏览到您的 ISO 映像的位置。然后，选择转发按钮。

在下一页上，您将看到可用操作系统的列表。选择您要安装的操作系统，然后单击“前进”。在下一页上，为您的虚拟机输入一个名称，然后单击转发。

在下一页上，您将看到可用存储设备的列表。选择您要使用的存储设备，然后单击转发。在下一页上，您将看到可用网络设备的列表。选择您要使用的网络设备，然后单击转发。

在下一页上，您将看到可用 CPU 型号的列表。选择您要使用的 CPU 型号，然后单击 Forward。在下一页上，您将看到可用内存大小的列表。选择您要使用的内存大小，然后单击 Forward。

在下一页上，您将看到可用视频设备的列表。选择您要使用的视频设备，然后单击转发。在最后一页上，检查您的选择并单击完成。

virt-manager 工具现在将创建您的虚拟机并从您选择的 ISO 映像启动它。虚拟机将处于暂停状态，因此您需要单击“恢复”按钮来启动它。

## 连接到虚拟机

虚拟机运行后，您可以使用 virt-manager 工具连接到它。为此，请在 virt-manager 窗口中选择您的虚拟机，然后单击“连接”按钮。您将看到图 3 中所示的“连接到 VM”窗口。


图 3. 连接到 VM 窗口

在向导的第一页，选择 VNC 选项并单击 Forward。在下一页上，您将看到可用 VNC 查看器的列表。选择您要使用的查看器，然后单击前进。在最后一页上，检查您的选择并单击完成。

virt-manager 工具现在将启动您的 VNC 查看器并连接到您的虚拟机。您将看到虚拟机的登录屏幕。

## 使用 virsh 管理虚拟机

除了 virt-manager 工具，您还可以使用 virsh 工具来管理您的虚拟机。 virsh 是一个命令行工具，它提供了一组强大的命令来管理虚拟机。

要列出所有可用的 virsh 命令，请键入以下命令：

```
virsh
```

要获取特定 virsh 命令的帮助，请键入以下命令：

```
virsh help {command}
```

要列出所有可用的虚拟机，请键入以下命令：

```
virsh list
```

要获取有关特定虚拟机的信息，请键入以下命令：

```
virsh dominfo {domain}
```

要启动虚拟机，请键入以下命令：

```
virsh start {domain}
```

要关闭虚拟机，请键入以下命令：

```
virsh shutdown {domain}
```

要销毁虚拟机，请键入以下命令：

```
virsh destroy {domain}
```

要挂起虚拟机，请键入以下命令：

```
virsh suspend {domain}
```

要恢复虚拟机，请键入以下命令：

```
virsh resume {domain}
```

要连接到虚拟机，请键入以下命令：

```
virsh console {domain}
```

## 使用 virt-manager 管理存储

除了管理虚拟机，virt-manager 工具还可以用来管理存储。要启动存储管理器，请键入以下命令：

```
virt-manager --storage
```

您将看到如图 4 所示的 virt-manager Storage 窗口。


图 4. virt-manager 存储窗口

要创建新的存储池，请单击“文件”菜单并选择“新建存储池”。您将看到如图 5 所示的 New Storage Pool 窗口。


图 5. 新存储池窗口

在向导的第一页，选择您要创建的存储池类型并单击 Forward。在下一页上，选择存储池的来源并单击转发。在下一页中，选择存储池的目标并单击转发。

在下一页上，您将看到可用存储设备的列表。选择您要使用的存储设备，然后单击转发。在下一页上，您将看到可用存储格式的列表。选择您要使用的存储格式，然后单击转发。

在下一页上，您将看到可用分配策略的列表。选择您要使用的分配策略并单击转发。在下一页上，您将看到可用缓存模式的列表。选择您要使用的缓存模式，然后单击转发。

在下一页上，您将看到可用 I/O 调度程序的列表。选择要使用的 I/O 调度程序并单击转发。在下一页上，您将看到可用块大小的列表。选择您要使用的块大小，然后单击转发。

在最后一页上，检查您的选择并单击完成。 virt-manager 工具现在将创建您的存储池。

## 结论

在本文中，我们介绍了使用 KVM 和 libvirt 进行 Linux 虚拟化的基础知识。我们已经了解了如何安装 KVM 和 libvirt，如何创建和管理虚拟机，以及如何管理存储。

有了这些知识，您应该能够开始使用 KVM 和 libvirt 来虚拟化您自己的 Linux 环境。