---
title: Linux I/O Scheduling and Disk Management
description: 
published: true
date: 2023-02-11T17:32:39.183Z
tags: 
editor: markdown
dateCreated: 2023-02-11T17:32:32.648Z
---

- [Programación de E/S de Linux y administración de discos***Spanish** document is available*](/es/Knowledge-base/Linux/linux-io-scheduling-and-disk-management)
{.links-list}
- [Linux I/O 调度和磁盘管理***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/linux-io-scheduling-and-disk-management)
{.links-list}
- [Linux I/O 스케줄링 및 디스크 관리***Korean** document is available*](/ko/Knowledge-base/Linux/linux-io-scheduling-and-disk-management)
{.links-list}


# Linux I/O Scheduling and Disk Management

The Linux kernel's I/O scheduler is responsible for optimizing the order in which block I/O requests from the kernel's block layer are submitted to storage devices. This process, known as I/O scheduling, can have a significant impact on system performance.

There are three primary goals of I/O scheduling:

- Improve performance by reordering requests to minimize seeks
- Improve performance by merging requests
- Reduce latency by giving priority to requests from processes with lower I/O priority

The I/O scheduler in the Linux kernel is designed to balance these three goals.

## I/O Scheduling Algorithms

There are three I/O scheduling algorithms available in the Linux kernel:

- Deadline I/O scheduler
- Noop I/O scheduler
- CFQ I/O scheduler

The Deadline I/O scheduler is the default I/O scheduler in the Linux kernel. It is designed to minimize latency by giving priority to requests from processes with lower I/O priority.

The Noop I/O scheduler is a very simple I/O scheduler that does not reorder requests. It is typically used for devices with very low I/O latency, such as solid-state drives.

The CFQ I/O scheduler is the default I/O scheduler on most Linux distributions. It is designed to balance the three goals of I/O scheduling: minimizing seek time, merging requests, and reducing latency.

## Changing the I/O Scheduler

The I/O scheduler can be changed on a per-device basis using the `-s` option of the `blockdev` command. For example, to change the I/O scheduler of `/dev/sda` to the Deadline I/O scheduler, you would use the following command:

```
blockdev -s /dev/sda deadline
```

The I/O scheduler can also be changed on a per-filesystem basis. To change the I/O scheduler of the `/` filesystem to the CFQ I/O scheduler, you would use the following command:

```
mount -o remount,ioscheduler=cfq /
```

## I/O Scheduling and Disk Management

The I/O scheduler can have a significant impact on disk performance. For example, the Deadline I/O scheduler is designed to minimize latency by giving priority to requests from processes with lower I/O priority. This can result in increased performance for processes with high I/O priority, such as database servers.

The CFQ I/O scheduler is designed to balance the three goals of I/O scheduling: minimizing seek time, merging requests, and reducing latency. This can result in increased performance for most workloads.

## Conclusion

The I/O scheduler in the Linux kernel is responsible for optimizing the order in which block I/O requests from the kernel's block layer are submitted to storage devices. There are three primary goals of I/O scheduling: improve performance by reordering requests to minimize seeks, improve performance by merging requests, and reduce latency by giving priority to requests from processes with lower I/O priority.

The I/O scheduler can have a significant impact on disk performance. The Deadline I/O scheduler is designed to minimize latency by giving priority to requests from processes with lower I/O priority. The CFQ I/O scheduler is designed to balance the three goals of I/O scheduling: minimizing seek time, merging requests, and reducing latency.

## Resources

- [Linux I/O Scheduling](https://www.kernel.org/doc/Documentation/block/ioprio.txt)
- [I/O scheduler](https://en.wikipedia.org/wiki/I/O_scheduler)
- [Noop I/O scheduler](https://www.kernel.org/doc/Documentation/block/noop-iosched.txt)
- [CFQ I/O scheduler](https://www.kernel.org/doc/Documentation/block/cfq-iosched.txt)
- [Deadline I/O scheduler](https://www.kernel.org/doc/Documentation/block/deadline-iosched.txt)