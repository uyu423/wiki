---
title: Java의 Low-Pause 가비지 수집기: G1GC 이해
description: 
published: true
date: 2023-02-13T07:17:26.570Z
tags: 
editor: markdown
dateCreated: 2023-02-13T07:17:25.023Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Java's Low-Pause Garbage Collectors: Understanding G1GC***English** document is available*](/en/Knowledge-base/Java/java-s-low-pause-garbage-collectors-understanding-g1gc)
{.links-list}


# Java의 Low-Pause 가비지 컬렉터: G1GC 이해

Java의 G1 가비지 수집기(GC)는 GC 일시 중지 시간을 최소화하려고 시도하는 낮은 일시 중지 수집기입니다. 힙을 여러 개의 작은 영역으로 나누고 개별적으로 수집하여 이를 수행합니다.

G1GC는 Java 7에서 처음 도입되었으며 Java 8의 기본 GC입니다. CMS GC의 후속 제품으로 간주됩니다.

## G1GC 작동 방식

G1GC는 힙을 여러 영역으로 나눕니다. 각 영역은 크기가 고정되어 있으며 각 영역에는 하나 또는 두 개의 개체가 포함될 수 있습니다.

영역이 가득 차면 "쓰레기"로 간주되어 수집됩니다. 영역의 개체는 이동되지 않습니다. 그들은 단순히 해방됩니다.

G1GC는 GC 일시 중지 시간을 최소화하기 위해 다음과 같은 다양한 기술을 사용합니다.

- **병렬성:** G1GC는 여러 스레드를 사용하여 병렬로 영역을 수집할 수 있습니다.

- **동시 마킹:** G1GC는 GC 주기까지 기다리지 않고 애플리케이션이 실행되는 동안 객체를 마킹할 수 있습니다.

- **Incremental Collection:** G1GC는 한 번에 몇 개의 region만 수집하여 점진적으로 region을 수집할 수 있습니다.

G1GC는 low-pause 컬렉터이지만, low-latency 컬렉터는 아닙니다. G1GC 일시 중지 시간은 여전히 중요할 수 있으며 대기 시간이 짧은 GC가 필요한 애플리케이션은 CMS GC와 같은 다른 수집기에 더 적합할 수 있습니다.

## G1GC 성능

G1GC는 GC 중지 시간을 최소화하도록 설계되었지만 항상 가장 빠른 GC는 아닙니다. 어떤 경우에는 G1GC가 다른 수집기보다 느릴 수 있습니다.

G1GC는 힙이 크고 개체 수가 많은 애플리케이션에 특히 적합합니다. G1GC는 높은 처리량 요구 사항이 있는 애플리케이션에도 좋은 선택이 될 수 있습니다.

## G1GC를 사용하는 경우

G1GC는 힙이 크고 개체 수가 많은 애플리케이션에 적합합니다. G1GC는 높은 처리량 요구 사항이 있는 애플리케이션에도 좋은 선택이 될 수 있습니다.

## G1GC를 사용하지 말아야 할 때

G1GC가 애플리케이션에 항상 최선의 선택은 아닙니다. 어떤 경우에는 G1GC가 다른 수집기보다 느릴 수 있습니다.

G1GC는 힙이 크고 개체 수가 많은 애플리케이션에 특히 적합합니다. G1GC는 높은 처리량 요구 사항이 있는 애플리케이션에도 좋은 선택이 될 수 있습니다.

## 결론

G1GC는 GC 일시 중지 시간을 최소화하도록 설계된 낮은 일시 중지 가비지 수집기입니다. G1GC는 힙이 크고 개체 수가 많은 애플리케이션에 적합합니다. G1GC는 높은 처리량 요구 사항이 있는 애플리케이션에도 좋은 선택이 될 수 있습니다.