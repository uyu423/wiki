---
title: 스레드 차단을 위한 Java의 java.util.concurrent.locks.LockSupport 작업
description: 
published: true
date: 2023-01-31T13:04:28.573Z
tags: 
editor: markdown
dateCreated: 2023-01-31T13:04:25.076Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Working with Java's java.util.concurrent.locks.LockSupport for Thread Blocking***English** version of this document is available*](/en/Knowledge-base/Java/working-with-java-s-java-util-concurrent-locks-locksupport-for-thread-blocking)
{.links-list}



스레드 차단
===============

Java에서 스레드 차단은 스레드가 다른 리소스를 기다리고 있기 때문에 작업을 계속할 수 없는 경우입니다. 이는 스레드가 다른 스레드가 작업을 완료하기를 기다리는 경우 또는 스레드가 리소스를 사용할 수 있기를 기다리는 경우와 같은 여러 가지 이유로 발생할 수 있습니다.

두 경우 모두 스레드가 차단되었다고 합니다. 스레드가 차단되면 어떤 코드도 실행할 수 없으며 차단이 제거될 때까지 사실상 중단됩니다.

Java에서 스레드 차단을 처리하는 방법에는 여러 가지가 있습니다. 일반적인 접근 방식 중 하나는 java.util.concurrent.locks.LockSupport 클래스를 사용하는 것입니다.

LockSupport는 잠금 및 차단을 처리하기 위한 여러 가지 정적 메서드를 제공하는 유틸리티 클래스입니다. 이는 동시 애플리케이션 개발을 지원하도록 설계된 클래스 세트인 Java 동시성 유틸리티의 일부입니다.

LockSupport의 가장 일반적인 용도는 다른 스레드가 작업을 완료할 때까지 스레드를 차단하는 것입니다. 이는 park() 및 unpark() 메소드를 사용하여 수행할 수 있습니다.

park() 메서드는 동일한 스레드에서 unpark() 메서드가 호출될 때까지 현재 스레드를 차단합니다. unpark() 메서드는 모든 스레드에서 호출할 수 있지만 스레드가 현재 주차된 경우에만 효과가 있습니다.

스레드가 현재 파킹되지 않은 경우 unpark()는 아무 작업도 수행하지 않습니다.

다음은 다른 스레드가 작업을 완료할 때까지 스레드를 차단하기 위해 park() 및 unpark()를 사용하는 방법에 대한 간단한 예입니다.

```java
public static void main(String[] args) {
    Thread worker = new Thread(() -> {
        // do some work
        System.out.println("Worker is done.");

        // call unpark to unblock the main thread
        LockSupport.unpark(Thread.currentThread());
    });

    worker.start();

    System.out.println("Main thread is waiting for worker to finish.");

    // call park to block the main thread until unpark is called
    LockSupport.park();

    System.out.println("Main thread is done.");
}
```

이 예제에서 메인 스레드는 park()를 호출하여 자신을 차단합니다. 작업자 스레드는 몇 가지 작업을 수행한 다음 unpark()를 호출하여 기본 스레드의 차단을 해제합니다.

메인 스레드가 차단 해제되면 계속 실행되고 "메인 스레드가 완료되었습니다."가 인쇄됩니다.

LockSupport는 또한 잠금 및 차단을 처리하기 위한 여러 다른 방법을 제공합니다. 여기에는 tryLock(), isParked() 및 parkNanos()가 포함됩니다.

tryLock()은 park()와 유사하지만 현재 스레드를 차단하지 않습니다. 대신 잠금 획득을 시도하고 즉시 반환합니다. 잠금을 사용할 수 없으면 tryLock()은 false를 반환합니다.

isParked() 스레드가 현재 차단되었는지 확인하는 데 사용할 수 있습니다. 스레드가 차단된 경우 true를 반환하고 스레드가 차단되지 않은 경우 false를 반환합니다.

parkNanos()는 park()와 유사하지만 지정된 시간 동안 현재 스레드를 차단합니다. 시간은 나노초 단위로 지정됩니다.

 LockSupport는 스레드 차단을 처리하는 데 유용한 도구입니다. 스레드를 차단 및 차단 해제하고 잠금을 시도하고 획득하는 데 사용할 수 있는 여러 가지 정적 메서드를 제공합니다.