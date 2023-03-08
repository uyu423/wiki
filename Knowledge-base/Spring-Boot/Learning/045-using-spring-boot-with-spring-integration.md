---
title: 045: Spring 통합과 함께 Spring Boot 사용
description: 
published: true
date: 2023-02-04T11:32:16.989Z
tags: 
editor: markdown
dateCreated: 2023-02-04T11:32:15.439Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [045: Using Spring Boot with Spring Integration***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/045-using-spring-boot-with-spring-integration)
{.links-list}


# Spring 통합과 함께 Spring Boot 사용

이번 포스트에서는 Spring Integration과 함께 Spring Boot를 사용하는 방법에 대해 알아보겠습니다. Spring Integration의 기본 사항을 살펴보고 Spring Boot와 함께 사용하는 방법을 보여줍니다.

## 스프링 통합이란?

Spring Integration은 Spring Framework를 확장하여 엔터프라이즈 통합 패턴을 지원하는 프레임워크입니다. 이러한 패턴은 서로 다른 애플리케이션과 시스템 간의 통신을 용이하게 하는 데 사용됩니다.

Spring Integration은 JMS, HTTP 및 FTP와 같은 다양한 기술에 대한 어댑터를 제공합니다. 또한 메시지 채널, 메시지 라우터 및 메시지 변환기에 대한 지원도 제공합니다.

## 스프링 통합을 사용하는 이유는 무엇입니까?

Spring Integration을 사용하면 탄력적이고 확장 가능한 엔터프라이즈급 애플리케이션을 구축할 수 있습니다. 다양한 기술에서 일관된 프로그래밍 모델을 제공하여 공급업체 종속을 방지하는 데 도움이 됩니다.

## 시작하기

이 섹션에서는 Spring 통합을 시작하는 방법을 보여줍니다. 필요한 다양한 종속성을 살펴보고 Spring 통합을 구성하는 방법을 보여줍니다.

### 종속성

먼저 프로젝트에 다음 종속 항목을 추가해야 합니다.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-integration</artifactId>
    </dependency>
</dependencies>
```

이러한 종속성은 Spring 통합에 필요한 jar를 가져옵니다.

### 구성

다음으로 Spring 통합을 구성해야 합니다. `application.properties` 파일에 다음을 추가하면 됩니다.

```properties
spring.integration.dsl.enabled=true
```

그러면 Spring Integration Java DSL이 활성화됩니다.

## 결론

이번 포스트에서는 Spring Integration과 함께 Spring Boot를 사용하는 방법에 대해 알아보았습니다. 지금까지 Spring 통합의 기본 사항을 살펴보고 이를 시작하는 방법을 보여 주었습니다.