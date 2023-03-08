---
title: 동시 프로그래밍을 위한 Java의 java.util.concurrent.CountDownLatch 활용
description: 
published: true
date: 2023-02-17T18:16:39.278Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:23:27.399Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Leveraging Java's java.util.concurrent.CountDownLatch for Concurrent Programming***English** version of this document is available*](/en/Knowledge-base/Java/leveraging-java-s-java-util-concurrent-countdownlatch-for-concurrent-programming)
{.links-list}


# 동시 프로그래밍을 위해 Java의 java.util.concurrent.CountDownLatch 활용

Java 5 릴리스와 함께 새로운 동시성 유틸리티 세트가 플랫폼에 추가되었습니다. 이 중 하나인 'java.util.concurrent.CountDownLatch'는 다른 스레드에서 수행 중인 일련의 작업이 완료될 때까지 하나 이상의 스레드가 대기할 수 있도록 하는 동기화 지원입니다. 이 기사에서는 `CountDownLatch`를 사용하여 동시 프로그래밍에서 일반적인 문제를 해결하는 방법을 보여줍니다.

## CountDownLatch란 무엇입니까?

'CountDownLatch'는 양의 정수 'count'로 초기화됩니다. `await` 메소드는 `countDown` 메소드의 호출로 인해 현재 `count`가 0에 도달할 때까지 차단되며, 그 이후에는 모든 대기 중인 스레드가 차단 해제되고 계속할 수 있습니다.

'CountDownLatch'는 한 번만 사용할 수 있습니다. 재설정 가능한 버전이 필요한 경우 `java.util.concurrent.CyclicBarrier`를 참조하십시오.

## CountDownLatch 만들기

`CountDownLatch`를 생성하는 것은 카운트다운할 스레드 수를 생성자에 전달하는 간단한 문제입니다.

```java
int numThreads = 5;
CountDownLatch latch = new CountDownLatch(numThreads);
```

## 카운트 다운

`CountDownLatch`가 있으면 `countDown` 메서드를 호출하여 카운트다운할 수 있습니다.

```java
latch.countDown();
```

예외가 발생하더라도 `countDown` 메서드가 항상 호출되도록 `finally` 블록에서 이 작업을 수행하는 것이 일반적입니다.

```java
try {
    // do some work
} finally {
    latch.countDown();
}
```

## CountDownLatch를 기다리는 중

0까지 카운트 다운하면 `await` 메소드를 호출하여 다른 것을 기다릴 수 있습니다.

```java
latch.await();
```

지정된 시간 동안 기다리려면 `long` 및 `TimeUnit`을 사용하는 `await` 메서드를 사용할 수 있습니다.

```java
latch.await(1, TimeUnit.SECONDS);
```

이것은 '카운트'가 0이 될 때까지 최대 1초 동안 기다립니다. 그렇지 않으면 `await`는 `false`를 반환합니다.

## 사용 사례

이제 `CountDownLatch`의 작동 방식을 살펴보았으므로 몇 가지 일반적인 사용 사례를 살펴보겠습니다.

### 구성 요소 초기화

사용하기 전에 초기화해야 하는 구성 요소가 있다고 가정합니다. 이는 `CountDownLatch`로 수행할 수 있습니다.

```java
public class MyComponent {
    private final CountDownLatch latch = new CountDownLatch(1);

    public void init() {
        // do some work
        latch.countDown();
    }

    public void use() {
        try {
            latch.await();
            // do some work
        } catch (InterruptedException e) {
            // handle exception
        }
    }
}
```

이 예에서 `use` 메서드는 `init`가 호출될 때까지 차단됩니다.

### 롤러코스터 타기

두 대의 차가 있는 롤러코스터가 있다고 가정해 봅시다. 자동차는 동일하므로 병렬로 작동할 수 있습니다. 각 차는 최대 10명의 승객을 태울 수 있습니다. 승객이 병렬로 차량에 탑승할 수 있기를 원하지만 차량이 모두 가득 찰 때까지 역을 떠날 수 없습니다. 이는 `CountDownLatch`로 수행할 수 있습니다.

```java
public class RollerCoaster {
    private final CountDownLatch latch = new CountDownLatch(2);

    public void boardPassenger(Passenger p) {
        // do some work
        if (isFull()) {
            latch.countDown();
        }
    }

    public void run() {
        try {
            latch.await();
            // do some work
        } catch (InterruptedException e) {
            // handle exception
        }
    }

    // Other methods omitted for brevity
}
```

이 예에서 `run` 메서드는 두 차가 가득 찰 때까지 차단됩니다.

### 여러 이벤트를 기다리는 중

다중 스레드 프로그램이 있고 진행하기 전에 여러 이벤트가 발생하기를 기다리고 싶다고 가정합니다. 이는 `CountDownLatch`로 수행할 수 있습니다.

```java
public void doWork() {
    CountDownLatch latch = new CountDownLatch(3);

    // start three threads
    new Thread(new Runnable() {
        public void run() {
            // do some work
            latch.countDown();
        }
    }).start();

    new Thread(new Runnable() {
        public void run() {
            // do some work
            latch.countDown();
        }
    }).start();

    new Thread(new Runnable() {
        public void run() {
            // do some work
            latch.countDown();
        }
    }).start();

    try {
        latch.await();
        // do some work
    } catch (InterruptedException e) {
        // handle exception
    }
}
```

이 예에서 `doWork`는 세 스레드가 모두 완료될 때까지 차단됩니다.

## 결론

`java.util.concurrent.CountDownLatch`는 동시 프로그래밍의 다양한 문제를 해결하는 데 사용할 수 있는 간단하고 유연한 동기화 보조 도구입니다. 질문이 있으시면 아래에 의견을 남겨주십시오.