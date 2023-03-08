---
title: Java에서 사용자 정의 동시 데이터 구조 구축
description: 
published: true
date: 2023-03-02T20:32:14.582Z
tags: 
editor: markdown
dateCreated: 2023-03-02T20:32:13.199Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building Custom Concurrent Data Structures in Java***English** document is available*](/en/Knowledge-base/Java/building-custom-concurrent-data-structures-in-java)
{.links-list}


## 소개

다중 스레드 환경에서 동시 데이터 구조는 모든 스레드가 공유 데이터를 손상시키지 않고 액세스할 수 있도록 하는 데 중요한 역할을 합니다. Java는 기본적으로 사용할 수 있는 일련의 동시 데이터 구조를 제공하지만 특정 요구 사항에 맞는 사용자 지정 데이터 구조를 구축해야 하는 경우가 있습니다. 이 기사에서는 Java에서 사용자 정의 동시 데이터 구조를 빌드하는 방법을 배웁니다.

## 동시 데이터 구조란 무엇입니까?
  
동시 데이터 구조는 여러 스레드의 동시 액세스를 처리하도록 설계된 데이터 구조입니다. 공유 데이터에 대한 스레드 안전 액세스를 제공하고 데이터 일관성을 보장합니다. Java에서 가장 일반적으로 사용되는 동시 데이터 구조는 `ConcurrentHashMap`, `ConcurrentLinkedQueue` 및 `ConcurrentSkipListMap`입니다.

## 사용자 지정 동시 데이터 구조를 구축하는 이유는 무엇입니까?
  
Java는 일련의 동시 데이터 구조를 제공하지만 모든 사용 사례에 항상 가장 적합한 것은 아닙니다. 사용자 지정 동시 데이터 구조를 구축하면 동기화 오버헤드를 최소화하고 보다 맞춤화된 기능을 제공하여 성능을 최적화할 수 있습니다.

## Java에서 사용자 지정 동시 데이터 구조 구축
  
Java에서 사용자 지정 동시 데이터 구조를 구축하려면 다음 개념을 이해해야 합니다.

### 스레드로부터 안전한 작업
  
스레드로부터 안전한 작업은 데이터 손상 위험 없이 여러 스레드에서 안전하게 액세스할 수 있는 작업입니다. Java에서는 `synchronized` 블록을 사용하거나 `ReentrantLock`과 같은 동시 잠금을 사용하여 스레드 안전성을 보장할 수 있습니다.

### 원자적 작업
  
원자적 작업은 다른 스레드에 의해 중단되지 않도록 단일 단계에서 실행되는 작업입니다. Java에서는 `java.util.concurrent.atomic` 패키지에서 제공하는 `Atomic` 클래스를 사용하여 원자적 작업을 수행할 수 있습니다.

### 잠금 해제 데이터 구조
  
잠금 없는 데이터 구조는 잠금 없이 작동하도록 설계된 데이터 구조이며 대신 원자적 작업 및 비차단 알고리즘에 의존합니다. 잠금이 없는 데이터 구조는 동기화 오버헤드를 최소화하고 성능을 향상시키는 데 도움이 될 수 있습니다.

### 사용자 지정 동시 데이터 구조 예
  
정수 집합을 저장하고 다음 작업을 제공하는 사용자 지정 동시 데이터 구조를 빌드하는 간단한 예를 살펴보겠습니다.
  
- `add(int x)` - 집합에 정수 x를 더합니다.
- `remove(int x)` - 집합에서 정수 x를 제거합니다(있는 경우).
- `contains(int x)` - 집합에 정수 x가 있으면 true를 반환하고 그렇지 않으면 false를 반환합니다.

데이터 구조를 구축하기 위해 각 `AtomicBoolean`은 세트의 정수에 해당하는 `AtomicBoolean` 개체의 배열을 사용합니다. 해당 정수가 있으면 `AtomicBoolean`은 `true`로 설정되고 그렇지 않으면 `false`로 설정됩니다.

다음은 사용자 지정 동시 데이터 구조의 구현입니다.

```java
import java.util.concurrent.atomic.AtomicBoolean;

public class CustomConcurrentSet {
    private final AtomicBoolean[] set;

    public CustomConcurrentSet(int capacity) {
        set = new AtomicBoolean[capacity];
        for (int i = 0; i < capacity; i++) {
            set[i] = new AtomicBoolean(false);
        }
    }

    public void add(int x) {
        set[x].set(true);
    }

    public boolean remove(int x) {
        return set[x].compareAndSet(true, false);
    }

    public boolean contains(int x) {
        return set[x].get();
    }
}
```

`CustomConcurrentSet` 클래스에서 지정된 용량으로 `AtomicBoolean` 개체의 배열을 초기화합니다. `add` 메서드에서 정수에 해당하는 `AtomicBoolean`을 `true`로 설정합니다. `remove` 메소드에서 `compareAndSet` 메소드를 사용하여 `AtomicBoolean`이 현재 `true`로 설정되어 있는 경우 `false`로 설정합니다. `contains` 메소드에서 단순히 `AtomicBoolean`의 부울 값을 반환합니다.

## 결론

스레드 안전 작업, 원자적 작업 및 잠금 없는 데이터 구조의 개념을 이해하면 Java에서 사용자 지정 동시 데이터 구조를 구축하는 데 도움이 될 수 있습니다. 맞춤형 데이터 구조를 구축하면 성능을 최적화하고 특정 요구 사항에 맞게 기능을 조정할 수 있습니다. Java는 기본적으로 사용할 수 있는 일련의 동시 데이터 구조를 제공하지만 때로는 필요에 맞게 사용자 지정 데이터 구조를 구축해야 합니다.

## 외부 리소스

- [자바 동시성 실습](https://www.amazon.com/Java-Concurrency-Practice-Brian-Goetz/dp/0321349601)
- [자바의 동시 데이터 구조](https://www.baeldung.com/java-concurrent-data-structures)
- [잠금 없는 데이터 구조](https://en.wikipedia.org/wiki/Lock-free_and_wait-free_algorithms)