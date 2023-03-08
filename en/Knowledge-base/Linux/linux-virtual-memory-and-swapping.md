---
title: Linux Virtual Memory and Swapping
description: 
published: true
date: 2023-02-11T15:32:56.909Z
tags: 
editor: markdown
dateCreated: 2023-02-11T15:32:54.640Z
---

- [Memoria virtual e intercambio de Linux***Spanish** document is available*](/es/Knowledge-base/Linux/linux-virtual-memory-and-swapping)
{.links-list}
- [Linux 虚拟内存和交换***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/linux-virtual-memory-and-swapping)
{.links-list}
- [Linux 가상 메모리 및 스와핑***Korean** document is available*](/ko/Knowledge-base/Linux/linux-virtual-memory-and-swapping)
{.links-list}


# Linux Virtual Memory and Swapping

Virtual memory is a technique that allows a system to use more memory than is physically available in the form of RAM by using the hard drive as temporary storage. This allows for more programs to be run at the same time and can improve performance.

Swapping is the process of moving data from RAM to the hard drive and back again as needed. When a system is low on RAM, the kernel will start swapping data to the hard drive to free up memory. This can cause the system to slow down as the hard drive is much slower than RAM.

## What is virtual memory?

Virtual memory is a technique that allows a system to use more memory than is physically available in the form of RAM by using the hard drive as temporary storage. This allows for more programs to be run at the same time and can improve performance.

When a program is started, the operating system allocates a certain amount of memory for it to use. This memory is used for the program's code and data. If the program tries to use more memory than has been allocated, an error will occur.

Virtual memory allows the operating system to allocate more memory to a program than is physically available. When the program tries to access this additional memory, the operating system will transparently copy the necessary data from the hard drive into RAM. This process is known as swapping.

Swapping is the process of moving data from RAM to the hard drive and back again as needed. When a system is low on RAM, the kernel will start swapping data to the hard drive to free up memory. This can cause the system to slow down as the hard drive is much slower than RAM.

Linux uses a technique called demand paging for virtual memory. This means that data is only copied from the hard drive to RAM when it is needed. This is in contrast to techniques like pre-paging where data is copied from the hard drive to RAM even if it is not needed.

Demand paging is more efficient as it only copies the data that is actually needed. However, it can cause the system to slow down if a lot of data is needed and is not already in RAM.

## Advantages of virtual memory

Virtual memory has several advantages over physical memory:

* More programs can be run at the same time as each program uses less memory.

* The operating system can use disk space more efficiently as it does not need to allocate a contiguous block of memory for each program.

* The operating system can avoid copying data to and from the hard drive as often as it would if the data was not in virtual memory.

* Virtual memory allows the operating system to protect the address space of each program from other programs. This is known as memory address protection.

## Disadvantages of virtual memory

Virtual memory also has some disadvantages:

* The system will slow down as data is copied to and from the hard drive.

* The hard drive is a lot slower than RAM so the system will not be able to run as quickly as if all the data was in RAM.

* The hard drive can fill up quickly if the system is using a lot of virtual memory.

## Setting up virtual memory

Linux uses a program called `swap` to manage virtual memory. The `swap` program is responsible for allocating space on the hard drive for virtual memory and for copying data to and from the hard drive as needed.

The `swap` program is configured using the `/etc/fstab` file. This file contains a list of all the partitions on the hard drive and other information about them. The `swap` program will look for a line in this file that starts with `/swap` and use the partition listed there for virtual memory.

Here is an example `/etc/fstab` file:

    /dev/sda1 /boot ext4 defaults 0 2
    /dev/sda2 / ext4 defaults 0 1
    /dev/sda3 swap swap defaults 0 0

In this example, the `/dev/sda3` partition is being used for virtual memory.

The `/etc/fstab` file can also be used to configure other options for the `swap` program. For example, the `swappiness` option can be used to control how often the `swap` program will copy data to and from the hard drive.

The `swappiness` option is a number between 0 and 100 that controls how often the `swap` program will copy data to and from the hard drive. A value of 0 means that the `swap` program will only copy data to the hard drive when the system is low on memory. A value of 100 means that the `swap` program will copy data to the hard drive even if the system is not low on memory.

The default value for `swappiness` is 60. This means that the `swap` program will start copying data to the hard drive when the system has 60% of its RAM free.

##Conclusion

Virtual memory is a technique that allows a system to use more memory than is physically available in the form of RAM by using the hard drive as temporary storage. This allows for more programs to be run at the same time and can improve performance.

Swapping is the process of moving data from RAM to the hard drive and back again as needed. When a system is low on RAM, the kernel will start swapping data to the hard drive to free up memory. This can cause the system to slow down as the hard drive is much slower than RAM.

 Linux uses a technique called demand paging for virtual memory. This means that data is only copied from the hard drive to RAM when it is needed. This is in contrast to techniques like pre-paging where data is copied from the hard drive to RAM even if it is not needed.

Demand paging is more efficient as it only copies the data that is actually needed. However, it can cause the system to slow down if a lot of data is needed and is not already in RAM.

The `swap` program is responsible for allocating space on the hard drive for virtual memory and for copying data to and from the hard drive as needed. The `swap` program is configured using the `/etc/fstab` file. This file contains a list of all the partitions on the hard drive and other information about them. The `swap` program will look for a line in this file that starts with `/swap` and use the partition listed there for virtual memory.

The `swappiness` option is a number between 0 and 100 that controls how often the `swap` program will copy data to and from the hard drive. A value of 0 means that the `swap` program will only copy data to the hard drive when the system is low on memory. A value of 100 means that the `swap` program will copy data to the hard drive even if the system is not low on memory.

## References

* [https://www.geeksforgeeks.org/virtual-memory-in-operating-system/](https://www.geeksforgeeks.org/virtual-memory-in-operating-system/)

* [https://www.geeksforgeeks.org/paging-in-operating-systems/](https://www.geeksforgeeks.org/paging-in-operating-systems/)

* [https://www.redhat.com/sysadmin/linux-swap-space](https://www.redhat.com/sysadmin/linux-swap-space)

* [https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-18-04](https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-18-04)