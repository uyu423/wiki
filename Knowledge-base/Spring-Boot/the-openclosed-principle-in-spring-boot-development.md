---
title: Spring Boot 개발의 개방/폐쇄 원칙
description: 
published: true
date: 2023-02-08T11:32:16.154Z
tags: 
editor: markdown
dateCreated: 2023-02-08T11:32:14.650Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [The Open/Closed Principle in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-openclosed-principle-in-spring-boot-development)
{.links-list}

      
# Spring Boot 개발의 개방/폐쇄 원칙

OCP(Open/Closed Principle)는 소프트웨어는 확장에는 열려 있어야 하지만 수정에는 닫혀 있어야 한다는 소프트웨어 설계 원칙입니다. 이 원칙은 객체 지향 프로그래밍의 핵심 원칙 중 하나이며 소프트웨어를 보다 유지 관리 및 확장 가능하게 만드는 것을 목표로 합니다.

Spring Boot 개발 맥락에서 OCP는 Spring Boot 애플리케이션 자체와 애플리케이션을 구성하는 코드 모두의 디자인에 적용될 수 있습니다.

Spring Boot 애플리케이션을 설계할 때 다음을 준수하여 OCP 원칙을 적용할 수 있습니다.

- 독립적으로 유지 관리 및 확장할 수 있는 모듈식 구성 요소를 사용하여 애플리케이션을 설계합니다.
- 부품을 서로 단단히 결합하지 마십시오.
- 좋은 테스트 방법을 따라 테스트 가능성을 고려하여 설계합니다.

Spring Boot 애플리케이션을 구성하는 코드를 작성할 때 다음 지침에 따라 OCP 원칙을 적용할 수 있습니다.

- 이해하고 유지하기 쉬운 코드를 작성합니다.
- 단위 테스트가 쉬운 코드를 작성합니다.
- 단일 책임 원칙을 따릅니다.
- DRY 원칙을 따릅니다.

OCP 원칙을 Spring Boot 애플리케이션의 설계와 구현 모두에 적용하면 보다 유지 관리, 확장 및 테스트 가능한 애플리케이션이 생성됩니다.