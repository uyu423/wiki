---
title: Hypervisor
description: 
published: true
date: 2023-02-17T18:15:49.286Z
tags: 
editor: markdown
dateCreated: 2023-01-30T23:57:41.068Z
---

- [Hypervisor***Korean** version of this document is available*](/ko/Knowledge-base/Dictionary/hypervisor)
{.links-list}
- [Hypervisor***Japanese** version of this document is available*](/ja/Knowledge-base/Dictionary/hypervisor)
{.links-list}
- [Hypervisor***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Dictionary/hypervisor)
{.links-list}


# Overview
A **hypervisor** is a software-based virtualization technology that creates and runs virtual machines (VMs) on a physical server. It allows multiple operating systems and applications to run on the same hardware, enabling the creation of virtualized computing environments. 

# History
The concept of virtualization was introduced in the 1960s and 1970s, with the development of **time-sharing** systems. These systems allowed multiple users to access the same computing resources, enabling the efficient use of resources. The first commercial hypervisor, IBM’s DIS/VMS, was released in 1978. 

# Description
A hypervisor is a layer of software that sits between the physical hardware and the operating system. It allows multiple guest operating systems to run on the same physical server, enabling the creation of virtualized computing environments. The hypervisor creates a **virtual machine** (VM) on the physical server. Each VM has its own operating system, applications, and data, allowing it to be managed independently from other VMs on the same server. 

The hypervisor manages the resources of the physical server, such as CPU, memory, and storage, and allocates them to the VMs. It also provides the **virtualization layer**, which allows the guest operating systems to be isolated from each other and access the physical hardware directly.

The most common type of hypervisor is the **hosted hypervisor**, which runs on top of an existing operating system. Examples include VMware ESXi and Microsoft Hyper-V. The other type is the **bare-metal hypervisor**, which runs directly on the physical hardware. Examples include VMware ESX and Microsoft Hyper-V Server.

# Related Links
- [What is a Hypervisor?*VMware*](https://www.vmware.com/resources/compatibility/what-is-a-hypervisor.html)
- [Hypervisor*Microsoft*](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/hypervisor-overview)
- [Hypervisor Types: A Comprehensive Guide*Ravello Systems*](https://ravellosystems.com/hypervisor-types-guide/)
{.links-list}