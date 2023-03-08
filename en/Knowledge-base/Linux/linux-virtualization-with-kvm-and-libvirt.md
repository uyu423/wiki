---
title: Linux Virtualization with KVM and libvirt
description: 
published: true
date: 2023-02-12T04:32:43.159Z
tags: 
editor: markdown
dateCreated: 2023-02-12T04:32:36.476Z
---

- [Virtualización de Linux con KVM y libvirt***Spanish** document is available*](/es/Knowledge-base/Linux/linux-virtualization-with-kvm-and-libvirt)
{.links-list}
- [使用 KVM 和 libvirt 的 Linux 虚拟化***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/linux-virtualization-with-kvm-and-libvirt)
{.links-list}
- [KVM 및 libvirt를 사용한 Linux 가상화***Korean** document is available*](/ko/Knowledge-base/Linux/linux-virtualization-with-kvm-and-libvirt)
{.links-list}


# Linux Virtualization with KVM and libvirt

## Introduction

Virtualization is the process of creating a virtual version of something, such as an operating system, a server, a storage device, or network resources. It is a powerful technology that has many uses, including consolidating multiple servers onto a single physical server, creating test and development environments, and more.

Linux has long been a leader in virtualization with many different virtualization technologies available. In this article, we will focus on two of the most popular: KVM and libvirt.

## What is KVM?

KVM (Kernel-based Virtual Machine) is a full virtualization solution for Linux that is included in the mainline Linux kernel since version 2.6.20. In order to use KVM, your CPU must have hardware virtualization extensions, such as Intel VT-x or AMD-V.

KVM is a hypervisor that runs on top of a Linux kernel and provides virtualization capabilities using hardware virtualization extensions. KVM is included in the mainline Linux kernel and is used by many Linux distributions as their default virtualization solution.

## What is libvirt?

libvirt is a toolkit that provides a unified API for managing virtualization platforms, such as KVM, Xen, and others. It is used by many virtualization management tools, such as virt-manager, and is also available as a command-line tool.

libvirt provides a powerful and easy-to-use API for managing virtual machines and other virtualization resources, such as storage and networking. It is available as a command-line tool and as a library that can be used by other programs.

## Getting Started with KVM and libvirt

In order to use KVM and libvirt, you need a Linux system with hardware virtualization extensions and a recent version of the Linux kernel. KVM is included in the mainline Linux kernel, so you should have no trouble getting it if you are using a recent version of your distribution's kernel.

Once you have a Linux system with hardware virtualization extensions and a recent kernel, you can install KVM and libvirt with your distribution's package manager. For example, on Debian and Ubuntu systems, you can install them with the following command:

```
sudo apt-get install kvm libvirt-bin
```

Once KVM and libvirt are installed, you can use the virt-manager tool to manage your virtual machines. virt-manager is a graphical tool that makes it easy to create and manage virtual machines.

## Creating a Virtual Machine

 virt-manager is a graphical tool for managing virtual machines. To launch it, type the following command:

```
virt-manager
```

You will see the virt-manager window shown in Figure 1.


Figure 1. The virt-manager Window

To create a new virtual machine, click the File menu and select New Virtual Machine. You will see the New VM Wizard window shown in Figure 2.


Figure 2. The New VM Wizard Window

On the first page of the wizard, select the Local install media option and click Forward. On the next page, select the ISO image option and click Forward. On the next page, select the Browse button and browse to the location of your ISO image. Then, select the Forward button.

On the next page, you will see a list of available operating systems. Select the operating system you want to install and click Forward. On the next page, enter a name for your virtual machine and click Forward.

On the next page, you will see a list of available storage devices. Select the storage device you want to use and click Forward. On the next page, you will see a list of available network devices. Select the network device you want to use and click Forward.

On the next page, you will see a list of available CPU models. Select the CPU model you want to use and click Forward. On the next page, you will see a list of available memory sizes. Select the memory size you want to use and click Forward.

On the next page, you will see a list of available video devices. Select the video device you want to use and click Forward. On the final page, review your selections and click Finish.

The virt-manager tool will now create your virtual machine and boot it from the ISO image you selected. The virtual machine will be in a paused state, so you will need to click the Resume button to start it.

## Connecting to a Virtual Machine

Once your virtual machine is running, you can connect to it using the virt-manager tool. To do this, select your virtual machine in the virt-manager window and click the Connect button. You will see the Connect to VM window shown in Figure 3.


Figure 3. The Connect to VM Window

On the first page of the wizard, select the VNC option and click Forward. On the next page, you will see a list of available VNC viewers. Select the viewer you want to use and click Forward. On the final page, review your selections and click Finish.

The virt-manager tool will now launch your VNC viewer and connect to your virtual machine. You will see the login screen for your virtual machine.

## Managing Virtual Machines with virsh

In addition to the virt-manager tool, you can also use the virsh tool to manage your virtual machines. virsh is a command-line tool that provides a powerful set of commands for managing virtual machines.

To list all of the available virsh commands, type the following command:

```
virsh
```

To get help for a specific virsh command, type the following command:

```
virsh help {command}
```

To list all of the available virtual machines, type the following command:

```
virsh list
```

To get information about a specific virtual machine, type the following command:

```
virsh dominfo {domain}
```

To start a virtual machine, type the following command:

```
virsh start {domain}
```

To shutdown a virtual machine, type the following command:

```
virsh shutdown {domain}
```

To destroy a virtual machine, type the following command:

```
virsh destroy {domain}
```

To suspend a virtual machine, type the following command:

```
virsh suspend {domain}
```

To resume a virtual machine, type the following command:

```
virsh resume {domain}
```

To connect to a virtual machine, type the following command:

```
virsh console {domain}
```

## Managing Storage with virt-manager

In addition to managing virtual machines, the virt-manager tool can also be used to manage storage. To launch the storage manager, type the following command:

```
virt-manager --storage
```

You will see the virt-manager Storage window shown in Figure 4.


Figure 4. The virt-manager Storage Window

To create a new storage pool, click the File menu and select New Storage Pool. You will see the New Storage Pool window shown in Figure 5.


Figure 5. The New Storage Pool Window

On the first page of the wizard, select the type of storage pool you want to create and click Forward. On the next page, select the source of the storage pool and click Forward. On the next page, select the target of the storage pool and click Forward.

On the next page, you will see a list of available storage devices. Select the storage devices you want to use and click Forward. On the next page, you will see a list of available storage formats. Select the storage format you want to use and click Forward.

On the next page, you will see a list of available allocation strategies. Select the allocation strategy you want to use and click Forward. On the next page, you will see a list of available cache modes. Select the cache mode you want to use and click Forward.

On the next page, you will see a list of available I/O schedulers. Select the I/O scheduler you want to use and click Forward. On the next page, you will see a list of available block sizes. Select the block size you want to use and click Forward.

On the final page, review your selections and click Finish. The virt-manager tool will now create your storage pool.

## Conclusion

In this article, we have covered the basics of Linux virtualization with KVM and libvirt. We have seen how to install KVM and libvirt, how to create and manage virtual machines, and how to manage storage.

With this knowledge, you should be able to start using KVM and libvirt to virtualize your own Linux environment.