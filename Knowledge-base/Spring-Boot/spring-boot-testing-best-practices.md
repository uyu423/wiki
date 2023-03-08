---
title: 스프링 부트 테스트 모범 사례
description: 
published: true
date: 2023-02-07T08:32:42.584Z
tags: 
editor: markdown
dateCreated: 2023-02-07T08:32:40.827Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Testing Best Practices***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-testing-best-practices)
{.links-list}


# 스프링 부트 테스트 모범 사례

Spring Boot 애플리케이션을 개발하고 테스트하는 것은 어려울 수 있습니다. 이 기사에서는 Spring Boot 애플리케이션을 테스트하기 위한 몇 가지 모범 사례를 살펴보겠습니다.

## 단위 테스트

단위 테스트는 모든 애플리케이션에서 가장 중요한 테스트입니다. 빠르고 안정적이며 작성 및 유지 관리가 쉬워야 합니다.

 Spring Boot는 다음과 같이 단위 테스트를 더 쉽게 만들 수 있는 여러 기능을 제공합니다.

* `@DataJpaTest` 주석은 JPA 저장소를 테스트하는 데 사용할 수 있습니다. 이 주석은 메모리 내 데이터베이스를 구성하고 Spring Data 및 JPA를 초기화하며 전체 자동 구성을 비활성화합니다.

* `@WebMvcTest` 주석은 Spring MVC 컨트롤러를 테스트하는 데 사용할 수 있습니다. 이 주석은 메모리 내 웹 서버를 구성하고 Spring MVC를 초기화하며 전체 자동 구성을 비활성화합니다.

* `@MockBean` 어노테이션을 사용하여 Spring 애플리케이션 컨텍스트에 모의 빈을 주입할 수 있습니다. 이것은 아직 사용할 수 없거나 아직 완전히 구현되지 않은 종속성을 조롱하는 데 유용합니다.

* `@TestPropertySource` 주석은 테스트에서 사용할 속성을 구성하는 데 사용할 수 있습니다. 이는 아직 사용할 수 없거나 아직 완전히 구현되지 않은 속성을 설정하는 데 유용합니다.

### JUnit 규칙

JUnit 규칙을 사용하여 단위 테스트를 단순화할 수 있습니다. 예를 들어 `@SpringBootTest` 규칙을 사용하여 Spring ApplicationContext를 로드할 수 있습니다. `@TestPropertySource` 규칙은 테스트 속성 파일에서 속성을 로드하는 데 사용할 수 있습니다. `@TempDir` 규칙은 테스트가 완료된 후 삭제될 임시 디렉토리를 만드는 데 사용할 수 있습니다.

### 주장J

AssertJ는 더 읽기 쉽고 간결한 단위 테스트를 작성하는 데 사용할 수 있는 강력한 어설션 라이브러리입니다.

## 통합 테스팅

통합 테스트는 응용 프로그램의 서로 다른 구성 요소 간의 상호 작용을 테스트하는 데 사용됩니다. 통합 테스트는 일반적으로 단위 테스트보다 느리고 작성 및 유지 관리가 더 어렵습니다.

Spring Boot는 다음과 같이 통합 테스트를 보다 쉽게 수행할 수 있는 여러 기능을 제공합니다.

* `@SpringBootTest` 주석을 사용하여 Spring ApplicationContext를 로드할 수 있습니다.

* `@Autowired` 주석은 테스트 클래스에 종속성을 주입하는 데 사용할 수 있습니다.

* `@MockBean` 어노테이션을 사용하여 Spring 애플리케이션 컨텍스트에 모의 빈을 주입할 수 있습니다. 이것은 아직 사용할 수 없거나 아직 완전히 구현되지 않은 종속성을 조롱하는 데 유용합니다.

* `@TestPropertySource` 주석은 테스트에서 사용할 속성을 구성하는 데 사용할 수 있습니다. 이는 아직 사용할 수 없거나 아직 완전히 구현되지 않은 속성을 설정하는 데 유용합니다.

### 스프링 레스트 템플릿

Spring RestTemplate은 Spring Boot 애플리케이션에 대한 HTTP 요청을 만드는 데 사용할 수 있습니다. RestTemplate은 HttpMessageConverter를 사용하여 응답 본문을 원하는 유형으로 자동 변환하도록 구성할 수 있습니다.

### 주장J

AssertJ는 더 읽기 쉽고 간결한 통합 테스트를 작성하는 데 사용할 수 있는 강력한 어설션 라이브러리입니다.

## 종단 간 테스트

종단 간 테스트는 사용자 관점에서 응용 프로그램을 테스트하는 데 사용됩니다. 종단 간 테스트는 일반적으로 느리고 작성 및 유지 관리가 더 어렵습니다.

Spring Boot는 다음과 같이 종단 간 테스트를 더 쉽게 만들 수 있는 여러 기능을 제공합니다.

* `@SpringBootTest` 주석을 사용하여 Spring ApplicationContext를 로드할 수 있습니다.

* `@Autowired` 주석은 테스트 클래스에 종속성을 주입하는 데 사용할 수 있습니다.

* `@MockBean` 어노테이션을 사용하여 Spring 애플리케이션 컨텍스트에 모의 빈을 주입할 수 있습니다. 이것은 아직 사용할 수 없거나 아직 완전히 구현되지 않은 종속성을 조롱하는 데 유용합니다.

* `@TestPropertySource` 주석은 테스트에서 사용할 속성을 구성하는 데 사용할 수 있습니다. 이는 아직 사용할 수 없거나 아직 완전히 구현되지 않은 속성을 설정하는 데 유용합니다.

### 스프링 레스트 템플릿

Spring RestTemplate은 Spring Boot 애플리케이션에 대한 HTTP 요청을 만드는 데 사용할 수 있습니다. RestTemplate은 HttpMessageConverter를 사용하여 응답 본문을 원하는 유형으로 자동 변환하도록 구성할 수 있습니다.

### 주장J

AssertJ는 보다 읽기 쉽고 간결한 종단 간 테스트를 작성하는 데 사용할 수 있는 강력한 어설션 라이브러리입니다.

## 외부 리소스

* [Spring Boot의 단위 테스트](https://spring.io/blog/2009/12/08/testing-in-spring-boot-apps/)
* [Spring Boot에서 통합 테스트](https://spring.io/blog/2014/05/07/spring-boot-java-config-integration-testing/)
* [Spring Boot의 End-to-End 테스트](https://spring.io/blog/2016/04/15/testing-improvements-in-spring-boot-1-4/)