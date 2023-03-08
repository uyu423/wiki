---
title: Understanding Java's Concurrent Mark Sweep Garbage Collector
description: 
published: true
date: 2023-01-31T22:43:39.549Z
tags: 
editor: markdown
dateCreated: 2023-01-31T22:43:35.862Z
---

- [Java의 동시 마크 스윕 가비지 수집기 이해***Korean** version of this document is available*](/ko/Knowledge-base/Java/understanding-java-s-concurrent-mark-sweep-garbage-collector)
{.links-list}
- [Java のコンカレント マーク スイープ ガベージ コレクタを理解する***Japanese** version of this document is available*](/ja/Knowledge-base/Java/understanding-java-s-concurrent-mark-sweep-garbage-collector)
{.links-list}
- [了解 Java 的并发标记清除垃圾收集器***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Java/understanding-java-s-concurrent-mark-sweep-garbage-collector)
{.links-list}



# Understanding Java's Concurrent Mark Sweep Garbage Collector

Java's Concurrent Mark Sweep (CMS) garbage collector is designed for applications that prefer short garbage collection (GC) pauses and can tolerate some application performance degradation when the collector is running. The CMS collector is concurrent, meaning that it runs concurrently with the application. This allows the CMS collector to avoid most application pauses.

The CMS collector uses a mark-sweep algorithm. It first marks all live objects in the heap. It then sweeps through the heap, freeing any dead objects it finds. Finally, it compacts the heap to reduce fragmentation.

The CMS collector has two main modes of operation: concurrent mode and stop-the-world mode.

Concurrent mode is the default mode of operation. In concurrent mode, the CMS collector runs concurrently with the application. It does most of its work while the application is running. This means that the CMS collector can avoid most application pauses.

Stop-the-world mode is a fallback mode of operation. In stop-the-world mode, the CMS collector pauses the application while it does its work. This mode is used when the CMS collector cannot finish its work in concurrent mode.

The CMS collector is designed for applications that can tolerate some application performance degradation while the collector is running. The CMS collector is not suitable for applications that require guaranteed low latency.

## How the CMS Collector Works

The CMS collector uses a mark-sweep algorithm. It first marks all live objects in the heap. It then sweeps through the heap, freeing any dead objects it finds. Finally, it compact the heap to reduce fragmentation.

The CMS collector has two main modes of operation: concurrent mode and stop-the-world mode.

Concurrent mode is the default mode of operation. In concurrent mode, the CMS collector runs concurrently with the application. It does most of its work while the application is running. This means that the CMS collector can avoid most application pauses.

Stop-the-world mode is a fallback mode of operation. In stop-the-world mode, the CMS collector pauses the application while it does its work. This mode is used when the CMS collector cannot finish its work in concurrent mode.

The CMS collector is designed for applications that can tolerate some application performance degradation while the collector is running. The CMS collector is not suitable for applications that require guaranteed low latency.

## Concurrent Mode

In concurrent mode, the CMS collector runs concurrently with the application. It does most of its work while the application is running. This means that the CMS collector can avoid most application pauses.

The CMS collector uses a mark-sweep algorithm. It first marks all live objects in the heap. It then sweeps through the heap, freeing any dead objects it finds. Finally, it compact the heap to reduce fragmentation.

## Stop-the-World Mode

In stop-the-world mode, the CMS collector pauses the application while it does its work. This mode is used when the CMS collector cannot finish its work in concurrent mode.

The CMS collector uses a mark-sweep algorithm. It first marks all live objects in the heap. It then sweeps through the heap, freeing any dead objects it finds. Finally, it compact the heap to reduce fragmentation.

## When to Use the CMS Collector

The CMS collector is designed for applications that can tolerate some application performance degradation while the collector is running. The CMS collector is not suitable for applications that require guaranteed low latency.

## Conclusion

The CMS collector is a concurrent, mark-sweep garbage collector. It is designed for applications that can tolerate some application performance degradation while the collector is running. The CMS collector is not suitable for applications that require guaranteed low latency.