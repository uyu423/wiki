---
title: 제어된 동시 액세스를 위한 Java의 java.util.concurrent.Semaphore
description: 
published: true
date: 2023-02-02T01:23:26.344Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:23:24.788Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Java's java.util.concurrent.Semaphore for Controlled Concurrent Access***English** document is available*](/en/Knowledge-base/Java/java-s-java-util-concurrent-semaphore-for-controlled-concurrent-access)
{.links-list}


# 제어된 동시 액세스를 위한 Java의 java.util.concurrent.Semaphore

다중 스레드 프로그래밍에서는 주어진 시간에 리소스나 코드 블록에 액세스할 수 있는 스레드 수를 제한해야 하는 경우가 많습니다. 이를 동시성 제어라고 합니다.

Java에서 동시성 제어를 달성하는 한 가지 방법은 `java.util.concurrent.Semaphore` 클래스를 사용하는 것입니다.

세마포어는 스레드가 한 번에 하나의 스레드에서만 실행할 수 있는 코드 블록인 임계 영역에 들어갈 수 있도록 하는 토큰입니다. 스레드가 임계 영역을 종료하면 세마포어를 풀로 반환합니다.

세마포어는 코드뿐만 아니라 모든 리소스에 대한 액세스를 제어하는 데 사용할 수 있습니다. 예를 들어 세마포어를 사용하여 프린터나 데이터베이스에 대한 액세스를 제어할 수 있습니다.

## 세마포어 생성

세마포어는 허가 수를 지정하여 생성됩니다. 크리티컬 섹션에 동시에 접근할 수 있는 쓰레드의 수이다. 예를 들어 허가가 10개인 세마포어를 만들려면 다음을 수행합니다.

```java
Semaphore semaphore = new Semaphore(10);
```

## 허가 요청

스레드는 `acquire()` 메서드를 호출하여 허가를 요청합니다. 이 메서드는 허가를 사용할 수 있을 때까지 스레드를 차단합니다. 예를 들어:

```java
semaphore.acquire();
```

## 허가증 발급

쓰레드가 크리티컬 섹션을 빠져나오면 `release()` 메소드를 호출하여 허가를 세마포어에 반환합니다. 예를 들어:

```java
semaphore.release();
```

## 예

다음 예제에서는 세마포어를 사용하여 프린터에 대한 액세스를 제어하는 방법을 보여줍니다.

```java
import java.util.concurrent.Semaphore;

public class Printer {
    private Semaphore semaphore;

    public Printer(int numPermits) {
        semaphore = new Semaphore(numPermits);
    }

    public void print(String document) {
        try {
            semaphore.acquire();
            // print the document
        } catch (InterruptedException e) {
            // handle error
        } finally {
            semaphore.release();
        }
    }
}
```

이 예제에서 `print()` 메서드는 문서를 인쇄하기 전에 허가를 획득합니다. 사용 가능한 허가가 없으면 'acquire()' 메서드는 사용 가능할 때까지 스레드를 차단합니다. 문서를 인쇄한 후 `release()` 메서드는 허가를 세마포어에 반환합니다.

## 세마포어와 잠금의 차이점

세마포어와 잠금은 모두 동시성 제어를 위한 메커니즘입니다. 그러나 그들 사이에는 몇 가지 주요 차이점이 있습니다.

- 세마포어는 여러 허가를 가질 수 있지만 잠금은 하나만 가질 수 있습니다.
- 세마포어는 획득하지 않은 스레드에 의해 해제될 수 있는 반면 잠금은 획득한 스레드에 의해서만 해제될 수 있습니다.
- 세마포어에는 소유권 개념이 없지만 잠금 장치에는 있습니다.

## 결론

Java의 `java.util.concurrent.Semaphore` 클래스는 동시성 제어를 위한 메커니즘을 제공합니다. 세마포어는 코드뿐만 아니라 모든 리소스에 대한 액세스를 제어하는 데 사용할 수 있습니다. 세마포어를 사용할 때 세마포어와 잠금 간의 차이점을 기억하는 것이 중요합니다.