---
title: Virtualization with Hypervisor and VMs
description: 
published: true
date: 2023-02-08T14:17:38.748Z
tags: 
editor: markdown
dateCreated: 2023-02-08T14:17:32.874Z
---

- [Virtualización con Hypervisor y VMs***Spanish** document is available*](/es/Knowledge-base/Backend/virtualization-with-hypervisor-and-vms)
{.links-list}
- [使用 Hypervisor 和 VM 进行虚拟化***Chinese Simplified** document is available*](/zh/Knowledge-base/Backend/virtualization-with-hypervisor-and-vms)
{.links-list}
- [Hypervisor 및 VM을 통한 가상화***Korean** document is available*](/ko/Knowledge-base/Backend/virtualization-with-hypervisor-and-vms)
{.links-list}


# Virtualization with Hypervisor and VMs

With the ever-growing demand for computing power, along with the trend of miniaturization in the hardware industry, it's no wonder that virtualization has become such a popular topic in recent years. Virtualization allows for the creation of virtual machines (VMs) that can run on a physical machine, sharing the underlying hardware resources.

There are two main types of virtualization:

1. **Full virtualization** - The guest operating system is given full access to the underlying hardware resources. This allows for unmodified guest operating systems to be run on the host.

2. **Paravirtualization** - The guest operating system is not given full access to the underlying hardware resources. Instead, it's given a modified version of the hardware that's optimized for running in a virtual environment.

There are also two main types of virtualization platforms:

1. **Bare metal** - The hypervisor is installed directly on the physical machine. This provides the best performance but requires dedicated hardware.

2. **Hosted** - The hypervisor is installed on top of a host operating system. This is less resource-intensive but can result in decreased performance.

## Setting up a Virtual Machine

There are a few things you'll need in order to set up a virtual machine:

1. A physical machine with enough resources to support the virtual machine.

2. A hypervisor. This can be either bare metal or hosted.

3. A guest operating system. This can be either full virtualization or paravirtualization.

4. Virtual machine software. This will allow you to create and manage your virtual machines.

Once you have all of these things, you can start setting up your virtual machine. The first thing you'll need to do is create a virtual disk. This will be used to store the guest operating system and any data you want to keep on the VM.

Once you have a virtual disk, you can install the guest operating system on it. If you're using full virtualization, you can just install the OS like you would on a physical machine. If you're using paravirtualization, you'll need to use a modified version of the OS that's optimized for virtual environments.

Once the OS is installed, you can start configuring the VM. This will include things like setting up networking, installing applications, and so on.

## Running a Virtual Machine

Once you have a virtual machine set up, you can start using it. To do this, you'll need to boot the VM. This can be done either from the hypervisor or from the guest OS.

If you're booting from the hypervisor, you'll need to select the VM you want to boot and then select the "boot" option. This will boot the VM and bring you to the guest OS.

If you're booting from the guest OS, you'll need to select the "boot" option from within the OS. This will boot the VM and bring you to the guest OS.

Once the VM is booted, you can use it just like you would any other computer. You can install applications, browse the web, and so on.

## Shutting Down a Virtual Machine

When you're done using a virtual machine, you'll need to shut it down. This can be done either from the hypervisor or from the guest OS.

If you're shutting down from the hypervisor, you'll need to select the VM you want to shut down and then select the "shut down" option. This will shut down the VM and bring you back to the hypervisor.

If you're shutting down from the guest OS, you'll need to select the "shut down" option from within the OS. This will shut down the VM and bring you back to the hypervisor.

Once the VM is shut down, you can either power off the machine or leave it running. If you power off the machine, the VM will be turned off and will not be able to be used until you power the machine back on. If you leave the machine running, the VM will be turned off but will remain available for use.

## Conclusion

Virtualization is a great way to increase the computing power of a physical machine. It allows for the creation of virtual machines that can share the underlying hardware resources. There are two main types of virtualization: full virtualization and paravirtualization. There are also two main types of virtualization platforms: bare metal and hosted.

To set up a virtual machine, you'll need a physical machine with enough resources to support the VM, a hypervisor, a guest operating system, and virtual machine software. Once you have all of these things, you can start setting up your VM.

Once your VM is set up, you can start using it. To do this, you'll need to boot the VM. This can be done either from the hypervisor or from the guest OS. Once the VM is booted, you can use it just like you would any other computer.

When you're done using a virtual machine, you'll need to shut it down. This can be done either from the hypervisor or from the guest OS. Once the VM is shut down, you can either power off the machine or leave it running.