---
title: 병렬 프로그래밍을 위한 Java의 java.util.concurrent 패키지
description: 
published: true
date: 2023-02-01T21:57:42.280Z
tags: 
editor: markdown
dateCreated: 2023-02-01T21:57:40.659Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Java's java.util.concurrent Package for Parallel Programming***English** document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-package-for-parallel-programming)
{.links-list}


# 병렬 프로그래밍을 위한 Java의 java.util.concurrent 패키지

`java.util.concurrent` 패키지는 다중 스레드 프로그래밍을 지원하는 일련의 클래스 및 인터페이스를 제공합니다. 이 패키지를 사용하면 개발자가 여러 프로세서를 활용하는 프로그램을 쉽게 작성할 수 있습니다.

`java.util.concurrent` 패키지에는 다음 항목이 포함되어 있습니다.

* 실행자
* 선물
* 스레드 풀
* 자물쇠
* 원자 변수
* 동시 수집
* 싱크로나이저

이 기사에서는 `java.util.concurrent` 패키지를 사용하여 병렬 프로그램을 작성하는 방법에 중점을 둘 것입니다.

## 실행자

`Executor`는 제출된 `Runnable` 작업을 실행하는 개체입니다. 'Executor' 인터페이스는 대기열, 예약 및 실행을 포함하여 각 작업이 실행되는 방식의 메커니즘에서 작업 제출을 분리하는 방법을 제공합니다.

`java.util.concurrent` 패키지에는 `ThreadPoolExecutor` 및 `ScheduledThreadPoolExecutor`와 같은 여러 내장 `Executor` 구현이 있습니다. 자체 `Executor` 구현을 만들 수도 있습니다.

다음 예제에서는 `Runnable` 태스크를 생성하고 실행을 위해 `Executor`에 제출합니다.

```java
Runnable task = () -> {
    // Do something
};

Executor executor = Executors.newSingleThreadExecutor();
executor.execute(task);
```

## 선물

'Future'는 비동기 계산의 결과를 나타냅니다. 계산이 완료되었는지 확인하고 계산 결과를 검색하기 위해 `Future`를 사용할 수 있습니다.

다음 예제에서는 `Future`를 사용하여 작업이 완료되었는지 확인하고 결과를 검색합니다.

```java
Future<Integer> future = executor.submit(task);

if (future.isDone()) {
    int result = future.get();
}
```

## 스레드 풀

`ThreadPool`은 작업을 실행하는 데 사용할 수 있는 `Threads`의 모음입니다. 'ThreadPool'은 풀에서 'Threads'를 관리하고 사용 가능한 경우 'Threads'를 재사용하는 메커니즘을 제공합니다.

다음 예에서는 4개의 `Threads`가 있는 `ThreadPool`을 생성합니다.

```java
ExecutorService threadPool = Executors.newFixedThreadPool(4);
```

실행을 위해 `Runnable` 작업을 `ThreadPool`에 제출할 수 있습니다.

```java
threadPool.submit(task);
```

`ThreadPool` 작업이 끝나면 종료할 수 있습니다.

```java
threadPool.shutdown();
```

## 잠금

'잠금'은 공유 리소스에 대한 액세스를 제어하는 메커니즘입니다. 잠금은 원자적으로 실행되어야 하는 코드 섹션인 중요 섹션을 구현하는 데 사용할 수 있습니다.

다음 예에서는 '잠금'을 사용하여 공유 리소스에 대한 액세스를 제어합니다.

```java
Lock lock = new ReentrantLock();

lock.lock();
try {
    // Access the shared resource
} finally {
    lock.unlock();
}
```

## 원자 변수

'AtomicVariable'은 원자적으로 업데이트할 수 있는 변수입니다. `AtomicVariable`은 중요한 섹션을 구현하는 데 사용됩니다.

다음 예제에서는 `AtomicVariable`을 사용하여 공유 리소스에 대한 액세스를 제어합니다.

```java
AtomicInteger counter = new AtomicInteger();

int value = counter.incrementAndGet();
```

## 동시 수집

`java.util.concurrent` 패키지에는 여러 스레드에서 안전하게 사용할 수 있는 컬렉션인 여러 동시 컬렉션이 포함되어 있습니다.

다음 예제에서는 `ConcurrentHashMap`을 사용하여 스레드로부터 안전한 방식으로 데이터를 저장합니다.

```java
ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();

map.put("foo", 42);
map.get("foo");
```

## 싱크로나이저

`동기화 장치`는 여러 스레드의 작업을 조정하는 개체입니다. `java.util.concurrent` 패키지에는 `Semaphore` 및 `CountDownLatch`와 같은 여러 동기화 장치가 포함되어 있습니다.

다음 예에서는 `CountDownLatch`를 사용하여 작업이 완료될 때까지 기다립니다.

```java
CountDownLatch latch = new CountDownLatch(1);

executor.submit(() -> {
    try {
        // Do something
        latch.countDown();
    } catch (InterruptedException e) {
        // Handle the exception
    }
});

latch.await();
```

## 결론

이 기사에서는 `java.util.concurrent` 패키지를 사용하여 병렬 프로그램을 작성하는 방법을 살펴보았습니다. `Executors`, `Futures`, `ThreadPools`, `Locks`, `AtomicVariables`, `ConcurrentCollections` 및 `Synchronizers`를 사용하는 방법을 살펴보았습니다.