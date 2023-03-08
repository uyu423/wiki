---
title: 사용자 지정 잠금을 위한 Java의 java.util.concurrent.locks.AbstractQueuedSynchronizer
description: 
published: true
date: 2023-01-31T16:43:58.551Z
tags: 
editor: markdown
dateCreated: 2023-01-31T16:43:56.923Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Java's java.util.concurrent.locks.AbstractQueuedSynchronizer for Custom Locking***English** version of this document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-locks-abstractqueuedsynchronizer-for-custom-locking)
{.links-list}


# 사용자 지정 잠금을 위한 Java의 java.util.concurrent.locks.AbstractQueuedSynchronizer

Java의 `java.util.concurrent.locks.AbstractQueuedSynchronizer`(AQS)는 사용자 지정 잠금을 구축하기 위한 강력한 도구입니다. 이 문서에서는 AQS를 사용하여 간단한 잠금을 만드는 방법을 살펴보겠습니다. 또한 AQS를 사용하여 공정하고 재진입 가능한 잠금을 구현하는 데 사용할 수 있는 더 복잡한 잠금을 만드는 방법도 살펴보겠습니다.

## AQS로 간단한 잠금 만들기

AQS를 사용하여 간단한 잠금을 만드는 방법부터 살펴보겠습니다. 가장 먼저 해야 할 일은 `AbstractQueuedSynchronizer`를 확장하는 클래스를 만드는 것입니다. 이 클래스는 잠금 기능 구현을 담당합니다.

```java
public class MyLock extends AbstractQueuedSynchronizer {

}
```

다음으로 잠금을 획득하고 해제하는 데 사용할 메서드를 추가해야 합니다. 'acquire' 메서드는 잠금을 획득하는 데 사용되고 'release' 메서드는 잠금을 해제하는 데 사용됩니다. `MyLock` 클래스에서 `acquire` 및 `release` 메서드를 재정의하여 이러한 메서드를 추가할 수 있습니다.

```java
@Override
protected boolean tryAcquire(int arg) {
    // TODO: implement tryAcquire
}

@Override
protected boolean tryRelease(int arg) {
    // TODO: implement tryRelease
}
```

`tryAcquire` 메서드는 잠금 획득을 담당합니다. `tryRelease` 메서드는 잠금 해제를 담당합니다.

## tryAcquire 메소드 구현

'tryAcquire' 메서드는 잠금 획득을 담당합니다. `MyLock` 클래스에서 `acquireQueued` 메소드를 호출하여 `tryAcquire` 메소드를 구현할 수 있습니다. 'acquireQueued' 메서드는 잠금 획득을 시도하고 잠금이 획득되면 'true'를 반환합니다. 그렇지 않으면 'false'를 반환합니다.

```java
@Override
protected boolean tryAcquire(int arg) {
    return acquireQueued(new Node(), arg);
}
```

## tryRelease 메서드 구현

`tryRelease` 메서드는 잠금 해제를 담당합니다. `MyLock` 클래스에서 `release` 메소드를 호출하여 `tryRelease` 메소드를 구현할 수 있습니다. `release` 메서드는 잠금을 해제하고 잠금이 해제되면 `true`를 반환합니다. 그렇지 않으면 'false'를 반환합니다.

```java
@Override
protected boolean tryRelease(int arg) {
    return release(arg);
}
```

## 자물쇠 사용하기

이제 `MyLock` 클래스를 구현했으므로 이를 사용하는 방법을 살펴보겠습니다. 먼저 `MyLock` 클래스의 인스턴스를 생성해야 합니다.

```java
MyLock lock = new MyLock();
```

다음으로 `lock` 메서드를 호출하여 잠금을 획득할 수 있습니다.

```java
lock.lock();
```

잠금을 획득하면 잠금을 유지하는 동안 수행해야 하는 작업을 수행할 수 있습니다. 완료되면 `unlock` 메서드를 호출하여 잠금을 해제할 수 있습니다.

```java
lock.unlock();
```

## AQS로 공정한 재진입 잠금 만들기

AQS를 사용하여 간단한 잠금을 만드는 방법을 살펴보았으므로 이제 더 복잡한 잠금을 만드는 방법을 살펴보겠습니다. 이 섹션에서는 AQS를 사용하여 공정하고 재진입 가능한 잠금을 구현합니다.

공정한 재진입 잠금은 공정하고 동일한 스레드에서 여러 번 획득할 수 있는 잠금입니다. 스레드가 잠금을 획득하는 순서대로 보호하는 리소스에 대한 액세스 권한을 부여하는 경우 잠금은 공정합니다. 스레드가 잠금을 여러 번 획득할 수 있는 경우 잠금은 재진입 가능합니다.

AQS를 사용하여 공정하고 재진입 가능한 잠금을 만드는 방법부터 살펴보겠습니다. 가장 먼저 해야 할 일은 `AbstractQueuedSynchronizer`를 확장하는 클래스를 만드는 것입니다. 이 클래스는 잠금 기능 구현을 담당합니다.

```java
public class MyLock extends AbstractQueuedSynchronizer {

}
```

다음으로 잠금을 획득하고 해제하는 데 사용할 메서드를 추가해야 합니다. 'acquire' 메서드는 잠금을 획득하는 데 사용되고 'release' 메서드는 잠금을 해제하는 데 사용됩니다. `MyLock` 클래스에서 `acquire` 및 `release` 메서드를 재정의하여 이러한 메서드를 추가할 수 있습니다.

```java
@Override
protected boolean tryAcquire(int arg) {
    // TODO: implement tryAcquire
}

@Override
protected boolean tryRelease(int arg) {
    // TODO: implement tryRelease
}
```

`tryAcquire` 메서드는 잠금 획득을 담당합니다. `tryRelease` 메서드는 잠금 해제를 담당합니다.

## tryAcquire 메소드 구현

'tryAcquire' 메서드는 잠금 획득을 담당합니다. `MyLock` 클래스에서 `acquireQueued` 메소드를 호출하여 `tryAcquire` 메소드를 구현할 수 있습니다. 'acquireQueued' 메서드는 잠금 획득을 시도하고 잠금이 획득되면 'true'를 반환합니다. 그렇지 않으면 'false'를 반환합니다.

```java
@Override
protected boolean tryAcquire(int arg) {
    return acquireQueued(new Node(), arg);
}
```

## tryRelease 메서드 구현

`tryRelease` 메서드는 잠금 해제를 담당합니다. `MyLock` 클래스에서 `release` 메소드를 호출하여 `tryRelease` 메소드를 구현할 수 있습니다. `release` 메서드는 잠금을 해제하고 잠금이 해제되면 `true`를 반환합니다. 그렇지 않으면 'false'를 반환합니다.

```java
@Override
protected boolean tryRelease(int arg) {
    return release(arg);
}
```

## 자물쇠 사용하기

이제 `MyLock` 클래스를 구현했으므로 이를 사용하는 방법을 살펴보겠습니다. 먼저 `MyLock` 클래스의 인스턴스를 생성해야 합니다.

```java
MyLock lock = new MyLock();
```

다음으로 `lock` 메서드를 호출하여 잠금을 획득할 수 있습니다.

```java
lock.lock();
```

잠금을 획득하면 잠금을 유지하는 동안 수행해야 하는 작업을 수행할 수 있습니다. 완료되면 `unlock` 메서드를 호출하여 잠금을 해제할 수 있습니다.

```java
lock.unlock();
```

## 결론

이 기사에서는 Java의 `java.util.concurrent.locks.AbstractQueuedSynchronizer`를 사용하여 간단한 잠금과 공정하고 재진입 가능한 잠금을 만드는 방법을 살펴보았습니다. 잠금을 획득하고 해제하기 위해 `acquire` 및 `release` 메서드를 사용하는 방법을 살펴보았습니다. 또한 `lock` 및 `unlock` 메서드를 사용하여 잠금을 획득하고 해제하는 방법도 살펴보았습니다.