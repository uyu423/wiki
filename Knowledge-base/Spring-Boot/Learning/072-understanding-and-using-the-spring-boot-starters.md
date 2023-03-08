---
title: 072: 스프링 부트 스타터 이해 및 사용
description: 
published: true
date: 2023-02-05T05:32:15.561Z
tags: 
editor: markdown
dateCreated: 2023-02-05T05:32:13.924Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [072: Understanding and Using the Spring Boot Starters***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/072-understanding-and-using-the-spring-boot-starters)
{.links-list}


# 072: 스프링 부트 스타터 이해 및 사용

Spring Boot Starters는 애플리케이션에 포함될 수 있는 편리한 종속성 설명자 집합입니다. 프로젝트에 이들 중 하나를 포함하면 프로젝트를 빠르고 쉽게 시작하고 실행하는 데 사용할 수 있는 잘 구성되고 바로 사용할 수 있는 종속성 세트를 얻을 수 있습니다.

이 게시물에서는 Spring Boot Starter가 무엇인지, 어떻게 작동하는지, 그리고 자신의 프로젝트에서 어떻게 사용할 수 있는지 살펴보겠습니다.

## 스프링 부트 스타터가 무엇인가요?

Spring Boot Starters는 프로젝트에 포함될 수 있는 종속성 설명자 집합입니다. 이러한 디스크립터는 프로젝트를 빠르고 쉽게 시작하고 실행하는 데 사용할 수 있는 잘 구성되고 즉시 사용할 수 있는 종속성 세트를 정의합니다.

Spring Boot Starter는 Core Starter와 Web Starter의 두 그룹으로 나뉩니다. Core Starter는 모든 Spring Boot 애플리케이션에 필요한 종속성입니다. Web Starter는 웹 인터페이스를 노출할 모든 Spring Boot 애플리케이션에 필요한 종속성입니다.

## Spring Boot Starter는 어떻게 작동하나요?

Spring Boot Starter는 잘 구성되고 바로 사용할 수 있는 종속성 집합을 제공하여 작동합니다. 이러한 종속성을 사용하여 프로젝트를 빠르고 쉽게 시작하고 실행할 수 있습니다.

프로젝트에 Spring Boot Starter를 포함하면 해당 Starter에 필요한 모든 종속성이 자동으로 포함됩니다. 예를 들어 프로젝트에 `spring-boot-starter-web` 스타터를 포함하면 `spring-boot-starter-web` 스타터가 `spring-boot-starter-tomcat` 스타터에 따라 자동으로 `spring-boot-starter-tomcat` 스타터가 포함됩니다. -boot-starter-tomcat` 스타터.

## 내 프로젝트에서 Spring Boot Starter를 어떻게 사용할 수 있나요?

자체 프로젝트에 Spring Boot Starter를 포함하는 것은 쉽습니다. 프로젝트의 `pom.xml` 파일에 적절한 종속성을 추가하기만 하면 됩니다.

예를 들어 프로젝트에 `spring-boot-starter-web` 스타터를 포함하려면 `pom.xml` 파일에 다음 종속성을 추가합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

## 결론

이 게시물에서는 Spring Boot Starter가 무엇인지, 어떻게 작동하는지, 자신의 프로젝트에서 어떻게 사용할 수 있는지 살펴보았습니다.