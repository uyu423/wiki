---
title: 동시 데이터 교환을 위한 Java의 java.util.concurrent.Exchanger 가이드
description: 
published: true
date: 2023-02-04T06:55:23.714Z
tags: 
editor: markdown
dateCreated: 2023-02-04T06:55:21.833Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [A Guide to Java's java.util.concurrent.Exchanger for Concurrent Data Exchange***English** document is available*](/en/Knowledge-base/Java/a-guide-to-java-s-java-util-concurrent-exchanger-for-concurrent-data-exchange)
{.links-list}


# 동시 데이터 교환을 위한 Java의 java.util.concurrent.Exchanger 가이드

동시 프로그래밍에서 스레드 간의 데이터 교환은 일반적인 작업입니다. Java Concurrent API의 Exchanger 클래스는 스레드가 안전하고 편리한 방식으로 데이터를 교환할 수 있는 메커니즘을 제공합니다.

이 문서에서는 Exchanger 클래스에 대한 개요를 제공하고 동시 프로그램에서 사용할 수 있는 방법을 보여줍니다.

## Exchanger 클래스가 무엇인가요?

Exchanger 클래스는 스레드 간에 데이터를 교환하기 위한 유틸리티 클래스입니다. 교환할 데이터와 시간 초과 값이라는 두 개의 인수를 사용하는 단일 메서드 exchange()를 제공합니다.

데이터 교환을 기다리는 다른 스레드가 있는 경우 exchange() 메서드는 다른 스레드의 데이터와 함께 즉시 반환됩니다. 대기 중인 다른 스레드가 없으면 다른 스레드가 동일한 데이터로 exchange()를 호출할 때까지 exchange() 메서드는 차단됩니다.

Exchanger 클래스는 생산자-소비자 관계와 같이 두 스레드가 데이터를 동기화해야 하는 상황에 유용합니다.

## Exchanger 클래스 사용

다음은 Exchanger 클래스를 사용하는 방법에 대한 간단한 예입니다. 이 예제에서는 두 개의 스레드를 사용하여 데이터를 교환합니다. 첫 번째 스레드는 난수를 생성하고 두 번째 스레드는 해당 숫자의 제곱을 계산합니다.

```java
import java.util.concurrent.Exchanger;

public class ExchangerExample {
    public static void main(String[] args) {
        Exchanger<Integer> exchanger = new Exchanger<>();
        
        new Thread(() -> {
            try {
                int data = (int) (Math.random() * 100);
                System.out.println("Thread 1: " + data);
                
                data = exchanger.exchange(data);
                
                System.out.println("Thread 1: " + data);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();
        
        new Thread(() -> {
            try {
                int data = (int) (Math.random() * 100);
                System.out.println("Thread 2: " + data);
                
                data = exchanger.exchange(data);
                
                System.out.println("Thread 2: " + data);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }).start();
    }
}
```

이 예제에서는 두 스레드가 데이터를 교환한 다음 결과를 인쇄합니다. 이 프로그램의 출력은 다음과 같습니다.

```
Thread 1: 97
Thread 2: 25
Thread 1: 625
Thread 2: 676
```

## 결론

Exchanger 클래스는 스레드가 안전하고 편리한 방식으로 데이터를 교환할 수 있는 메커니즘을 제공합니다. 두 스레드가 데이터를 동기화해야 하는 상황에 유용합니다.