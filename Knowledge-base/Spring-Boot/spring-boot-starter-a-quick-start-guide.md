---
title: Spring Boot Starter: 빠른 시작 가이드
description: 
published: true
date: 2023-02-17T18:02:34.069Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:31:10.378Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Spring Boot Starter: A Quick Start Guide***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-starter-a-quick-start-guide)
{.links-list}


# Spring Boot Starter: 빠른 시작 가이드

[Spring Framework](https://spring.io/projects/spring-framework)의 인기가 계속 높아지면서 [Spring Boot](https://spring.io/projects/spring-framework)가 boot) 프로젝트도 인기가 상승했습니다. Spring Boot를 사용하면 "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다.

이 문서에서는 [Spring Boot 스타터](https://docs.spring.io/spring-boot/docs/current/reference/html/using-boot-build-systems)에 대한 빠른 시작 가이드를 제공합니다. html#using-boot-starter). 스타터가 Maven 또는 Gradle 구성을 단순화하는 방법을 보여드리겠습니다. 또한 사용할 수 있는 일반적인 스타터의 몇 가지 예를 제공합니다. 이 기사를 마칠 때쯤이면 스타터가 무엇인지, 자신의 애플리케이션에서 스타터를 어떻게 사용할 수 있는지 잘 이해하게 될 것입니다.

## 스타터란?

스타터는 특정 작업을 완료하는 데 필요한 모든 종속성을 포함하는 템플릿입니다. 예를 들어 웹 애플리케이션을 빌드하려는 경우 `web` 스타터를 사용할 수 있습니다. 이 스타터에는 웹 서버, 템플릿 엔진 등과 같은 웹 애플리케이션에 필요한 모든 종속성이 포함됩니다.

스타터는 종속성을 수동으로 관리할 필요가 없도록 설계되었습니다. 스타터를 사용하면 애플리케이션에 스타터를 포함하기만 하면 종속성이 자동으로 관리됩니다.

## Maven 및 Gradle 구성

Maven을 사용하는 경우 `pom.xml` 파일에 다음 종속성을 추가하여 스타터를 사용할 수 있습니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
</dependency>
```

Gradle을 사용하는 경우 `build.gradle` 파일에 다음 종속성을 추가하여 스타터를 사용할 수 있습니다.

```groovy
dependencies {
    compile group: 'org.springframework.boot', name: 'spring-boot-starter'
}
```

## 웹 스타터

`web` 스타터는 Spring Boot 애플리케이션에서 사용되는 가장 일반적인 스타터입니다. 여기에는 웹 애플리케이션을 만드는 데 필요한 모든 종속성이 포함됩니다. 여기에는 웹 서버, 템플릿 엔진 등이 포함됩니다.

`web` 스타터에는 `spring-boot-starter-tomcat` 종속성도 포함됩니다. 이 종속성은 임베디드 Tomcat 서버를 제공하는 데 사용됩니다. 이것은 웹 애플리케이션을 실행하는 데 사용될 서버입니다.

`web` 스타터를 사용하려면 `pom.xml` 파일에 다음 종속성을 추가합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

또는 Gradle을 사용하는 경우 `build.gradle` 파일에 다음 종속성을 추가합니다.

```groovy
dependencies {
    compile group: 'org.springframework.boot', name: 'spring-boot-starter-web'
}
```

## JPA 스타터

`jpa` 스타터는 JPA(Java Persistence API)에 대한 지원을 추가하는 데 사용됩니다. JPA는 관계형 데이터베이스에서 데이터 액세스, 지속 및 관리를 위한 Java 사양입니다.

`jpa` 스타터에는 `hibernate-entitymanager` 종속성이 포함됩니다. 최대 절전 모드는 널리 사용되는 JPA 구현입니다. `hibernate-entitymanager` 종속성은 JPA 구현을 제공하는 데 사용됩니다.

`jpa` 스타터를 사용하려면 `pom.xml` 파일에 다음 종속성을 추가합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

또는 Gradle을 사용하는 경우 `build.gradle` 파일에 다음 종속성을 추가합니다.

```groovy
dependencies {
    compile group: 'org.springframework.boot', name: 'spring-boot-starter-data-jpa'
}
```

## JDBC 스타터

`jdbc` 스타터는 JDBC(Java Database Connectivity API)에 대한 지원을 추가하는 데 사용됩니다. JDBC는 관계형 데이터베이스의 데이터에 액세스하고 데이터를 관리하기 위한 Java 사양입니다.

`jdbc` 스타터에는 `tomcat-jdbc` 종속성이 포함됩니다. Tomcat JDBC는 관계형 데이터베이스에 연결하는 데 사용되는 JDBC 드라이버입니다.

`jdbc` 스타터를 사용하려면 `pom.xml` 파일에 다음 종속성을 추가합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
```

또는 Gradle을 사용하는 경우 `build.gradle` 파일에 다음 종속성을 추가합니다.

```groovy
dependencies {
    compile group: 'org.springframework.boot', name: 'spring-boot-starter-jdbc'
}
```

## 테스트 스타터

`test` 스타터는 Spring Boot 애플리케이션 테스트 지원을 추가하는 데 사용됩니다. `test` 스타터에는 `junit` 및 `mockito-core` 종속성이 포함됩니다. JUnit은 널리 사용되는 Java 테스트 프레임워크입니다. Mockito는 널리 사용되는 Java 모킹 프레임워크입니다.

`test` 스타터를 사용하려면 `pom.xml` 파일에 다음 종속성을 추가합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
</dependency>
```

또는 Gradle을 사용하는 경우 `build.gradle` 파일에 다음 종속성을 추가합니다.

```groovy
dependencies {
    testCompile group: 'org.springframework.boot', name: 'spring-boot-starter-test'
}
```

## 결론

이 기사에서는 Spring Boot 스타터에 대한 빠른 시작 가이드를 제공했습니다. 스타터가 Maven 또는 Gradle 구성을 단순화하는 방법을 보여주었습니다. 또한 사용할 수 있는 일반적인 스타터의 몇 가지 예를 제공했습니다. 이 기사를 마칠 때쯤이면 스타터가 무엇인지, 자신의 애플리케이션에서 스타터를 어떻게 사용할 수 있는지 잘 이해하게 될 것입니다.