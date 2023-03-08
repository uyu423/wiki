---
title: Java에서 사용자 지정 실행기 빌드
description: 
published: true
date: 2023-02-02T23:57:28.250Z
tags: 
editor: markdown
dateCreated: 2023-02-02T23:57:23.576Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building Custom Executors in Java***English** document is available*](/en/Knowledge-base/Java/building-custom-executors-in-java)
{.links-list}


# 자바로 커스텀 실행기 만들기

개발자는 작업을 병렬로 실행하기 위해 사용자 지정 실행기를 만들어야 하는 경우가 많습니다. 이 문서에서는 Java에서 이 작업을 수행하는 방법을 살펴보겠습니다.

## 스레드 풀 생성

사용자 지정 실행기를 만드는 첫 번째 단계는 스레드 풀을 만드는 것입니다. 이는 ```Executors``` 클래스를 사용하여 수행할 수 있습니다.

```java
ExecutorService executor = Executors.newFixedThreadPool(10);
```

이렇게 하면 10개의 스레드가 있는 스레드 풀이 생성됩니다. ```Executors``` 클래스를 사용하여 단일 스레드 실행기를 만들 수도 있습니다.

```java
ExecutorService executor = Executors.newSingleThreadExecutor();
```

## 작업 실행

실행자가 있으면 실행을 위해 작업을 제출할 수 있습니다. 예를 들어 ```Runnable``` 작업이 있다고 가정해 보겠습니다.

```java
Runnable task = () -> {
    // task logic here
};
```java
Callable<T> task = () -> {
    // task logic here
    return result;
};
```java
executor.submit(task);
```자바
실행자.제출(태스크);
```

```Callable``` 작업이 있는 경우 ```submit()``` 메소드를 사용하여 제출할 수도 있습니다.

```java
executor.shutdown();
```

## 스레드 풀 종료

작업 실행을 마치면 스레드 풀을 종료해야 합니다. 이는 ```shutdown()``` 메서드를 사용하여 수행할 수 있습니다:

```java
executor.shutdownNow();
```

스레드 풀을 즉시 종료하려면 ```shutdownNow()``` 메서드를 사용할 수 있습니다.

```자바
executor.shutdownNow();
```

## 자원

- [Java Executors and Thread Pools Tutorial](https://www.baeldung.com/java-executors-and-thread-pools)
- [Java 스레드 풀](https://www.geeksforgeeks.org/java-thread-pool/)
- [Java ExecutorService 튜토리얼](https://www.journaldev.com/1069/java-executor-service-example-thread-pool-executor)