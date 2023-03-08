---
title: 088: Spring Boot 및 Spring WebFlux를 사용하여 반응형 시스템 구축
description: 
published: true
date: 2023-02-05T18:32:33.233Z
tags: 
editor: markdown
dateCreated: 2023-02-05T18:32:31.610Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [088: Building a Reactive System with Spring Boot and Spring WebFlux***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/088-building-a-reactive-system-with-spring-boot-and-spring-webflux)
{.links-list}


# 088: Spring Boot와 Spring WebFlux로 리액티브 시스템 구축하기

이번 포스트에서는 Spring Boot와 Spring WebFlux를 사용하여 리액티브 시스템을 구축하는 방법에 대해 알아보겠습니다.

리액티브 시스템은 리액티브 매니페스토 원칙을 사용하여 구축된 시스템입니다. 이러한 시스템은 응답성이 뛰어나고 탄력적이며 탄력적이며 메시지 중심적입니다.

반응형 시스템에서 모든 구성 요소는 메시지 생성자이자 메시지 소비자입니다. 구성 요소는 메시지를 사용하여 서로 비동기식으로 통신합니다.

메시지 기반 시스템은 시스템의 나머지 부분에 영향을 주지 않고 장애를 처리할 수 있기 때문에 기존 시스템보다 확장성과 복원력이 뛰어납니다.

Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있는 프레임워크입니다.

Spring WebFlux는 반응형 프로그래밍 모델을 사용하여 웹 애플리케이션을 구축하기 위한 반응형 웹 프레임워크입니다.

이번 포스트에서는 Spring Boot와 Spring WebFlux를 사용하여 간단한 리액티브 시스템을 구축하는 방법에 대해 알아보겠습니다.

## 스프링 부트 프로젝트 생성

Spring Initializr를 사용하여 Spring Boot 프로젝트를 만들 수 있습니다. 다음 종속성을 선택해야 합니다.

- 웹
- 반응형 웹
- 롬복

Lombok은 애플리케이션에서 상용구 코드를 줄이는 데 사용할 수 있는 라이브러리입니다.

## 코드 작성

문자열 목록을 반환하는 간단한 컨트롤러를 만드는 것으로 시작하겠습니다.

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public List<String> hello() {
        return Arrays.asList("Hello", "World");
    }
}
```

컨트롤러에서 `hello()` 메서드에 `@GetMapping` 주석을 추가했습니다. 이 주석은 `hello()` 메서드를 `/hello` 경로에 매핑합니다.

또한 `@RestController` 주석으로 `HelloController` 클래스에 주석을 달았습니다. 이 주석은 클래스를 컨트롤러로 표시하고 Spring이 웹 요청을 처리할 수 있도록 합니다.

`@RestController` 주석은 클래스에 `@Controller` 및 `@ResponseBody` 주석을 추가하는 것과 같은 편리한 주석입니다.

`@ResponseBody` 주석은 Spring에게 `hello()` 메서드의 반환 값을 JSON으로 직렬화하고 응답 본문에 보내도록 지시합니다.

애플리케이션을 실행하고 `/hello` 경로에 요청하면 다음 JSON 응답이 표시됩니다.

```json
["Hello","World"]
```

## `hello()` 메서드를 반응성으로 만들기

`List<String>` 대신 `Mono<List<String>>`을 반환하여 `hello()` 메서드를 반응성으로 만들 수 있습니다.

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public Mono<List<String>> hello() {
        return Mono.just(Arrays.asList("Hello", "World"));
    }
}
```

'Mono' 클래스는 0 또는 1 요소의 스트림을 나타냅니다. 이 경우 문자열 목록을 래핑하는 데 사용합니다.

`just()` 메소드는 지정된 요소를 포함하는 `Mono`를 생성합니다.

`/hello` 경로에 요청하면 이전과 동일한 JSON 응답이 표시됩니다.

## `hello()` 메서드를 비동기로 만들기

`publishOn()` 연산자를 사용하여 `hello()` 메서드를 비동기식으로 만들 수 있습니다.

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public Mono<List<String>> hello() {
        return Mono.just(Arrays.asList("Hello", "World"))
                .publishOn(Schedulers.elastic());
    }
}
```

`publishOn()` 연산자는 지정된 스케줄러에 스트림의 요소를 게시하도록 Spring에 지시합니다. 이 경우 비동기 스케줄러인 `탄력적인` 스케줄러를 사용하고 있습니다.

`/hello` 경로에 요청하면 이전과 동일한 JSON 응답이 표시됩니다.

## `hello()` 메서드를 비블로킹으로 만들기

`subscribeOn()` 연산자를 사용하여 `hello()` 메서드를 차단하지 않도록 만들 수 있습니다.

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public Mono<List<String>> hello() {
        return Mono.just(Arrays.asList("Hello", "World"))
                .subscribeOn(Schedulers.elastic());
    }
}
```

`subscribeOn()` 연산자는 지정된 스케줄러에서 스트림을 구독하도록 Spring에 지시합니다. 이 경우 비동기 스케줄러인 `탄력적인` 스케줄러를 사용하고 있습니다.

`/hello` 경로에 요청하면 이전과 동일한 JSON 응답이 표시됩니다.

## 결론

이번 포스트에서는 Spring Boot와 Spring WebFlux를 사용하여 리액티브 시스템을 구축하는 방법에 대해 알아보았습니다. 또한 `hello()` 메서드를 반응성, 비동기성 및 비차단 방식으로 만드는 방법도 배웠습니다.