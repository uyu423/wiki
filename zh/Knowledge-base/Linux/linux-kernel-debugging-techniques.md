---
title: Linux 内核调试技巧
description: 
published: true
date: 2023-02-11T21:32:59.164Z
tags: 
editor: markdown
dateCreated: 2023-02-11T21:32:52.676Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Linux Kernel Debugging Techniques***English** document is available*](/en/Knowledge-base/Linux/linux-kernel-debugging-techniques)
{.links-list}


# Linux 内核调试技巧

Linux 内核是一个包含许多活动部件的复杂软件。因此，当出现问题时很难调试。本文将探索一些用于调试 Linux 内核的最有用的技术。

## 打印内核消息

调试内核的最基本和最有用的技术之一是将消息打印到内核日志中。内核日志是存储在文件“/var/log/kern.log”中的所有内核活动的记录。可以使用 `printk` 函数将消息打印到内核日志中。

`printk` 函数采用格式字符串和可变数量的参数。格式字符串类似于用户空间中的 `printf` 函数，但有一些重要的区别。首先，`printk` 格式字符串可以包含`%p`、`%t` 和`%i` 的格式说明符，分别是当前任务的地址、jiffies 中的当前时间和当前CPU ID .其次，`printk` 格式字符串可以包含 `%ln` 说明符，以字节为单位指示后续参数的大小。最后，`printk` 格式字符串可以包含 `%s` 说明符，它打印以下参数的字符串表示形式。

这是 `printk` 用法的一个简单示例：

```c
#include <linux/kernel.h>

void print_message(void)
{
    printk("This is a test message.\n");
}
```

## 使用内核调试器

内核调试器或“kdb”是调试内核的强大工具。 `kdb` 可用于检查和更改内核数据结构、设置断点和单步执行内核代码。通过将 `kdb` 命令行选项添加到内核引导参数来调用 `kdb`。使用此选项启动内核时，发生内核崩溃时将自动输入 `kdb`。

也可以通过按 Ctrl-Alt-SysRq-K 组合键手动输入 `kdb`。输入 `kdb` 后，将显示 `kdb>` 提示符。可以在此提示符下输入 `kdb` 命令。在 `kdb>` 提示符下键入 `help` 以查看可用命令列表。

最有用的 `kdb` 命令之一是 `bt`。此命令打印当前调用堆栈的回溯。这有助于了解发生内核恐慌的位置和原因。

另一个有用的 `kdb` 命令是 `md`。此命令可用于检查内存的内容。例如，命令 `md 0xffffffff80000000 0x200` 将打印内核内存前 512 字节的内容。

## 使用内核探测器

内核探测或“kprobe”是一项 Linux 内核功能，允许在调用特定内核函数时执行用户空间代码。 `kprobe` 可用于检测内核以进行调试。

使用 `kprobe` 命令行选项调用 `kprobe`。 `kprobe` 选项采用内核函数名称和用户空间处理函数。每次调用内核函数时都会执行处理函数。处理函数可以访问内核函数的参数和返回值。

以下是 `kprobe` 用法的一个简单示例：

```c
#include <linux/kprobes.h>

static int handler_kprobe(struct kprobe *p, void *data)
{
    printk("kprobe hit!\n");
    return 0;
}

static struct kprobe kp = {
    .symbol_name    = "do_fork",
    .handler        = handler_kprobe,
};

static int __init kprobe_init(void)
{
    register_kprobe(&kp);
    return 0;
}

static void __exit kprobe_exit(void)
{
    unregister_kprobe(&kp);
}

module_init(kprobe_init)
module_exit(kprobe_exit)
```

在此示例中，为 do_fork 内核函数注册了一个 `kprobe`。每次调用 do_fork 时，都会执行 handler_kprobe 函数。 `handler_kprobe` 函数只是将一条消息打印到内核日志中。

## 使用内核跟踪

内核跟踪或“ktrace”是一种 Linux 内核功能，可以跟踪内核活动。 `ktrace` 可用于检测内核以进行调试。

`ktrace` 是使用 `ktrace` 命令行选项调用的。 `ktrace` 选项采用跟踪缓冲区大小和跟踪文件名。跟踪缓冲区用于存储跟踪事件。跟踪文件用于存储跟踪事件的人类可读表示。

以下是 `ktrace` 用法的简单示例：

```c
#include <linux/ktrace.h>

static int __init ktrace_init(void)
{
    ktrace("/tmp/ktrace.out", 1024);
    return 0;
}

static void __exit ktrace_exit(void)
{
    ktrace_stop();
}

module_init(ktrace_init)
module_exit(ktrace_exit)
```

在此示例中，“ktrace”被配置为跟踪内核活动到文件“/tmp/ktrace.out”。跟踪缓冲区设置为 1024 KB。

## 使用内核分析器

内核分析器或“kprof”是一种 Linux 内核功能，可以分析内核代码。 `kprof` 可用于收集有关内核的性能信息。

使用 `kprof` 命令行选项调用 `kprof`。 `kprof` 选项采用分析间隔和跟踪文件名。分析间隔是样本之间的时间，以纳秒为单位。跟踪文件用于存储分析信息。

以下是 `kprof` 用法的简单示例：

```c
#include <linux/kprof.h>

static int __init kprof_init(void)
{
    kprof("/tmp/kprof.out", 10000000);
    return 0;
}

static void __exit kprof_exit(void)
{
    kprof_stop();
}

module_init(kprof_init)
module_exit(kprof_exit)
```

在此示例中，`kprof` 配置为每 10 毫秒分析一次内核代码。分析信息存储在文件“/tmp/kprof.out”中。

## 结论

本文探索了一些用于调试 Linux 内核的最有用的技术。这些技术可用于调试内核崩溃、性能问题和其他问题。