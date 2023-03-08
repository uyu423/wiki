---
title: Java 的低暂停垃圾收集器：了解 G1GC
description: 
published: true
date: 2023-02-13T07:17:26.610Z
tags: 
editor: markdown
dateCreated: 2023-02-13T07:17:25.023Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Java's Low-Pause Garbage Collectors: Understanding G1GC***English** document is available*](/en/Knowledge-base/Java/java-s-low-pause-garbage-collectors-understanding-g1gc)
{.links-list}


# Java 的低暂停垃圾收集器：了解 G1GC

Java 的 G1 垃圾收集器 (GC) 是一种低暂停收集器，它试图最大限度地减少 GC 暂停时间。它通过将堆分成许多较小的区域并单独收集它们来实现这一点。

G1GC 最早在 Java 7 中引入，是 Java 8 中的默认 GC，被认为是 CMS GC 的继承者。

## G1GC 是如何工作的

G1GC 将堆划分为多个区域。每个区域的大小都是固定的，每个区域可以包含一个或两个对象。

当一个区域已满时，它被认为是“垃圾”并被收集。区域内的物体没有移动；他们只是被释放了。

G1GC 使用多种技术来最小化 GC 暂停时间，包括：

- **并行性：** G1GC 可以使用多线程并行收集区域。

- **并发标记：** G1GC 可以在应用程序运行时标记对象，而不是等到 GC 周期才这样做。

- **增量收集：** G1GC 可以增量收集区域，一次只收集几个区域。

G1GC 是一个低暂停收集器，但它不是一个低延迟收集器。 G1GC 暂停时间仍然很长，需要低延迟 GC 的应用程序可能更适合其他收集器，例如 CMS GC。

## G1GC 性能

G1GC 旨在最大限度地减少 GC 暂停时间，但它并不总是最快的 GC。在某些情况下，G1GC 可能比其他收集器慢。

G1GC 特别适合具有大堆和大量对象的应用程序。对于具有高吞吐量要求的应用程序，G1GC 也是一个不错的选择。

## 何时使用 G1GC

G1GC 是具有大堆和大量对象的应用程序的不错选择。对于具有高吞吐量要求的应用程序，G1GC 也是一个不错的选择。

## 何时不使用 G1GC

G1GC 并不总是应用程序的最佳选择。在某些情况下，G1GC 可能比其他收集器慢。

G1GC 特别适合具有大堆和大量对象的应用程序。对于具有高吞吐量要求的应用程序，G1GC 也是一个不错的选择。

## 结论

G1GC 是一种低暂停垃圾收集器，旨在最大限度地减少 GC 暂停时间。 G1GC 是具有大堆和大量对象的应用程序的不错选择。对于具有高吞吐量要求的应用程序，G1GC 也是一个不错的选择。