---
title: 093: 스프링 부트 추적 시스템 이해 및 구성
description: 
published: true
date: 2023-02-04T20:55:17.528Z
tags: 
editor: markdown
dateCreated: 2023-02-04T20:55:15.925Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [093: Understanding and Configuring the Spring Boot Tracing System***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/093-understanding-and-configuring-the-spring-boot-tracing-system)
{.links-list}


# 093: 스프링 부트 추적 시스템 이해 및 구성

Spring Boot는 시스템을 통해 흐르는 요청에 대한 정보를 수집하고 보는 데 사용할 수 있는 추적 시스템을 제공합니다. 이는 디버깅 목적이나 시스템 성능 모니터링에 유용할 수 있습니다.

이 게시물에서는 Spring Boot 추적 시스템을 구성하는 방법과 이를 사용하여 요청 처리에 대한 정보를 수집하는 방법을 살펴보겠습니다.

## Spring Boot 추적 시스템 구성

Spring Boot 추적 시스템은 `application.properties` 파일의 `spring.sleuth` 속성을 사용하여 구성됩니다. 다음 속성을 사용하여 추적 시스템을 구성할 수 있습니다.

- `spring.sleuth.sampler.probability`: 요청이 샘플링될 확률입니다. 기본값은 1.0이며 모든 요청이 샘플링됨을 의미합니다.

- `spring.sleuth.sampler.spans`: 단일 요청에 대해 생성할 수 있는 최대 스팬 수입니다. 기본값은 100입니다.

- `spring.sleuth.trace-id128`: true로 설정하면 128비트 트레이스 ID가 생성됩니다. 기본값은 거짓입니다.

- `spring.sleuth.web.skip-pattern`: 추적하지 않아야 하는 요청을 결정하는 데 사용되는 정규식입니다. 기본값은 `/건강`입니다.

이러한 속성에 대한 자세한 내용은 [Spring Boot 설명서](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-tracing.html# boot-features- 추적-스프링-슬루스).

## 추적 정보 수집

Spring Boot 추적 시스템을 사용하여 요청 처리에 대한 정보를 수집할 수 있습니다. 이 정보는 두 가지 방법으로 수집할 수 있습니다.

- 정보를 파일에 기록하여
- [집킨](https://zipkin.io/) 서버로 정보 전송

### 추적 정보를 파일에 기록

추적 정보를 파일에 기록하도록 Spring Boot 추적 시스템을 구성할 수 있습니다. 이는 `application.properties` 파일에서 `spring.sleuth.log.file` 속성을 설정하여 수행할 수 있습니다. 다음은 정보를 파일에 기록하도록 추적 시스템을 구성하는 방법의 예입니다.

```
spring.sleuth.log.file=traces.log
```

### Zipkin 서버에 추적 정보 보내기

추적 정보를 Zipkin 서버로 보내도록 Spring Boot 추적 시스템을 구성할 수 있습니다. 이는 `application.properties` 파일에서 `spring.sleuth.zipkin.baseUrl` 속성을 설정하여 수행할 수 있습니다. 다음은 Zipkin 서버에 정보를 보내도록 추적 시스템을 구성하는 방법의 예입니다.

```
spring.sleuth.zipkin.baseUrl=http://localhost:9411
```

## 추적 정보 보기

### 추적 정보를 파일에 기록

추적 시스템이 정보를 파일에 기록하도록 구성된 경우 텍스트 편집기에서 파일을 열어 정보를 볼 수 있습니다. 정보는 [JSON](https://www.json.org/) 형식으로 기록됩니다.

### Zipkin 서버에 추적 정보 보내기

추적 시스템이 Zipkin 서버로 정보를 보내도록 구성된 경우 웹 브라우저에서 Zipkin 서버를 열면 정보를 볼 수 있습니다. Zipkin 서버는 추적 정보를 볼 수 있는 그래픽 인터페이스를 제공합니다.

## 결론

이 게시물에서는 Spring Boot 추적 시스템을 구성하는 방법과 이를 사용하여 요청 처리에 대한 정보를 수집하는 방법을 살펴보았습니다. 또한 시스템에서 수집한 추적 정보를 보는 방법도 살펴보았습니다.