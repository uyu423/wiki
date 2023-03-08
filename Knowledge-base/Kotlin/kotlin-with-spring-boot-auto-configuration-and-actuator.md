---
title: Spring Boot를 사용한 Kotlin: 자동 구성 및 액추에이터
description: 
published: true
date: 2023-02-02T18:23:16.583Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:23:15.014Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin with Spring Boot: Auto-configuration and Actuator***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-with-spring-boot-auto-configuration-and-actuator)
{.links-list}


# Spring Boot를 사용한 Kotlin: 자동 구성 및 액추에이터

Kotlin은 JVM에서 실행되고 Android 앱을 개발하는 데 사용할 수 있는 정적으로 유형이 지정된 프로그래밍 언어입니다. Spring Boot는 "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 쉽게 만들 수 있는 프레임워크입니다.

Kotlin with Spring Boot 프로젝트는 Kotlin 및 Spring Boot 애플리케이션에 대한 자동 구성 및 액추에이터 지원을 제공합니다.

## 자동 구성

자동 구성은 클래스 경로에 있는 종속성을 기반으로 Spring 애플리케이션을 자동으로 구성하는 Spring Boot의 기능입니다. 예를 들어 클래스 경로에 spring-boot-starter-data-jpa 종속성을 포함하면 Spring Boot가 자동으로 DataSource 및 JPA EntityManagerFactory를 구성합니다.

Kotlin with Spring Boot 프로젝트는 Kotlin 및 Spring Boot 애플리케이션을 위한 자동 구성을 제공합니다. 즉, 예를 들어 클래스 경로에 spring-boot-starter-data-jpa 종속성을 포함하면 Spring Boot를 사용하는 Kotlin이 자동으로 DataSource 및 JPA EntityManagerFactory를 구성합니다.

Spring Boot 자동 구성과 함께 Kotlin을 사용하려면 클래스 경로에 kotlin-spring-boot-autoconfigure 모듈을 추가해야 합니다.

## 액추에이터

Actuator는 애플리케이션을 모니터링하고 관리할 수 있는 Spring Boot 기능입니다. 예를 들어 Actuator는 애플리케이션의 상태를 모니터링하는 데 사용할 수 있는 HTTP 엔드포인트를 제공합니다.

Kotlin with Spring Boot 프로젝트는 Kotlin 및 Spring Boot 애플리케이션을 위한 Actuator 지원을 제공합니다. 예를 들어 Actuator를 사용하여 Kotlin 및 Spring Boot 애플리케이션의 상태를 모니터링할 수 있습니다.

Spring Boot Actuator와 함께 Kotlin을 사용하려면 클래스 경로에 kotlin-spring-boot-actuator 모듈을 추가해야 합니다.

## 시작하기

Kotlin 및 Spring Boot를 시작하려면 Spring Initializr를 사용하여 필요한 종속성이 있는 프로젝트를 생성할 수 있습니다. 예를 들어 kotlin-spring-boot-autoconfigure 및 kotlin-spring-boot-actuator 종속성이 있는 프로젝트를 생성하려면 다음을 수행합니다.

1. https://start.spring.io/로 이동합니다.
2. 언어 드롭다운에서 Kotlin을 선택합니다.
3. 부트 버전 드롭다운에서 Spring Boot 2.0.0을 선택합니다.
4. 아티팩트 필드에 kotlin-spring-boot-example을 입력합니다.
5. kotlin-spring-boot-autoconfigure 및 kotlin-spring-boot-actuator 종속성을 선택합니다.
6. 프로젝트 생성을 클릭합니다.

그런 다음 생성된 프로젝트를 선호하는 IDE로 가져오고 코딩을 시작할 수 있습니다!

## 결론

이 기사에서는 Kotlin 및 Spring Boot 애플리케이션에 대한 자동 구성 및 Actuator 지원을 제공하는 Kotlin with Spring Boot 프로젝트를 살펴보았습니다. 또한 필요한 종속성이 있는 프로젝트를 생성하기 위해 Spring Initializr를 사용하여 Kotlin 및 Spring Boot를 시작하는 방법도 살펴보았습니다.