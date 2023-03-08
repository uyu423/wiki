---
title: 스프링 부트 액추에이터 끝점
description: 
published: true
date: 2023-02-07T06:32:15.462Z
tags: 
editor: markdown
dateCreated: 2023-02-07T06:32:13.915Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Actuator Endpoints***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-actuator-endpoints)
{.links-list}


# 스프링 부트 액추에이터 엔드포인트

Spring Boot Actuator Endpoints를 사용하면 Spring Boot 애플리케이션을 모니터링하고 관리할 수 있습니다. 이 기사에서는 이러한 엔드포인트가 무엇이고 어떻게 사용할 수 있는지 살펴보겠습니다.

## 액추에이터 끝점이란 무엇입니까?

액추에이터 엔드포인트는 애플리케이션을 모니터링하고 관리하는 데 사용할 수 있는 Spring Boot 애플리케이션에 의해 노출되는 URL입니다. 이러한 엔드포인트는 애플리케이션 상태, 애플리케이션 버전 등과 같은 애플리케이션에 대한 정보를 제공합니다.

## 끝점

Spring Boot에서 사용할 수 있는 여러 액추에이터 엔드포인트가 있습니다. 이러한 끝점 중 일부는 다음과 같습니다.

### /정보

이 엔드포인트는 애플리케이션에 대한 정보를 제공합니다. 이 정보는 `application.properties` 파일에서 구성됩니다.

### /건강

이 엔드포인트는 애플리케이션의 상태에 대한 정보를 제공합니다. 이 정보는 애플리케이션에 등록된 HealthIndicator 빈에 의해 수집됩니다.

### /측정항목

이 엔드포인트는 애플리케이션의 메트릭에 대한 정보를 제공합니다. 이 정보는 애플리케이션에 등록된 Metrics Bean에 의해 수집됩니다.

### /추적하다

이 엔드포인트는 애플리케이션 추적에 대한 정보를 제공합니다. 이 정보는 애플리케이션에 등록된 TraceRepository 빈에 의해 수집됩니다.

## 액추에이터 엔드포인트 활성화

액추에이터 끝점은 Spring Boot에서 기본적으로 활성화되지 않습니다. 프로젝트에 `spring-boot-actuator` 종속성을 추가하여 활성화할 수 있습니다.

## 보안

프로젝트에 Spring Security를 추가하여 액추에이터 엔드포인트를 보호할 수 있습니다. 프로젝트에 `spring-boot-starter-security` 종속성을 추가하여 이를 수행할 수 있습니다.

## 결론

이 기사에서는 Spring Boot Actuator Endpoints가 무엇이고 어떻게 사용할 수 있는지 살펴보았습니다. 또한 이러한 엔드포인트를 활성화하고 보호하는 방법도 살펴보았습니다.