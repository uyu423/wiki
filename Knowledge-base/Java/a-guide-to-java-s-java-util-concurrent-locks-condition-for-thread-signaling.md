---
title: 스레드 시그널링을 위한 Java의 java.util.concurrent.locks.Condition 가이드
description: 
published: true
date: 2023-02-04T02:55:25.532Z
tags: 
editor: markdown
dateCreated: 2023-02-04T02:55:20.080Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [A Guide to Java's java.util.concurrent.locks.Condition for Thread Signaling***English** document is available*](/en/Knowledge-base/Java/a-guide-to-java-s-java-util-concurrent-locks-condition-for-thread-signaling)
{.links-list}



# 스레드 시그널링을 위한 Java의 java.util.concurrent.locks.Condition 가이드

스레드는 종종 서로 통신해야 합니다. 예를 들어 한 스레드는 작업이 완료되었거나 공유 리소스를 사용할 수 있음을 다른 스레드에 알려야 할 수 있습니다.

Java에는 `java.util.concurrent.locks.Condition` 클래스라고 하는 스레드 통신을 위한 기본 제공 메커니즘이 있습니다. 이 기사에서는 `Condition`을 사용하여 스레드 간에 통신하는 방법을 살펴보겠습니다.

## 컨디션이란?

조건은 스레드가 다른 스레드를 기다리거나 신호를 보낼 수 있도록 하는 Java 클래스입니다. 또한 `Lock` 클래스를 포함하는 `java.util.concurrent.locks` 패키지의 일부입니다.

Condition은 Lock과 함께 작동하여 스레드가 실행될 수 있는 시기를 보다 유연하게 제어할 수 있는 방법을 제공합니다. Lock을 사용하면 스레드는 잠금을 보유하고 있을 때만 실행할 수 있습니다. Condition을 사용하면 스레드는 다른 스레드가 신호를 보낸 경우에만 실행할 수 있습니다.

## 사용 조건

Condition은 Lock과 함께 작동하여 스레드가 실행될 수 있는 시기를 보다 유연하게 제어할 수 있는 방법을 제공합니다. Lock을 사용하면 스레드는 잠금을 보유하고 있을 때만 실행할 수 있습니다. Condition을 사용하면 스레드는 다른 스레드가 신호를 보낸 경우에만 실행할 수 있습니다.

다음은 조건을 사용하는 방법에 대한 간단한 예입니다. 비어 있음 또는 가득 참의 두 가지 상태 중 하나일 수 있는 공유 리소스가 있다고 가정합니다. 리소스를 생성하는 스레드와 리소스를 소비하는 스레드의 두 가지 스레드가 있습니다.

우리는 소비자 스레드가 "가득" 상태일 때만 리소스를 소비하려고 시도하고 생산자 스레드가 "비어 있음" 상태일 때만 리소스를 생성하려고 시도하는지 확인하려고 합니다. 이를 위해 잠금 및 조건을 사용할 수 있습니다.


```java
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class Resource {
    private final Lock lock = new ReentrantLock();
    private final Condition isEmpty = lock.newCondition();
    private final Condition isFull = lock.newCondition();

    private boolean empty = true;

    public void produce() throws InterruptedException {
        lock.lock();
        try {
            while (!empty) {
                isEmpty.await();
            }
            // produce resource
            empty = false;
            isFull.signalAll();
        } finally {
            lock.unlock();
        }
    }

    public void consume() throws InterruptedException {
        lock.lock();
        try {
            while (empty) {
                isFull.await();
            }
            // consume resource
            empty = true;
            isEmpty.signalAll();
        } finally {
            lock.unlock();
        }
    }
}
```

이 예제에서 `produce()` 메서드는 먼저 리소스가 비어 있는지 확인합니다. 그렇지 않은 경우 비어 있을 때까지 기다립니다(`isEmpty.await()` 호출). 리소스가 비면 리소스를 생성하고 대기 중인 스레드에 신호를 보냅니다(`isFull.signalAll()` 호출).

마찬가지로 `consume()` 메서드는 먼저 리소스가 가득 찼는지 확인합니다. 그렇지 않은 경우 가득 찰 때까지 기다립니다(`isFull.await()` 호출). 리소스가 가득 차면 리소스를 소비하고 대기 중인 스레드에 신호를 보냅니다(`isEmpty.signalAll()` 호출).

## 기타 방법

조건은 또한 조건을 기다리고 있는 단일 스레드를 깨우는 `signal()` 메서드를 제공합니다. 여러 스레드가 대기 중인 경우 그중 하나가 무작위로 선택되어 깨어납니다.

또한 `awaitUninterruptibly()` 메서드도 있는데, 스레드가 중단되더라도 InterruptedException을 발생시키지 않는다는 점을 제외하고는 `await()`와 유사합니다.

## 조건 사용 팁

다음은 조건 사용에 대한 몇 가지 팁입니다.

- 항상 루프 내에서 `await()` 또는 `signal()`을 호출합니다. 이는 `await()`가 인터럽트(`interrupt()`에 대한 호출에 의해)될 수 있고 `signal()`이 손실될 수 있기 때문입니다(여러 스레드가 대기 중인 경우 스레드 중 하나만 깨어날 것임).

- 잠금 외부에서 `await()` 또는 `signal()`을 호출하지 않도록 주의하십시오. 그렇게 하면 조건을 확인하는 시간과 `await()` 또는 `signal()`을 호출하는 시간 사이에 다른 스레드가 잠금을 획득할 수 있습니다. 이로 인해 프로그램이 멈출 수 있습니다.

- 여러 조건을 사용할 때 모두 같은 잠금을 사용하지 않도록 주의하세요. 이로 인해 교착 상태가 발생할 수 있습니다.

## 결론

이 기사에서는 스레드 통신을 위해 Java의 `java.util.concurrent.locks.Condition` 클래스를 사용하는 방법을 살펴보았다. Condition 사용에 대한 몇 가지 팁도 확인했습니다.