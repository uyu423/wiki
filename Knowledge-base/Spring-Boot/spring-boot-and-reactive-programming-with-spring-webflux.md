---
title: Spring WebFlux를 사용한 Spring Boot 및 반응형 프로그래밍
description: 
published: true
date: 2023-02-01T03:18:35.867Z
tags: 
editor: markdown
dateCreated: 2023-02-01T03:18:31.781Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Spring Boot and Reactive Programming with Spring WebFlux***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-reactive-programming-with-spring-webflux)
{.links-list}


  이 블로그의 대상 독자는 Spring WebFlux를 사용한 Spring Boot 및 Reactive 프로그래밍에 대해 배우고자 하는 IT 개발 전문가입니다.


# Spring WebFlux를 사용한 Spring Boot 및 Reactive 프로그래밍

Spring Boot는 개발자가 웹 애플리케이션을 신속하게 만들고 배포할 수 있도록 하는 인기 있는 Java 애플리케이션 프레임워크입니다. Spring Boot는 Spring Framework 위에 구축되며 Java 플랫폼을 사용합니다.

리액티브 프로그래밍은 응답성과 탄력성이 뛰어난 코드를 작성하는 데 도움이 되는 프로그래밍 패러다임입니다. 차단되지 않고 비동기적인 이벤트 기반 프로그래밍 스타일입니다.

Spring WebFlux는 Spring Framework 위에 구축된 웹 애플리케이션을 위한 반응형 프로그래밍 모델입니다. 완전히 차단되지 않고 배압을 지원하며 이벤트 루프 실행 모델을 사용합니다.

이 기사에서는 Spring Boot 및 Spring WebFlux를 사용하여 반응형 웹 애플리케이션을 만드는 방법을 살펴봅니다. 또한 Reactive Streams API를 사용하여 이벤트 스트림을 생성하는 방법도 살펴보겠습니다.

## 스프링 부트 프로젝트 설정

가장 먼저 해야 할 일은 새로운 Spring Boot 프로젝트를 만드는 것입니다. Spring Initializr 웹 사이트를 사용하여 필요한 종속성이 있는 프로젝트를 생성할 수 있습니다.

다음 종속성을 선택해야 합니다.

* 웹 - 웹 애플리케이션용
* 반응형 웹 - 반응형 프로그래밍 모델용
* Lombok - 상용구 코드 단순화

![스프링 이니셜라이저](https://i.imgur.com/Rv4U2in.png)

프로젝트가 생성되면 선호하는 IDE로 가져올 수 있습니다. IntelliJ IDEA를 사용하겠습니다.

## 헬로월드

간단한 Hello World 웹 애플리케이션을 만들어 보겠습니다. 클라이언트에 문자열을 반환하는 컨트롤러를 생성합니다.

먼저 `com.example.demo` 패키지에 `HelloController.java`라는 새 파일을 만들어야 합니다.

```java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello, World!";
    }

}
```

`HelloController` 클래스에서 `@RestController`로 클래스에 주석을 달았습니다. 이 주석은 클래스를 웹 컨트롤러로 표시하는 데 사용됩니다.

또한 `@GetMapping`으로 `hello()` 메서드에 주석을 달았습니다. 이 주석은 HTTP GET 요청을 `hello()` 메서드에 매핑하는 데 사용됩니다.

`hello()` 메서드는 문자열을 반환합니다. 이 문자열은 JSON으로 변환되어 클라이언트로 반환됩니다.

이제 애플리케이션을 실행하고 `/hello` 엔드포인트에 액세스할 수 있습니다. 다음 출력이 표시됩니다.

```
Hello, World!
```

## 리액티브 스트림

Reactive Streams는 비차단 배압을 사용하는 비동기 스트림 처리를 위한 API입니다. 4개의 인터페이스로 구성됩니다.

* 게시자 - 데이터 스트림을 내보냅니다.
* 가입자 - 데이터 스트림을 소비합니다.
* 프로세서 - 데이터 스트림을 변환합니다.
* 구독 - 게시자와 구독자 간의 일대일 관계를 나타냅니다.

Reactive Streams는 특정 프로그래밍 언어나 플랫폼에 얽매이지 않습니다. 언어에 구애받지 않으며 모든 JVM 기반 언어와 함께 사용할 수 있습니다.

## 스트림 만들기

이제 Reactive Streams API를 사용하여 이벤트 스트림을 생성하는 방법을 살펴보겠습니다. 정수 스트림을 방출하기 위해 `Publisher` 인터페이스를 사용할 것입니다.

먼저 `com.example.demo` 패키지에 `Publisher.java`라는 새 파일을 만들어야 합니다.

```java
package com.example.demo;

import org.reactivestreams.Publisher;
import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

import java.util.concurrent.atomic.AtomicInteger;

public class Publisher implements org.reactivestreams.Publisher<Integer> {

    private Subscriber<? super Integer> subscriber;
    private AtomicInteger counter;

    public Publisher() {
        this.counter = new AtomicInteger();
    }

    @Override
    public void subscribe(Subscriber<? super Integer> s) {
        this.subscriber = s;
        this.subscriber.onSubscribe(new Subscription() {
            @Override
            public void request(long n) {
                for (int i = 0; i < n; i++) {
                    if (counter.incrementAndGet() > 10) {
                        subscriber.onComplete();
                        break;
                    } else {
                        subscriber.onNext(counter.get());
                    }
                }
            }

            @Override
            public void cancel() {

            }
        });
    }
}
```

`Publisher` 클래스에서 `Publisher` 인터페이스의 `subscribe()` 메서드를 구현했습니다. 이 메서드는 스트림에 '구독자'를 구독하는 데 사용됩니다.

`subscribe()` 메서드에서 익명의 `Subscription` 개체를 사용하고 있습니다. 이 개체는 `게시자`에서 데이터를 요청하는 데 사용됩니다. `게시자`에게 10개의 항목을 요청하고 있습니다.

또한 `Publisher`가 내보낸 항목 수를 추적하기 위해 `AtomicInteger`를 사용하고 있습니다.

## 스트림 구독

이제 `Publisher`가 내보낸 이벤트 스트림을 구독할 수 있습니다. `Publisher` 인터페이스에서 `subscribe()` 메서드를 사용합니다.

먼저 `com.example.demo` 패키지에 `Subscriber.java`라는 새 파일을 만들어야 합니다.

```java
package com.example.demo;

import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

public class Subscriber implements org.reactivestreams.Subscriber<Integer> {

    @Override
    public void onSubscribe(Subscription s) {
        s.request(Long.MAX_VALUE);
    }

    @Override
    public void onNext(Integer integer) {
        System.out.println("Received: " + integer);
    }

    @Override
    public void onError(Throwable t) {
        t.printStackTrace();
    }

    @Override
    public void onComplete() {
        System.out.println("Done!");
    }
}
```

`Subscriber` 클래스에서 `Subscriber` 인터페이스의 `onSubscribe()` 메서드를 구현했습니다. 이 메서드는 이벤트 스트림을 구독하는 데 사용됩니다.

`onSubscribe()` 메소드에서 `Publisher`로부터 무제한 이벤트 스트림을 요청하고 있습니다.

또한 `onNext()`, `onError()` 및 `onComplete()` 메서드도 구현했습니다. 이러한 메서드는 `Publisher`에서 이벤트를 내보낼 때 호출됩니다.

## 스트림 테스트

이제 `Publisher`가 내보낸 이벤트 스트림을 테스트할 수 있습니다.

먼저 `com.example.demo` 패키지에 `DemoApplicationTests.java`라는 새 파일을 만들어야 합니다.

```java
package com.example.demo;

import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class DemoApplicationTests {

    @Test
    public void testStream() {
        Publisher publisher = new Publisher();
        Subscriber subscriber = new Subscriber();
        publisher.subscribe(subscriber);
    }

}
```

`DemoApplicationTests` 클래스에서 `testStream()` 메서드를 만들었습니다. 이 방법에서는 `Publisher` 및 `Subscriber`를 생성합니다. 그런 다음 `구독자`를 `게시자`에 구독합니다.

테스트를 실행하면 다음 출력이 표시됩니다.

```
Received: 1
Received: 2
Received: 3
Received: 4
Received: 5
Received: 6
Received: 7
Received: 8
Received: 9
Received: 10
Done!
```

## 반응형 웹 애플리케이션 만들기

이제 Reactive Streams API를 사용하는 방법을 살펴보았으므로 이를 사용하여 반응형 웹 애플리케이션을 만드는 방법을 살펴보겠습니다.

반응형 웹 애플리케이션은 반응형 프로그래밍 모델을 사용하는 웹 애플리케이션입니다. 반응형 프로그래밍 모델에서 애플리케이션은 메시지 전달을 사용하여 서로 통신하는 작고 독립적인 동시 프로세스 집합으로 구축됩니다.

반응형 웹 애플리케이션에서 웹 애플리케이션은 메시지 전달을 사용하여 서로 통신하는 작고 독립적인 동시 프로세스 집합으로 구축됩니다.

## 안녕하세요 리액티브 월드

간단한 "Hello Reactive World" 웹 애플리케이션을 만들어 보겠습니다. 클라이언트에 문자열을 반환하는 컨트롤러를 생성합니다.

먼저 `com.example.demo` 패키지에 `HelloReactiveController.java`라는 새 파일을 만들어야 합니다.

```java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import reactor.core.publisher.Mono;

@RestController
public class HelloReactiveController {

    @GetMapping("/hello-reactive")
    public Mono<String> helloReactive() {
        return Mono.just("Hello, Reactive World!");
    }

}
```

`HelloReactiveController` 클래스에서 `@RestController`로 클래스에 주석을 달았습니다. 이 주석은 클래스를 웹 컨트롤러로 표시하는 데 사용됩니다.

또한 `@GetMapping`으로 `helloReactive()` 메서드에 주석을 달았습니다. 이 주석은 HTTP GET 요청을 `helloReactive()` 메서드에 매핑하는 데 사용됩니다.

`helloReactive()` 메서드는 `Mono<String>`을 반환합니다. 'Mono'는 0개 또는 1개의 항목을 방출하는 반응형 스트림입니다. 이 경우 `Mono`는 단일 문자열을 내보냅니다.

이제 애플리케이션을 실행하고 `/hello-reactive` 엔드포인트에 액세스할 수 있습니다. 다음 출력이 표시됩니다.

```
Hello, Reactive World!
```

## 반응형 스트림 만들기

간단한 반응형 웹 애플리케이션을 만드는 방법을 살펴보았으므로 이제 더 복잡한 반응형 스트림을 만드는 방법을 살펴보겠습니다.

`Publisher`에서 방출하는 정수 스트림을 생성합니다. 그런 다음 'Processor'를 사용하여 정수 스트림을 문자열 스트림으로 변환합니다. 마지막으로 `Subscriber`를 사용하여 문자열 스트림을 소비합니다.

먼저 `com.example.demo` 패키지에 `Publisher.java`라는 새 파일을 만들어야 합니다.

```java
package com.example.demo;

import org.reactivestreams.Publisher;
import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

import java.util.concurrent.atomic.AtomicInteger;

public class Publisher implements org.reactivestreams.Publisher<Integer> {

    private Subscriber<? super Integer> subscriber;
    private AtomicInteger counter;

    public Publisher() {
        this.counter = new AtomicInteger();
    }

    @Override
    public void subscribe(Subscriber<? super Integer> s) {
        this.subscriber = s;
        this.subscriber.onSubscribe(new Subscription() {
            @Override
            public void request(long n) {
                for (int i = 0; i < n; i++) {
                    if (counter.incrementAndGet() > 10) {
                        subscriber.onComplete();
                        break;
                    } else {
                        subscriber.onNext(counter.get());
                    }
                }
            }

            @Override
            public void cancel() {

            }
        });
    }
}
```

`Publisher` 클래스에서 `Publisher` 인터페이스의 `subscribe()` 메서드를 구현했습니다. 이 메서드는 스트림에 '구독자'를 구독하는 데 사용됩니다.

`subscribe()` 메서드에서 익명의 `Subscription` 개체를 사용하고 있습니다. 이 개체는 `게시자`에서 데이터를 요청하는 데 사용됩니다. `게시자`에게 10개의 항목을 요청하고 있습니다.

또한 `Publisher`가 내보낸 항목 수를 추적하기 위해 `AtomicInteger`를 사용하고 있습니다.

## 스트림 변환

이제 `프로세서`를 사용하여 정수 스트림을 문자열 스트림으로 변환할 수 있습니다. `Processor` 인터페이스의 `map()` 메서드를 사용하여 각 정수를 문자열로 변환합니다.

먼저 `com.example.demo` 패키지에 `Processor.java`라는 새 파일을 만들어야 합니다.

```java
package com.example.demo;

import org.reactivestreams.Processor;
import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

public class Processor implements org.reactivestreams.Processor<Integer, String> {

    private Subscriber<? super String> subscriber;
    private Subscription subscription;

    @Override
    public void subscribe(Subscriber<? super String> s) {
        this.subscriber = s;
        this.subscriber.onSubscribe(new Subscription() {
            @Override
            public void request(long n) {
                subscription.request(n);
            }

            @Override
            public void cancel() {
                subscription.cancel();
            }
        });
    }

    @Override
    public void onSubscribe(Subscription s) {
        this.subscription = s;
        this.subscription.request(Long.MAX_VALUE);
    }

    @Override
    public void onNext(Integer integer) {
        this.subscriber.onNext(integer.toString());
    }

    @Override
    public void onError(Throwable t) {
        this.subscriber.onError(t);
    }

    @Override
    public void onComplete() {
        this.subscriber.onComplete();
    }
}
```

`Processor` 클래스에서 `Processor` 인터페이스의 `subscribe()` 및 `onSubscribe()` 메서드를 구현했습니다. 이러한 메서드는 스트림에 '구독자'를 구독하는 데 사용됩니다.

`subscribe()` 메서드에서 익명의 `Subscription` 개체를 사용하고 있습니다. 이 개체는 `게시자`에서 데이터를 요청하는 데 사용됩니다. `게시자`에게 제한 없는 이벤트 스트림을 요청하고 있습니다.

또한 `Publisher`가 내보낸 항목 수를 추적하기 위해 `AtomicInteger`를 사용하고 있습니다.

## 스트림 소비

이제 `Processor`가 방출하는 문자열 스트림을 사용하기 위해 `Subscriber`를 사용할 수 있습니다.

먼저 `com.example.demo` 패키지에 `Subscriber.java`라는 새 파일을 만들어야 합니다.

```java
package com.example.demo;

import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

public class Subscriber implements org.reactivestreams.Subscriber<String> {

    @Override
    public void onSubscribe(Subscription s) {
        s.request(Long.MAX_VALUE);
    }

    @Override
    public void onNext(String s) {
        System.out.println("Received: " + s);
    }

    @Override
    public void onError(Throwable t) {
        t.printStackTrace();
    }

    @Override
    public void onComplete() {
        System.out.println("Done!");
    }
}
```

`구독자` 클래스에서 `onSubscribe()` 메서드를 구현했습니다.