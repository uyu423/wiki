---
title: 재진입 잠금을 위한 Java의 java.util.concurrent.locks.ReentrantLock
description: 
published: true
date: 2023-02-12T02:55:26.670Z
tags: 
editor: markdown
dateCreated: 2023-02-12T02:55:25.083Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Java's java.util.concurrent.locks.ReentrantLock for Reentrant Locking***English** document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-locks-reentrantlock-for-reentrant-locking)
{.links-list}


# 재진입 잠금을 위한 Java의 java.util.concurrent.locks.ReentrantLock

재진입 잠금은 Java 애플리케이션에서 스레드 안전을 보장하기 위해 널리 사용되는 메커니즘입니다. 이 기사에서는 Java에서 ReentrantLock이 작동하는 방식을 자세히 살펴보겠습니다.

ReentrantLock은 Java 동시성 유틸리티의 일부이며 Lock 인터페이스를 구현합니다. Java에서 사용할 수 있는 고유 잠금보다 더 정교한 잠금 메커니즘을 제공합니다.

ReentrantLock 공정성 정책

ReentrantLock에는 두 가지 유형의 공정성 정책이 있습니다.

* 공정한
* 불공평

공정한 정책은 잠금을 기다리는 동안 스레드가 굶주리는 것을 방지합니다. 공정한 ReentrantLock에서는 여러 스레드가 잠금을 기다리고 있을 때 가장 오래 기다린 스레드에 먼저 잠금이 부여됩니다.

비공정 정책은 기본 정책이며 스레드가 잠금을 획득하는 순서에 대해 보장하지 않습니다. 이 정책은 공정한 정책보다 더 효율적입니다.

ReentrantLock 작동 방식

ReentrantLock은 내부 잠금 개체를 사용하여 잠긴 상태를 나타냅니다. 스레드가 lock() 메서드를 호출하면 사용 가능한 경우 잠금을 획득합니다. 잠금을 사용할 수 없으면 스레드는 대기 상태가 됩니다.

스레드가 잠금을 획득하면 보류 횟수를 얻습니다. 스레드는 unlock() 메서드를 호출하여 잠금을 해제할 수 있습니다. 잠금은 스레드의 보류 횟수가 0이 될 때만 해제됩니다.

스레드가 이미 보유하고 있는 잠금을 획득하려고 하면 스레드의 보유 횟수가 증가합니다.

스레드는 unlock() 메서드를 호출하여 보유하지 않은 잠금을 해제할 수 있습니다. 이로 인해 IllegalMonitorStateException이 발생합니다.

tryLock() 메서드

tryLock() 메서드는 잠금을 획득하는 데 사용됩니다. 잠금을 사용할 수 있는 경우 스레드는 잠금을 획득하고 메서드는 true를 반환합니다. 잠금을 사용할 수 없으면 스레드가 차단되지 않고 메서드가 false를 반환합니다.

tryLock(long time, TimeUnit unit) 메서드는 지정된 시간 내에 잠금을 획득하는 데 사용됩니다. 잠금을 사용할 수 있는 경우 스레드는 잠금을 획득하고 메서드는 true를 반환합니다. 잠금을 사용할 수 없으면 지정된 시간이 만료될 때까지 스레드가 차단됩니다. 잠금을 사용할 수 있기 전에 시간이 만료되면 스레드는 잠금을 획득하지 못하고 메서드는 false를 반환합니다.

lockInterruptibly() 메소드

lockInterruptibly() 메서드는 잠금을 획득하는 데 사용됩니다. 잠금을 사용할 수 있으면 스레드가 잠금을 획득합니다. 잠금을 사용할 수 없으면 잠금을 사용할 수 있게 되거나 스레드가 중단될 때까지 스레드가 차단됩니다.

newCondition() 메소드

newCondition() 메서드는 이 Lock 인스턴스에 바인딩된 새 Condition 개체를 만듭니다.

isHeldByCurrentThread() 메서드

isHeldByCurrentThread() 메서드는 현재 스레드가 이 잠금을 보유하고 있으면 true를 반환하고 그렇지 않으면 false를 반환합니다.

isLocked() 메서드

isLocked() 메서드는 이 잠금이 스레드에 의해 유지되면 true를 반환하고 그렇지 않으면 false를 반환합니다.

getQueueLength() 메소드

getQueueLength() 메서드는 이 잠금을 획득하기 위해 대기 중인 스레드 수를 반환합니다.

hasQueuedThreads() 메서드

hasQueuedThreads() 메서드는 이 잠금을 획득하기 위해 대기 중인 스레드가 있으면 true를 반환하고 그렇지 않으면 false를 반환합니다.

isFair() 메서드

isFair() 메서드는 이 잠금이 공정하면 true를 반환하고 그렇지 않으면 false를 반환합니다.

getHoldCount() 메소드

getHoldCount() 메서드는 현재 스레드가 보유한 잠금 수를 반환합니다.

toString() 메서드

toString() 메서드는 이 잠금의 문자열 표현을 반환합니다.