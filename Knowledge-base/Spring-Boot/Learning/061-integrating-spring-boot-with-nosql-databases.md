---
title: 061: NoSQL 데이터베이스와 Spring Boot 통합
description: 
published: true
date: 2023-02-05T00:32:21.285Z
tags: 
editor: markdown
dateCreated: 2023-02-05T00:32:19.638Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [061: Integrating Spring Boot with NoSQL Databases***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/061-integrating-spring-boot-with-nosql-databases)
{.links-list}


# 061: NoSQL 데이터베이스와 Spring Boot 통합

이 게시물에서는 Spring Boot 애플리케이션을 NoSQL 데이터베이스와 통합하는 방법을 알아봅니다.

## NoSQL이란?

NoSQL은 비관계형 데이터베이스를 설명하는 데 사용되는 용어입니다. NoSQL 데이터베이스는 대부분의 관계형 데이터베이스에서 사용하는 전통적인 테이블 기반 관계형 모델을 사용하지 않는 데이터베이스입니다.

NoSQL 데이터베이스는 종종 관계형 데이터베이스보다 확장성이 뛰어나고 작업하기 쉽습니다. 또한 기존의 테이블 기반 스키마로 쉽게 구조화되지 않는 대량의 데이터를 저장하는 데 적합합니다.

## Spring Boot에서 NoSQL을 사용하는 이유는 무엇입니까?

NoSQL 데이터베이스는 많은 Spring Boot 애플리케이션에 적합한 선택입니다. 그들은 종종 관계형 데이터베이스보다 더 확장 가능하고 작업하기 쉽습니다. Spring Boot는 NoSQL 데이터베이스에 대한 우수한 지원을 제공하므로 애플리케이션에서 쉽게 작업할 수 있습니다.

## NoSQL을 Spring Boot와 통합하는 방법

 Spring Boot는 NoSQL 데이터베이스를 잘 지원합니다. Spring Boot에서 널리 사용되는 NoSQL 데이터베이스를 사용할 수 있습니다. 이 게시물에서는 MongoDB를 NoSQL 데이터베이스로 사용합니다.

MongoDB는 Spring Boot와 함께 사용하기 쉬운 널리 사용되는 NoSQL 데이터베이스입니다. Spring Boot는 애플리케이션에서 MongoDB를 쉽게 사용할 수 있도록 하는 MongoDB용 스타터 모듈을 제공합니다.

Spring Boot에서 MongoDB를 사용하려면 프로젝트에 spring-boot-starter-data-mongodb 스타터 모듈을 추가해야 합니다. 다음 Maven 종속성을 사용하여 이 모듈을 프로젝트에 추가할 수 있습니다.

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

또한 애플리케이션으로 MongoDB를 구성해야 합니다. 애플리케이션에 MongoDB 구성 파일을 추가하여 이를 수행할 수 있습니다. 다음은 기본 MongoDB 구성 파일입니다.

```properties
spring.data.mongodb.uri=mongodb://localhost/test
```

이 구성 파일은 기본 포트(27017)의 localhost에서 MongoDB 데이터베이스에 연결하도록 Spring Boot에 지시합니다. 데이터베이스 이름은 테스트입니다.

## 요약

이 게시물에서는 Spring Boot 애플리케이션을 NoSQL 데이터베이스와 통합하는 방법을 배웠습니다. 또한 Spring Boot에서 NoSQL 데이터베이스를 사용하려는 이유와 Spring Boot에서 MongoDB를 구성하는 방법도 배웠습니다.