---
title: Spring Boot 애플리케이션 배포: 모범 사례
description: 
published: true
date: 2023-02-17T18:02:44.981Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:59:25.895Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Deploying Spring Boot Applications: Best Practices***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/deploying-spring-boot-applications-best-practices)
{.links-list}
 


# Spring Boot 애플리케이션 배포: 모범 사례

Spring Boot는 프로덕션 등급의 독립 실행형 Spring 기반 애플리케이션을 쉽게 만들 수 있는 인기 있는 Java 웹 프레임워크입니다. 이 기사에서는 Spring Boot 애플리케이션을 배포하기 위한 몇 가지 모범 사례에 대해 설명합니다.

## 목차

1. [스프링 부트 애플리케이션 생성](#creating-a-spring-boot-application)
2. [Spring Boot 애플리케이션 배포](#deploying-a-spring-boot-application)
    1. [건축](#architecture)
    2. [웹 서버](#web-servers)
3. [결론](#결론)

## 스프링 부트 애플리케이션 만들기

Spring Boot 애플리케이션을 만드는 것은 간단합니다. Java와 텍스트 편집기만 있으면 됩니다. Spring Boot 애플리케이션은 일반적으로 jar 파일로 패키징되며 `java -jar` 명령을 사용하여 실행할 수 있습니다. 예를 들어 다음 명령은 포트 8080에서 실행되는 Spring Boot 애플리케이션을 시작합니다.

```java
java -jar my-spring-boot-app.jar
```

Maven을 사용하는 경우 `spring-boot:run` 목표를 사용할 수도 있습니다.

```
mvn spring-boot:run
```

Spring Initializr를 사용하여 Spring Boot 애플리케이션을 만들 수도 있습니다. Spring Initializr는 선택 사항에 따라 Spring Boot 애플리케이션을 생성할 수 있는 웹 애플리케이션입니다. 원하는 종속성을 선택하기만 하면 Initializr가 해당 종속성을 포함하는 프로젝트를 생성합니다.

## 스프링 부트 애플리케이션 배포

Spring Boot 애플리케이션을 배포하는 것은 쉽습니다. 기존 Java 웹 애플리케이션과 달리 서블릿 컨테이너 또는 애플리케이션 서버를 구성할 필요가 없습니다. 그러나 Spring Boot 애플리케이션을 배포할 때 염두에 두어야 할 몇 가지 사항이 있습니다.

### 건축학

Spring Boot 애플리케이션은 일반적으로 독립 실행형 jar 파일로 배포됩니다. 이를 통해 Java를 지원하는 모든 플랫폼에서 Spring Boot 애플리케이션을 쉽게 배포하고 실행할 수 있습니다.

Spring Boot 애플리케이션은 war 파일로도 배포할 수 있습니다. 그러나 애플리케이션을 실행하려면 서블릿 컨테이너 또는 애플리케이션 서버가 필요하므로 권장되는 배포 방식은 아닙니다.

### 웹 서버

Spring Boot 애플리케이션은 다양한 웹 서버에 배포할 수 있습니다. 가장 인기 있는 옵션은 Apache Tomcat 및 Jetty입니다.

Tomcat은 Java 애플리케이션에 가장 널리 사용되는 웹 서버입니다. Tomcat은 서블릿 컨테이너이며 War 파일을 실행할 수 있습니다. Tomcat은 독립 실행형 서버와 포함 가능한 서블릿 컨테이너로 모두 사용할 수 있습니다.

Jetty는 널리 사용되는 오픈 소스 웹 서버입니다. Jetty는 서블릿 컨테이너이며 War 파일을 실행할 수 있습니다. Jetty는 독립 실행형 서버와 포함 가능한 서블릿 컨테이너로 모두 사용할 수 있습니다.

## 결론

Spring Boot 애플리케이션을 배포하는 것은 쉽습니다. Spring Boot 애플리케이션은 다양한 웹 서버에 배포할 수 있으며 서블릿 컨테이너 또는 애플리케이션 서버가 필요하지 않습니다.