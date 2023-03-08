---
title: 프로젝트 생성을 위한 Spring Boot Initializer
description: 
published: true
date: 2023-02-07T21:32:33.416Z
tags: 
editor: markdown
dateCreated: 2023-02-07T21:32:31.782Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Initializer for Project Creation***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-initializer-for-project-creation)
{.links-list}


# 프로젝트 생성을 위한 Spring Boot Initializer

새 프로젝트를 개발하는 것은 특히 처음부터 시작할 때 시간이 많이 소요될 수 있습니다. Spring Boot를 사용하면 "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 더 쉽게 만들 수 있습니다. 쉽게 구성할 수 있는 유연한 빌드 시스템과 애플리케이션 서버를 제공합니다.

이 기사에서는 Spring Boot Initializr를 사용하여 새로운 Spring Boot 프로젝트를 생성하는 방법을 보여줍니다. Spring Boot Initializr는 Spring Boot 프로젝트를 생성할 수 있는 웹 애플리케이션입니다. 프로젝트에 필요한 종속성을 선택하는 옵션을 제공합니다.

## 스프링부트 이니셜라이저란?

Spring Boot Initializr는 Spring Boot 프로젝트를 생성할 수 있는 웹 애플리케이션입니다. 프로젝트에 필요한 종속성을 선택하는 옵션을 제공합니다.

생성된 프로젝트에는 선택한 종속 항목이 포함되며 Gradle 또는 Maven 빌드 도구로 빌드할 수 있습니다. 또한 애플리케이션 서버(있는 경우) 및 빌드 도구에 필요한 구성 파일도 포함되어 있습니다.

## Spring Boot Initializr는 어떻게 사용하나요?

Spring Boot Initializr를 사용하려면 Initializr 웹 애플리케이션에 액세스해야 합니다. Spring Boot Initializr 웹 사이트(https://start.spring.io/)를 방문하여 이를 수행할 수 있습니다.

![스프링 부트 초기화](https://i.imgur.com/HLgHZzg.png)

Initializr 웹 사이트에서 프로젝트에 필요한 종속성을 선택할 수 있습니다. 예를 들어 데이터베이스 액세스에 JPA를 사용해야 하는 경우 "JPA" 종속성을 선택할 수 있습니다.

![Spring Boot Initializr 종속성](https://i.imgur.com/pz4UHz.png)

종속성을 선택한 후 프로젝트를 생성할 수 있습니다. 프로젝트는 ZIP 파일로 생성됩니다.

## Spring Boot 프로젝트는 어떻게 생성하나요?

Spring Boot Initializr를 사용하는 방법을 살펴보았으니 이제 Spring Boot 프로젝트를 생성해 보겠습니다.

우리는 Initializr 웹사이트를 사용하여 다음과 같은 종속성이 있는 Spring Boot 프로젝트를 생성할 것입니다.

- 웹
- JPA
- MySQL

![Spring Boot Initializr 종속성](https://i.imgur.com/pz4UHz.png)

종속성을 선택한 후 프로젝트를 생성할 수 있습니다. 프로젝트는 ZIP 파일로 생성됩니다.

## 프로젝트를 Eclipse로 가져오는 방법은 무엇입니까?

이제 프로젝트를 생성했으므로 Eclipse로 가져오겠습니다.

Eclipse에서 파일 -> 가져오기 -> 기존 Maven 프로젝트를 선택합니다.

![Maven 프로젝트를 Eclipse로 가져오기](https://i.imgur.com/Vywzo8I.png)

"Import Maven Project" 대화 상자에서 방금 생성한 "spring-boot-mysql-example" 프로젝트를 선택합니다.

![메이븐 프로젝트 가져오기](https://i.imgur.com/pz4UHz.png)

"마침"을 클릭하여 프로젝트를 가져옵니다.

프로젝트를 Eclipse로 가져옵니다.

## 프로젝트를 어떻게 실행하나요?

이제 프로젝트를 가져왔으니 실행해 보겠습니다.

프로젝트를 마우스 오른쪽 버튼으로 클릭하고 "Run As -> Java Application"을 선택합니다.

![자바 애플리케이션 실행](https://i.imgur.com/7lFWoqo.png)

"Java 애플리케이션" 대화창에서 "애플리케이션" 클래스를 선택하고 "확인"을 클릭하십시오.

![자바 애플리케이션](https://i.imgur.com/pz4UHz.png)

프로젝트는 임베디드 Tomcat 서버에서 실행됩니다.

http://localhost:8080/에서 애플리케이션에 액세스할 수 있습니다.

## 결론

이 기사에서는 Spring Boot Initializr를 사용하여 새로운 Spring Boot 프로젝트를 생성하는 방법을 설명했습니다. Spring Boot Initializr는 Spring Boot 프로젝트를 생성할 수 있는 웹 애플리케이션입니다. 프로젝트에 필요한 종속성을 선택하는 옵션을 제공합니다.