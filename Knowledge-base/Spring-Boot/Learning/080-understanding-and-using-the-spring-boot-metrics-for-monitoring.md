---
title: 080: 모니터링을 위한 Spring Boot 메트릭 이해 및 사용
description: 
published: true
date: 2023-02-05T11:32:25.195Z
tags: 
editor: markdown
dateCreated: 2023-02-05T11:32:19.622Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [080: Understanding and Using the Spring Boot Metrics for Monitoring***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/080-understanding-and-using-the-spring-boot-metrics-for-monitoring)
{.links-list}


# 소개

모니터링은 모든 소프트웨어 개발 프로세스의 중요한 부분입니다. 이를 통해 개발자는 프로덕션 환경에서 애플리케이션의 문제를 식별하고 진단할 수 있습니다.

Spring Boot는 애플리케이션 모니터링을 위한 다양한 내장 메트릭을 제공합니다. 이 게시물에서는 Spring Boot 메트릭이 무엇이고 애플리케이션 모니터링에 이를 사용하는 방법을 살펴보겠습니다.

# Spring Boot Metrics란?

Spring Boot 메트릭은 Spring 기반 애플리케이션을 모니터링하기 위한 도구 세트입니다. 애플리케이션의 런타임 동작에 대한 통찰력을 제공하고 성능 병목 현상을 식별하는 데 사용할 수 있습니다.

Spring Boot 메트릭은 Prometheus, Graphite 및 StatsD와 같은 다양한 모니터링 도구와 함께 사용하도록 설계되었습니다.

# Spring Boot Metrics 사용 방법

Spring Boot는 메트릭을 구성하고 사용하는 다양한 방법을 제공합니다. 이 섹션에서는 가장 중요한 몇 가지 구성 옵션을 살펴보겠습니다.

## 메트릭 활성화

메트릭은 Spring Boot에서 기본적으로 비활성화되어 있습니다. 메트릭을 활성화하려면 애플리케이션의 `application.properties` 파일에 다음 속성을 추가해야 합니다.

```
spring.metrics.enable=true
```

## 메트릭 구성

Spring Boot를 사용하면 메트릭 시스템의 여러 측면을 구성할 수 있습니다. 예를 들어 기본 레지스트리, 메트릭 이름 접두사 및 내보내기 형식을 구성할 수 있습니다.

다음 속성을 사용하여 기본 레지스트리를 구성할 수 있습니다.

```
spring.metrics.default-registry=my-registry
```

다음 속성을 사용하여 메트릭 이름 접두사를 구성할 수 있습니다.

```
spring.metrics.prefix=my-prefix
```

다음 속성을 사용하여 내보내기 형식을 구성할 수 있습니다.

```
spring.metrics.export.format=json
```

## 메트릭 내보내기

Spring Boot는 메트릭을 내보내는 다양한 방법을 지원합니다. 가장 일반적인 방법은 `/metrics` 엔드포인트를 사용하는 것입니다. 이 엔드포인트는 기본적으로 Prometheus 형식으로 메트릭을 노출합니다.

`/metrics/{name}` 엔드포인트를 사용하여 단일 메트릭을 내보낼 수도 있습니다. 예를 들어 다음 엔드포인트는 `jvm.memory.used` 메트릭을 내보냅니다.

```
/metrics/jvm.memory.used
```

# 결론

이 게시물에서는 Spring Boot 메트릭과 이를 애플리케이션 모니터링에 사용하는 방법을 살펴보았습니다. 또한 메트릭을 활성화하고 구성하는 방법과 모니터링 도구와 함께 사용하기 위해 메트릭을 내보내는 방법도 살펴보았습니다.