---
title: 작업 예약 및 실행을 위한 Java 실행자 프레임워크
description: 
published: true
date: 2023-03-05T12:32:37.918Z
tags: 
editor: markdown
dateCreated: 2023-03-05T12:32:30.693Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Java's Executor Framework for Task Scheduling and Execution***English** document is available*](/en/Knowledge-base/Java/java-s-executor-framework-for-task-scheduling-and-execution)
{.links-list}

## 소개
Java는 복잡한 애플리케이션을 구축하기 위해 일반적으로 사용되는 프로그래밍 언어입니다. 애플리케이션이 복잡해짐에 따라 효율적인 작업 예약 및 실행에 대한 필요성이 더욱 중요해졌습니다. Java Executor Framework는 다중 스레드 환경에서 작업을 관리하고 실행하기 위한 간단한 메커니즘을 제공합니다. 이 기사에서는 Executor 프레임워크를 자세히 살펴보고 태스크 예약 및 실행에 어떻게 사용할 수 있는지 살펴보겠습니다.

## 실행자 프레임워크가 무엇인가요?
Executor Framework는 Java 5에 도입된 java.util.concurrent 패키지의 일부입니다. 다중 스레드 환경에서 작업을 비동기적으로 관리하고 실행하는 방법을 제공합니다. 프레임워크에는 태스크와 실행자 간의 계약을 정의하는 인터페이스와 다양한 태스크 관리 방법을 제공하는 일련의 구현이 포함됩니다.

## 실행자 프레임워크는 어떻게 작동하나요?
Executor Framework는 스레드 풀을 사용하여 작업을 비동기식으로 실행합니다. 작업이 실행자에게 제출되면 실행자가 관리하는 대기열에 추가됩니다. 그런 다음 실행자는 대기열에서 작업을 선택하고 스레드 풀에서 스레드에 할당합니다. 스레드가 사용 가능해지면 대기열에서 작업이 할당됩니다. 이렇게 하면 작업이 제출될 때마다 새 스레드를 생성할 필요 없이 적시에 효율적인 방식으로 작업이 실행됩니다.

## 실행자
Executor Framework는 Executor 인터페이스의 여러 구현을 제공합니다. 이러한 구현은 작업을 관리하는 다양한 방법을 제공합니다. 일반적으로 사용되는 구현 중 일부는 다음과 같습니다.

### ThreadPoolExecutor
ThreadPoolExecutor는 Executor 인터페이스의 가장 일반적으로 사용되는 구현입니다. 고정 크기의 스레드 풀을 생성하고 블로킹 큐를 사용하여 작업을 관리합니다. 스레드 풀의 크기, 대기열에 보관할 수 있는 최대 작업 수 및 대기열이 가득 찼을 때 작업을 처리하는 정책을 지정할 수 있습니다.

```java
ExecutorService executor = Executors.newFixedThreadPool(10);

executor.submit(new RunnableTask());
```

### ScheduledThreadPoolExecutor
ScheduledThreadPoolExecutor는 특정 시간 또는 지정된 간격으로 실행되도록 작업을 예약할 수 있는 ThreadPoolExecutor의 확장입니다. 애플리케이션에서 정기적인 작업을 예약하는 간단한 방법을 제공합니다.

```java
ScheduledExecutorService executor = Executors.newScheduledThreadPool(10);

executor.schedule(new RunnableTask(), 5, TimeUnit.SECONDS);
```

### 단일 스레드 실행기
SingleThreadExecutor는 태스크를 실행하기 위해 단일 스레드를 생성하는 Executor 인터페이스의 구현입니다. 모든 작업이 순차적으로 실행되도록 하려는 경우에 유용합니다.

```java
ExecutorService executor = Executors.newSingleThreadExecutor();

executor.submit(new RunnableTask());
```

## 호출 가능 및 미래
Executor Framework에는 작업을 실행하고 결과를 검색하는 방법을 제공하는 Callable 및 Future라는 두 가지 인터페이스가 포함되어 있습니다.

### 호출 가능
Callable 인터페이스는 Runnable 인터페이스와 유사하지만 작업이 결과를 반환할 수 있도록 합니다. 계산 결과를 나타내는 형식 매개 변수를 사용하는 일반 인터페이스입니다. submit() 메서드를 사용하여 작업이 실행자에게 제출되면 계산 결과를 나타내는 Future 객체를 반환합니다.

```java
ExecutorService executor = Executors.newFixedThreadPool(10);

Future<Integer> result = executor.submit(new CallableTask());
```

### 미래
Future 인터페이스는 아직 완료되지 않은 계산 결과를 나타냅니다. 계산 상태를 확인하고 사용 가능할 때 결과를 검색하는 방법을 제공합니다. cancel() 메서드를 사용하여 계산을 취소할 수도 있습니다.

```java
ExecutorService executor = Executors.newFixedThreadPool(10);

Future<Integer> result = executor.submit(new CallableTask());

if(result.isDone()) {
  Integer value = result.get();
}
```

## 결론
Executor Framework는 멀티스레드 환경에서 작업을 비동기적으로 관리하고 실행하기 위한 강력한 도구입니다. 스레드 풀을 사용하여 작업을 관리하는 간단하고 효율적인 방법을 제공하며 다양한 사용 사례에 적합한 Executor 인터페이스의 여러 구현을 포함합니다.

## 외부 리소스
- [자바 동시성 실습](https://www.amazon.com/Java-Concurrency-Practice-Brian-Goetz/dp/0321349601)
- [자바 실행자 프레임워크 Javadoc](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/util/concurrent/ExecutorService.html)