---
title: 읽기-쓰기 동시 잠금을 위한 Java의 ReentrantReadWriteLock
description: 
published: true
date: 2023-02-23T21:32:36.713Z
tags: 
editor: markdown
dateCreated: 2023-02-23T21:32:29.920Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Java's ReentrantReadWriteLock for Read-Write Concurrent Locking***English** document is available*](/en/Knowledge-base/Java/java-s-reentrantreadwritelock-for-read-write-concurrent-locking)
{.links-list}


# 읽기-쓰기 동시 잠금을 위한 Java의 ReentrantReadWriteLock

ReentrantReadWriteLock은 JDK 5.0 이상에서 Java 동시성 유틸리티의 일부로 제공되는 읽기-쓰기 잠금 구현입니다. 이 구현은 공정하게 설계되어 독자와 작성자 모두에게 동등한 액세스 기회를 제공합니다.

ReentrantReadWriteLock은 한 쌍의 잠금(읽기 전용 작업용 잠금과 쓰기용 잠금)을 유지합니다. 잠금을 획득하기 위해 대기 중인 쓰기 스레드가 없는 한 읽기 잠금은 여러 판독기 스레드에서 동시에 보유할 수 있습니다. 마찬가지로 쓰기 잠금은 단일 쓰기 스레드에만 적용되지만 다른 대기 스레드가 없는 경우 읽기 스레드에서 획득할 수 있습니다.

작가보다 독자가 우선입니다. 즉, 쓰기 잠금이 이미 설정된 상태에서 스레드가 읽기 잠금을 획득하려고 하면 쓰기 잠금이 해제되는 즉시 스레드에 잠금이 부여됩니다. 그러나 다른 스레드가 읽기 또는 쓰기 잠금을 보유하고 있는 동안 스레드가 쓰기 잠금을 획득하려고 하면 해당 스레드는 다른 모든 스레드가 잠금을 해제할 때까지 차단됩니다.

## 구현

ReentrantReadWriteLock은 ReentrantLock 주변의 래퍼로 구현되어 몇 가지 추가 기능과 함께 동일한 기본 기능을 제공합니다.

읽기 잠금을 획득하기 위해 스레드는 잠금이 사용 가능한 경우 잠금을 획득하는 lockRead()를 호출하고 그렇지 않은 경우 잠금이 해제될 때까지 기다립니다.

쓰기 잠금을 획득하기 위해 스레드는 잠금이 사용 가능한 경우 잠금을 획득하는 lockWrite()를 호출하고 그렇지 않은 경우 잠금이 해제될 때까지 기다립니다.

lockRead() 및 lockWrite()는 모두 비차단 메서드이므로 잠금이 사용 가능한 경우 즉시 반환됩니다.

읽기 잠금을 해제하려면 스레드가 unlockRead()를 호출하고 쓰기 잠금을 해제하려면 unlockWrite()를 호출합니다.

## 코드 예

다음은 ReentrantReadWriteLock을 사용하여 공유 리소스를 보호하는 방법에 대한 간단한 예입니다.

```java
import java.util.concurrent.locks.ReentrantReadWriteLock;

public class ReadWriteLockExample {

    private static final ReentrantReadWriteLock lock = new ReentrantReadWriteLock();

    public static void main(String[] args) {
        new Thread(ReadWriteLockExample::read).start();
        new Thread(ReadWriteLockExample::write).start();
    }

    private static void read() {
        lock.readLock().lock();
        try {
            // do something with the shared resource
        } finally {
            lock.readLock().unlock();
        }
    }

    private static void write() {
        lock.writeLock().lock();
        try {
            // do something with the shared resource
        } finally {
            lock.writeLock().unlock();
        }
    }
}
```

이 예제에는 읽기 스레드와 쓰기 스레드 모두에서 액세스할 수 있는 공유 리소스가 있습니다. 리소스를 보호하기 위해 ReentrantReadWriteLock을 사용합니다.

읽기 스레드는 lockRead()를 호출하여 읽기 잠금을 획득한 다음 unlockRead()를 호출하여 잠금을 해제합니다. 쓰기 스레드는 쓰기 잠금과 동일한 작업을 수행합니다.

## 이익

ReentrantReadWriteLock은 동기화된 키워드 및 ReentrantLock과 같은 다른 잠금 메커니즘에 비해 많은 이점을 제공합니다.

첫째, ReentrantReadWriteLock은 여러 판독기 스레드가 동시에 잠금을 획득하도록 허용하는 반면 동기화된 키워드 및 ReentrantLock은 한 번에 하나의 스레드만 잠금을 획득하도록 허용합니다. 이로 인해 많은 수의 읽기 작업을 수행하는 애플리케이션에서 처리량이 크게 증가할 수 있습니다.

둘째, ReentrantReadWriteLock은 작성기 스레드보다 판독기 스레드에 우선 순위를 부여하는 메커니즘을 제공합니다. 이는 쓰기 잠금이 이미 유지된 상태에서 잠금을 획득하려고 시도할 때 판독기 스레드에 우선 순위를 부여하여 수행됩니다.

셋째, ReentrantReadWriteLock은 쓰기 잠금을 획득한 다음 읽기 잠금을 위해 해제하는 프로세스인 잠금 다운그레이드를 허용합니다. 이는 스레드가 단일 쓰기 작업에 이어 일련의 읽기 작업을 수행해야 하는 상황에서 유용할 수 있습니다.

마지막으로 ReentrantReadWriteLock은 읽기 잠금을 획득한 다음 쓰기 잠금을 위해 해제하는 프로세스인 잠금 업그레이드를 위한 메커니즘을 제공합니다. 이는 스레드가 단일 쓰기 작업에 이어 일련의 읽기 작업을 수행해야 하는 상황에서 유용할 수 있습니다.

## ReentrantReadWriteLock을 사용해야 하는 경우

ReentrantReadWriteLock은 많은 수의 읽기 작업과 상대적으로 적은 수의 쓰기 작업을 수행하는 애플리케이션에서 가장 잘 사용됩니다. 이러한 응용 프로그램에서 ReentrantReadWriteLock은 다른 잠금 메커니즘에 비해 향상된 처리량을 제공합니다.

ReentrantReadWriteLock은 작성기 스레드보다 판독기 스레드에 우선 순위를 부여하는 것이 중요한 응용 프로그램에서도 좋은 선택입니다.

## ReentrantReadWriteLock을 사용하지 않는 경우

쓰기 작업 수가 읽기 작업 수에 비해 상대적으로 많은 애플리케이션에서는 ReentrantReadWriteLock을 사용하면 안 됩니다. 이러한 응용 프로그램에서 두 개의 잠금을 유지 관리하는 것과 관련된 증가된 오버헤드는 여러 판독기 스레드를 갖는 이점보다 중요합니다.

ReentrantReadWriteLock은 작성기 스레드보다 판독기 스레드에 우선 순위를 부여하는 것이 중요하지 않은 응용 프로그램에서도 좋은 선택이 아닙니다. 이러한 응용 프로그램에서 두 개의 잠금을 유지 관리하는 것과 관련된 증가된 오버헤드는 여러 판독기 스레드를 갖는 이점보다 중요합니다.

## ReentrantReadWriteLock의 대안

ReentrantReadWriteLock에는 여러 가지 대안이 있으며 각각 고유한 장점과 단점이 있습니다.

한 가지 대안은 동기화된 키워드입니다. Synchronized 키워드는 동시 액세스로부터 코드 블록을 보호하는 데 사용할 수 있는 언어 구조입니다. 동기화된 키워드는 ReentrantReadWriteLock보다 사용하기 쉽지만 여러 가지 단점이 있습니다.

첫째, 동기화된 키워드는 잠금 다운그레이드 또는 잠금 업그레이드를 허용하지 않습니다. 이로 인해 스레드가 일련의 읽기 작업을 수행한 후 단일 쓰기 작업을 수행해야 하는 상황에서 교착 상태가 발생할 수 있습니다.

둘째, 동기화된 키워드는 여러 판독기 스레드가 동시에 잠금을 획득하는 것을 허용하지 않습니다. 이로 인해 많은 수의 읽기 작업을 수행하는 애플리케이션에서 처리량이 감소할 수 있습니다.

또 다른 대안은 ReentrantLock입니다. ReentrantLock은 Java 동시성 유틸리티의 일부인 잠금 구현입니다. ReentrantLock은 동기화된 키워드보다 유연하지만 여러 가지 단점이 있습니다.

첫째, ReentrantLock은 잠금 다운그레이드 또는 잠금 업그레이드를 허용하지 않습니다. 이로 인해 스레드가 일련의 읽기 작업을 수행한 후 단일 쓰기 작업을 수행해야 하는 상황에서 교착 상태가 발생할 수 있습니다.

둘째, ReentrantLock은 여러 판독기 스레드가 동시에 잠금을 획득하는 것을 허용하지 않습니다. 이로 인해 많은 수의 읽기 작업을 수행하는 애플리케이션에서 처리량이 감소할 수 있습니다.

ReentrantReadWriteLock은 많은 수의 읽기 작업과 상대적으로 적은 수의 쓰기 작업을 수행하는 애플리케이션에 적합합니다. ReentrantReadWriteLock은 작성기 스레드보다 판독기 스레드에 우선 순위를 부여하는 것이 중요한 응용 프로그램에서도 좋은 선택입니다.