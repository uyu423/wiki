---
title: Spring Boot CLI의 이점
description: 
published: true
date: 2023-02-17T18:02:36.821Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:32:22.146Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [The Benefits of Spring Boot CLI***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-benefits-of-spring-boot-cli)
{.links-list}


# Spring Boot CLI의 이점

Spring Boot 명령줄 인터페이스(CLI)는 Spring 기반 애플리케이션을 빠르게 만들고 실행하는 데 사용할 수 있는 강력한 도구입니다. 또한 Spring을 학습하고 새로운 아이디어를 프로토타이핑하기 위한 훌륭한 도구입니다. 이 기사에서는 Spring Boot CLI를 사용할 때의 몇 가지 이점을 살펴보겠습니다.

## 1. 빠르고 쉽게 Spring 기반 애플리케이션 생성

Spring Boot CLI를 사용하는 가장 큰 이점 중 하나는 Spring 기반 애플리케이션을 빠르고 쉽게 만들 수 있다는 것입니다. 별도의 Spring 도구 제품군을 설치하고 구성할 필요가 없습니다. JDK(Java Development Kit)와 Spring Boot CLI만 있으면 됩니다.

JDK 및 Spring Boot CLI가 설치되면 다음 명령을 실행하여 새 Spring Boot 애플리케이션을 생성할 수 있습니다.

```
$ spring boot my-app
```

이렇게 하면 Spring Boot 애플리케이션의 기본 구조로 `my-app`이라는 새 디렉토리가 생성됩니다. 그런 다음 이 디렉터리로 이동하고 다음 명령을 사용하여 애플리케이션을 실행할 수 있습니다.

```
$ cd my-app
$ ./mvnw spring-boot:run
```

Spring Boot CLI를 사용하면 몇 가지 명령만으로 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다.

## 2. 스프링 애플리케이션 실행

Spring 기반 애플리케이션을 만드는 것 외에도 Spring Boot CLI를 사용하여 Spring 애플리케이션을 실행할 수도 있습니다. 이는 테스트 및 디버깅 목적에 특히 유용합니다. 예를 들어 다음 명령을 사용하여 디버그 모드에서 Spring 애플리케이션을 실행할 수 있습니다.

```
$ spring boot --debug my-app
```

Spring Boot CLI를 사용하여 프로덕션 환경에서 Spring 애플리케이션을 실행할 수도 있습니다. 이는 애플리케이션을 실행할 때 `--prod` 플래그를 사용하여 수행할 수 있습니다.

```
$ spring boot --prod my-app
```

## 3. 봄 배우기

Spring Boot CLI는 Spring 학습을 위한 훌륭한 도구이기도 합니다. 다양한 Spring 기능에 대한 정보를 얻기 위해 `spring` 명령을 사용할 수 있습니다. 예를 들어 다음 명령을 사용하여 Bean 정의 Dsl에 대한 정보를 얻을 수 있습니다.

```
$ spring bean-dsl
```

`spring help` 명령을 사용하여 사용 가능한 모든 명령 목록을 얻을 수도 있습니다.

```
$ spring help
```

## 4. 새로운 아이디어 프로토타입 만들기

Spring Boot CLI의 또 다른 큰 이점은 새로운 아이디어의 프로토타입을 신속하게 만드는 데 사용할 수 있다는 것입니다. 예를 들어 새로운 Spring 기능을 시험해보고 싶다면 Spring Boot CLI를 사용하여 별도의 Spring 도구 모음을 설치 및 구성하지 않고도 새로운 애플리케이션을 생성하고 테스트할 수 있습니다.

결론

Spring Boot CLI는 Spring 기반 애플리케이션을 빠르게 만들고 실행하는 데 사용할 수 있는 강력한 도구입니다. 또한 Spring을 학습하고 새로운 아이디어를 프로토타이핑하기 위한 훌륭한 도구입니다.