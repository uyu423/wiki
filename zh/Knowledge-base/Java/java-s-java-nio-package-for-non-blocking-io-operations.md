---
title: Java 的非阻塞 I/O 操作的 java.nio 包
description: 
published: true
date: 2023-02-15T11:17:45.116Z
tags: 
editor: markdown
dateCreated: 2023-02-15T11:17:43.485Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Java's java.nio Package for Non-Blocking I/O Operations***English** document is available*](/en/Knowledge-base/Java/java-s-java-nio-package-for-non-blocking-io-operations)
{.links-list}



# Java 的非阻塞 I/O 操作的 java.nio 包

Java 的“java.nio”包提供了用于在 Java 中执行*非阻塞*输入/输出 (I/O) 操作的 API。非阻塞 I/O 意味着线程可以发起 I/O 操作，而不必等待操作完成。这可以导致更高效的 I/O 操作，因为线程可以在执行 I/O 操作的同时执行其他工作。

## java.nio 概述

java.nio 包是在 Java 1.4 中引入的，它提供了以下内容：

- 一组用于以各种原始类型存储数据的“Buffer”类
- 一组用于执行 I/O 操作的“Channel”类
- 一组用于多路复用 I/O 操作的“选择器”类
- 一组用于执行基于文件的 I/O 操作的 `FileLock` 和 `FileChannel` 类

此外，java.nio.file 包是在 Java 7 中引入的，它提供了对基于文件的 I/O 操作的支持。

## 缓冲

`Buffer` 是特定原始类型数据的容器。每种原始数据类型都有“Buffer”类：“ByteBuffer”、“CharBuffer”、“DoubleBuffer”、“FloatBuffer”、“IntBuffer”、“LongBuffer”和“ShortBuffer”。

`Buffer` 具有以下属性：

- **Capacity：**缓冲区中可以存储的最大元素数。
- **限制：**不应读取或写入的第一个元素的索引。
- **Position:** 要读取或写入的下一个元素的索引。

`Buffer` 也有以下方法：

- `clear()`：将位置设置为 0，并将限制设置为容量。
- `flip()`：将限制设置为当前位置并将位置设置为 0。
- `rewind()`：将位置设置为 0。
- `remaining()`：返回位置和限制之间的元素数。
- `hasRemaining()`：如果还有剩余元素，则返回 `true`，否则返回 `false`。

## 渠道

`Channel` 是一种类似于 `Buffer` 的结构，表示与 I/O 设备的开放连接。 `Channel` 可以打开用于读取、写入或两者。

`Channel` 有多种类型，包括`FileChannel`、`DatagramChannel`、`SocketChannel` 和`Pipe.SinkChannel`。

`Channel` 有以下方法：

- `isOpen()`：如果通道打开则返回 `true`，否则返回 `false`。
- `close()`: 关闭通道。
- `read(Buffer)`：将数据从通道读入给定的缓冲区。
- `write(Buffer)`：将给定缓冲区中的数据写入通道。

## 选择器

`Selector` 用于多路复用 I/O 操作。 `Selector` 可用于等待 I/O 操作在一个或多个 `Channel` 上完成。

`Selector` 有以下方法：

- `open()`：打开一个 `Selector`。
- `close()`：关闭`Selector`。
- `select()`：返回准备执行 I/O 操作的 `Channel` 的 `SelectionKey`。
- `select(long)`：返回准备执行 I/O 操作的 `Channel` 的 `SelectionKey`，如果超时到期则返回 `null`。
- `selectedKeys()`：返回准备执行 I/O 操作的 `Channel` 的 `SelectionKey` 的 `Set`。
- `keys()`：返回所有使用此 `Selector` 注册的 `Channel` 的 `SelectionKey` 的 `Set`。

## 文件锁

`FileLock` 用于锁定 `FileChannel` 的区域。 `FileLock` 具有以下方法：

- `isShared()`：如果锁是共享的，则返回 true，否则返回 false。
- `release()`：释放锁。
- `isValid()`：如果锁仍然有效，则返回 `true`，否则返回 `false`。

## 文件通道

`FileChannel` 是用于执行基于文件的 I/O 操作的 `Channel`。 `FileChannel` 具有以下方法：

- `lock(long, long, boolean)`: 锁定文件的一个区域。
- `tryLock()`：尝试锁定文件的一个区域。
- `read(ByteBuffer, long)`：将文件中的数据读入给定的缓冲区。
- `write(ByteBuffer, long)`：将给定缓冲区中的数据写入文件。

## java.nio.文件

`java.nio.file` 包是在 Java 7 中引入的，它提供了对基于文件的 I/O 操作的支持。这个包包含以下类：

- `Path`：文件系统路径的表示。
- `Paths`：用于创建 `Path` 对象的工厂。
- `Files`：用于执行文件相关操作的实用程序类。

## 结论

Java 的 java.nio 包提供了用于在 Java 中执行非阻塞 I/O 操作的 API。 `java.nio.file` 包是在 Java 7 中引入的，它提供了对基于文件的 I/O 操作的支持。