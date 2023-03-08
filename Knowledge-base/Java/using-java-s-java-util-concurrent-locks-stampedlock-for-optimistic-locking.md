---
title: 낙관적 잠금을 위해 Java의 java.util.concurrent.locks.StampedLock 사용
description: 
published: true
date: 2023-02-01T07:17:42.202Z
tags: 
editor: markdown
dateCreated: 2023-02-01T07:17:40.594Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Using Java's java.util.concurrent.locks.StampedLock for Optimistic Locking***English** version of this document is available*](/en/Knowledge-base/Java/using-java-s-java-util-concurrent-locks-stampedlock-for-optimistic-locking)
{.links-list}



# 낙관적 잠금을 위해 Java의 java.util.concurrent.locks.StampedLock 사용

낙관적 잠금은 데이터가 둘 이상의 스레드에 의해 동시에 수정되지 않도록 하는 전략입니다. 잠금의 오버헤드를 피하면서 데이터 손상에 대한 보호를 제공하기 위해 동시 프로그래밍에서 널리 사용되는 기술입니다.

Java의 java.util.concurrent.locks.StampedLock은 낙관적 잠금을 위한 메커니즘을 제공합니다. 이 기사에서는 Java에서 낙관적 잠금을 달성하기 위해 StampedLock 클래스를 사용하는 방법을 살펴봅니다.

## 낙관적 잠금이란 무엇입니까?

낙관적 잠금은 데이터가 둘 이상의 스레드에 의해 동시에 수정되지 않도록 하는 전략입니다. 잠금의 오버헤드를 피하면서 데이터 손상에 대한 보호를 제공하기 위해 동시 프로그래밍에서 널리 사용되는 기술입니다.

낙관적 잠금을 사용할 때 각 스레드는 먼저 데이터를 읽습니다. 데이터가 다른 스레드에 의해 수정되지 않은 경우 스레드는 데이터를 안전하게 업데이트할 수 있습니다. 데이터가 다른 스레드에 의해 수정된 경우 업데이트가 중단되고 데이터가 다시 로드됩니다.

## StampedLock은 어떻게 작동하나요?

StampedLock은 세 가지 잠금 모드(낙관적, 읽기 및 쓰기)가 있는 재진입 잠금입니다.

낙관적 모드는 기본 모드입니다. 낙관적 모드에서 스레드는 차단하지 않고 잠금을 잠글 수 있습니다. 잠금이 다른 스레드에 의해 이미 잠긴 경우 잠금 시도가 실패합니다.

읽기 모드에서는 여러 스레드가 읽기를 위해 잠금을 잠글 수 있습니다. 쓰기를 위해 잠금이 이미 잠겨 있으면 잠금 시도가 실패합니다.

쓰기 모드에서는 하나의 스레드만 쓰기를 위해 잠금을 잠글 수 있습니다. 읽기 또는 쓰기를 위해 잠금이 이미 잠겨 있으면 잠금 시도가 실패합니다.

## StampedLock 사용

다음은 동시 수정으로부터 데이터를 보호하기 위해 StampedLock을 사용하는 간단한 예입니다.

```java
import java.util.concurrent.locks.StampedLock;

public class OptimisticLocking {

    private static final StampedLock lock = new StampedLock();
    private static int data = 0;

    public static void main(String[] args) {
        // thread 1 tries to read data
        long stamp = lock.tryOptimisticRead();
        int localData = data;
        if (!lock.validate(stamp)) {
            // data has been modified, need to acquire read lock
            stamp = lock.readLock();
            try {
                localData = data;
            } finally {
                lock.unlockRead(stamp);
            }
        }
        // data has not been modified, can use localData safely

        // thread 2 tries to update data
        long stamp = lock.writeLock();
        try {
            data = localData + 1;
        } finally {
            lock.unlockWrite(stamp);
        }
    }
}
```

위의 예에서 스레드 1은 데이터 읽기를 시도합니다. 데이터가 다른 스레드에 의해 수정되지 않은 경우 읽기가 성공하고 스레드 1이 데이터를 안전하게 사용할 수 있습니다. 데이터가 다른 스레드에 의해 수정된 경우 읽기가 실패하고 스레드 1이 데이터를 읽으려면 읽기 잠금을 획득해야 합니다.

스레드 2는 데이터 업데이트를 시도합니다. 데이터가 다른 스레드에 의해 수정되지 않은 경우 업데이트가 성공합니다. 데이터가 다른 스레드에 의해 수정된 경우 업데이트가 실패하고 스레드 2는 데이터를 업데이트하기 위해 쓰기 잠금을 획득해야 합니다.

## StampedLock을 사용하는 경우

StampedLock은 Java에서 낙관적 잠금을 달성하는 데 유용한 도구입니다. 낙관적 잠금을 사용할 때 성능과 정확성 사이의 균형을 고려하는 것이 중요합니다.

낙관적 잠금은 잠금 오버헤드를 피함으로써 성능을 향상시킬 수 있습니다. 그러나 데이터 손상 위험이 높아집니다. 데이터가 동시 스레드에 의해 자주 수정되는 경우 낙관적 잠금이 최선의 전략이 아닐 수 있습니다.

## 결론

이 기사에서는 낙관적 잠금을 달성하기 위해 Java의 java.util.concurrent.locks.StampedLock을 사용하는 방법을 살펴보았습니다. 우리는 낙관적 잠금을 사용할 때 고려해야 할 장단점도 살펴보았습니다.