---
title: Java's Low-Pause Garbage Collectors: Understanding G1GC
description: 
published: true
date: 2023-02-13T07:17:32.974Z
tags: 
editor: markdown
dateCreated: 2023-02-13T07:17:25.032Z
---

- [Recolectores de basura de baja pausa de Java: comprensión de G1GC***Spanish** document is available*](/es/Knowledge-base/Java/java-s-low-pause-garbage-collectors-understanding-g1gc)
{.links-list}
- [Java 的低暂停垃圾收集器：了解 G1GC***Chinese Simplified** document is available*](/zh/Knowledge-base/Java/java-s-low-pause-garbage-collectors-understanding-g1gc)
{.links-list}
- [Java의 Low-Pause 가비지 수집기: G1GC 이해***Korean** document is available*](/ko/Knowledge-base/Java/java-s-low-pause-garbage-collectors-understanding-g1gc)
{.links-list}


# Java's Low-Pause Garbage Collectors: Understanding G1GC

Java's G1 garbage collector (GC) is a low-pause collector that attempts to minimize GC pause times. It does this by dividing the heap into a number of smaller regions and collecting them individually.

G1GC was first introduced in Java 7 and is the default GC in Java 8. It is considered to be the successor to the CMS GC.

## How G1GC Works

G1GC divides the heap into a number of regions. Each region is of a fixed size, and each region can contain either one or two objects.

When a region is full, it is considered "garbage" and is collected. The objects in the region are not moved; they are simply freed.

G1GC uses a number of techniques to minimize GC pause times, including:

-   **Parallelism:** G1GC can collect regions in parallel, using multiple threads.

-   **Concurrent Marking:** G1GC can mark objects while the application is running, instead of waiting until a GC cycle to do so.

-   **Incremental Collection:** G1GC can collect regions incrementally, collecting only a few regions at a time.

G1GC is a low-pause collector, but it is not a low-latency collector. G1GC pause times can still be significant, and applications that require low-latency GC may be better suited to another collector, such as the CMS GC.

## G1GC Performance

G1GC is designed to minimize GC pause times, but it is not always the fastest GC. In some cases, G1GC can be slower than other collectors.

G1GC is particularly well-suited to applications with large heaps and large numbers of objects. G1GC can also be a good choice for applications with high throughput requirements.

## When to Use G1GC

G1GC is a good choice for applications with large heaps and large numbers of objects. G1GC can also be a good choice for applications with high throughput requirements.

## When Not to Use G1GC

G1GC is not always the best choice for applications. In some cases, G1GC can be slower than other collectors.

G1GC is particularly well-suited to applications with large heaps and large numbers of objects. G1GC can also be a good choice for applications with high throughput requirements.

## Conclusion

G1GC is a low-pause garbage collector that is designed to minimize GC pause times. G1GC is a good choice for applications with large heaps and large numbers of objects. G1GC can also be a good choice for applications with high throughput requirements.