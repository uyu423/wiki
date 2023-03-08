---
title: 089: 구성 관리를 위한 Spring Boot 프로필 이해 및 사용
description: 
published: true
date: 2023-02-05T19:32:21.708Z
tags: 
editor: markdown
dateCreated: 2023-02-05T19:32:16.248Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [089: Understanding and Using the Spring Boot Profiles for Configuration Management***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/089-understanding-and-using-the-spring-boot-profiles-for-configuration-management)
{.links-list}


# 089: 구성 관리를 위한 Spring Boot 프로필 이해 및 사용

Spring Boot는 애플리케이션 구성을 관리하기 위한 강력하고 유연한 메커니즘을 제공합니다. Spring Boot 프로필 기능을 사용하면 개발, 프로덕션 또는 테스트와 같은 다양한 환경에 맞게 애플리케이션을 구성할 수 있습니다.

이 게시물에서는 Spring Boot 프로필이 무엇이며 애플리케이션 구성을 관리하는 데 어떻게 사용할 수 있는지 살펴보겠습니다. 또한 Spring Boot 프로필을 사용하기 위한 몇 가지 모범 사례를 살펴보겠습니다.

## 스프링 부트 프로필이 무엇인가요?

Spring Boot Profile은 다양한 환경에 맞게 애플리케이션을 구성하는 방법입니다. 예를 들어 개발 프로필과 프로덕션 프로필이 있을 수 있습니다. 각 프로파일은 고유한 구성 설정을 가질 수 있습니다.

애플리케이션을 특정 환경에 배포할 때 적절한 프로필을 활성화할 수 있습니다. 이렇게 하면 해당 환경에 대한 구성 설정만 사용됩니다.

## 스프링 부트 프로필 사용 방법

Spring Boot Profile은 `spring.profiles.active` 속성을 사용하여 활성화됩니다. 이 속성은 다음과 같은 다양한 방법으로 설정할 수 있습니다.

* `application.properties` 또는 `application.yml` 파일에서
* 시스템 속성으로
* 환경변수로

예를 들어 `production` 프로필을 활성화하려면 `application.properties` 파일에 다음을 추가할 수 있습니다.

```
spring.profiles.active=production
```

또는 애플리케이션을 시작할 때 `spring.profiles.active` 시스템 속성을 설정할 수 있습니다.

```
java -jar myapp.jar --spring.profiles.active=production
```

## Spring Boot 프로필 사용을 위한 모범 사례

다음은 Spring Boot 프로필을 사용하기 위한 몇 가지 모범 사례입니다.

* 개발, 프로덕션, 테스트 등 환경별로 별도의 프로필을 사용하세요.
* 구성 파일을 작고 집중적으로 유지하십시오. 모든 구성 설정을 하나의 파일에 넣지 마십시오.
* 구성 파일에서 자리 표시자(`${placeholder}`)를 사용하십시오. 이렇게 하면 여러 프로필에서 구성 설정을 재사용할 수 있습니다.
* 프로필별 구성 파일을 사용합니다. 예를 들어 프로덕션 프로필에 대한 `application-production.properties` 파일이 있을 수 있습니다.
*`@Profile` 주석을 사용하여 빈을 조건부로 활성화하십시오. 특정 프로필에 필요한 빈만 로드하는 데 사용할 수 있습니다.

## 결론

이 게시물에서는 Spring Boot 프로필이 무엇이며 애플리케이션 구성을 관리하는 데 어떻게 사용할 수 있는지 살펴보았습니다. Spring Boot Profiles 사용에 대한 몇 가지 모범 사례도 살펴보았습니다.

Spring Boot에 대해 자세히 알아보려면 다음 리소스를 확인하세요.

* [Spring Boot 참조 가이드](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
* [Spring Boot 샘플](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples)
* [Spring Boot Starters](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-starters)