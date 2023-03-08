---
title: 003: Spring Boot 자동 구성 이해
description: 
published: true
date: 2023-02-03T07:17:17.000Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:17:15.496Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [003: Understanding Spring Boot auto-configuration***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/003-understanding-spring-boot-auto-configuration)
{.links-list}


## Spring Boot 자동 구성 이해

Spring Boot 자동 구성은 프로젝트에 있는 종속성을 기반으로 Spring 애플리케이션을 자동으로 구성하는 기능입니다. 이것은 예를 들어 Hibernate가 클래스 경로에 있는 경우 Spring Boot가 자동으로 DataSource 및 엔티티 관리자 팩토리를 설정한다는 것을 의미합니다.

자동 구성 기능은 Spring Boot에서 기본적으로 활성화됩니다. 그러나 spring.boot.autoconfigure.EnableAutoConfiguration 속성을 false로 설정하여 비활성화할 수 있습니다.

자동 구성이 활성화되면 Spring Boot는 프로젝트에 있는 종속성을 기반으로 애플리케이션 구성을 시도합니다. 예를 들어 Hibernate가 클래스 경로에 있는 경우 Spring Boot는 자동으로 DataSource 및 엔티티 관리자 팩토리를 구성합니다.

자동 구성은 Spring Boot를 시작할 때 유용한 기능이 될 수 있습니다. 그러나 애플리케이션이 커짐에 따라 애플리케이션의 특정 부분에 대한 자동 구성을 비활성화할 수 있습니다.

Spring Boot 자동 구성에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [Spring Boot의 자동 구성 기능](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-auto-configuration.html)

- [Spring Boot에서 자동 구성 비활성화](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-auto-configuration.html# boot-features-auto -구성 제외)