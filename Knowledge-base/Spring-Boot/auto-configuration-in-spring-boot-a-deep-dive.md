---
title: Spring Boot의 자동 구성: 심층 분석
description: 
published: true
date: 2023-01-30T08:32:29.759Z
tags: 
editor: markdown
dateCreated: 2023-01-30T08:32:29.759Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Auto-configuration in Spring Boot: A Deep Dive***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/auto-configuration-in-spring-boot-a-deep-dive)
{.links-list}




자동 구성은 클래스 경로에 있는 종속성을 기반으로 Spring 애플리케이션을 자동으로 구성하는 Spring Boot의 기능입니다. 예를 들어 클래스 경로에 spring-boot-starter-data-jpa 종속성을 포함하면 Spring Boot는 자동으로 JpaTransactionManager 및 spring-data-jpa를 구성합니다. 이렇게 하면 애플리케이션에 대해 Spring을 구성할 때 많은 시간과 노력을 절약할 수 있습니다.

이 기사에서는 Spring Boot의 자동 구성에 대해 자세히 살펴보겠습니다. 먼저 자동 구성이 작동하는 방식을 살펴본 다음 가장 일반적인 자동 구성 모듈 중 일부를 살펴보겠습니다.

자동 구성 작동 방식

Spring Boot의 자동 구성은 기본적으로 활성화되어 있습니다. 클래스 경로에 Spring Boot 스타터 종속성을 포함하면 Spring Boot가 자동으로 스타터를 구성합니다. 예를 들어 spring-boot-starter-data-jpa 종속성을 포함하면 Spring Boot는 JpaTransactionManager 및 spring-data-jpa를 자동으로 구성합니다.

Spring Boot는 자동 구성에 2단계 접근 방식을 사용합니다. 첫 번째 단계에서는 모든 자동 구성 클래스가 로드되고 처리됩니다. 두 번째 단계에서는 애플리케이션 컨텍스트에 자동 구성이 적용됩니다.

첫 번째 단계는 일반적으로 Spring 환경에 자동 구성 옵션을 등록하는 데 사용됩니다. 두 번째 단계는 실제 자동 구성이 애플리케이션 컨텍스트에 적용되는 단계입니다.

자동 구성의 첫 번째 단계는 SpringApplication 클래스가 초기화될 때 트리거됩니다. 애플리케이션 컨텍스트가 새로 고쳐지면 자동 구성의 두 번째 단계가 트리거됩니다.

자동 구성은 spring.boot.autoconfigure 속성에 의해 제어됩니다. 이 속성은 자동 구성을 활성화하거나 비활성화하는 데 사용됩니다. 또한 특정 자동 구성 모듈을 활성화 또는 비활성화하는 데 사용됩니다.

spring.boot.autoconfigure.exclude 속성을 사용하여 특정 자동 구성 모듈을 제외할 수 있습니다. 예를 들어 데이터 소스 자동 구성 모듈을 제외하려면 spring.boot.autoconfigure.exclude 속성을 spring.boot.autoconfigure.data.DataSourceAutoConfiguration 으로 설정합니다.

spring.boot.autoconfigure.include 속성은 특정 자동 구성 모듈을 포함하는 데 사용할 수 있습니다. 이는 기본적으로 활성화되지 않은 자동 구성 모듈을 포함하려는 경우에 유용합니다.

공통 자동 구성 모듈

Spring Boot는 광범위한 자동 구성 모듈을 제공합니다. 이 섹션에서는 가장 일반적으로 사용되는 자동 구성 모듈 중 일부를 살펴보겠습니다.

데이터 소스 자동 구성

데이터 소스 자동 구성 모듈은 애플리케이션의 데이터 소스를 구성하는 데 사용됩니다. Spring Boot는 클래스 경로에서 데이터 소스 드라이버를 찾으면 자동으로 데이터 소스를 구성합니다.

특정 데이터 소스를 사용하려면 spring.datasource.url , spring.datasource.username 및 spring.datasource.password 속성을 설정할 수 있습니다. 그런 다음 Spring Boot는 이러한 속성을 사용하여 데이터 소스를 구성합니다.

연결 풀을 사용하려면 spring.datasource.type 속성을 org.apache.commons.dbcp.BasicDataSource 로 설정할 수 있습니다. 그러면 Spring Boot가 BasicDataSource를 구성합니다.

JPA 자동 구성

JPA 자동 구성 모듈은 애플리케이션에 맞게 JPA를 구성하는 데 사용됩니다. Spring Boot는 클래스 경로에서 JPA 구현을 찾으면 자동으로 JpaTransactionManager 및 spring-data-jpa를 구성합니다.

특정 JPA 구현을 사용하려는 경우 spring.jpa.database 속성을 설정할 수 있습니다. 그런 다음 Spring Boot는 이 속성을 사용하여 JpaTransactionManager 및 spring-data-jpa를 구성합니다.

특정 EntityManagerFactory를 사용하려면 spring.jpa.entitymanagerfactory.id 속성을 설정할 수 있습니다. 그런 다음 Spring Boot는 이 속성을 사용하여 JpaTransactionManager를 구성합니다.

몽고 자동 구성

Mongo 자동 구성 모듈은 애플리케이션에 맞게 Mongo를 구성하는 데 사용됩니다. Spring Boot는 클래스 경로에서 Mongo 드라이버를 찾으면 자동으로 MongoTemplate을 구성합니다.

특정 Mongo 인스턴스를 사용하려는 경우 spring.data.mongodb.host , spring.data.mongodb.port 및 spring.data.mongodb.database 속성을 설정할 수 있습니다. 그런 다음 Spring Boot는 이러한 속성을 사용하여 MongoTemplate을 구성합니다.

연결 풀을 사용하려면 spring.data.mongodb.type 속성을 com.mongodb.MongoClient 로 설정할 수 있습니다. 그러면 Spring Boot가 MongoClient를 구성합니다.