---
title: Spring Boot로 백엔드 시스템 설정
description: 
published: true
date: 2023-02-17T18:01:03.735Z
tags: 
editor: markdown
dateCreated: 2023-01-29T21:31:47.652Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Setting up a Backend System with Spring Boot***English** version of this document is available*](/en/Knowledge-base/Backend/setting-up-a-backend-system-with-spring-boot)
{.links-list}


# Spring Boot로 백엔드 시스템 설정하기

Spring Boot는 웹 애플리케이션 및 마이크로 서비스 개발에 사용되는 널리 사용되는 Java 기반 프레임워크입니다. Pivotal에서 개발했으며 Apache 라이선스 2.0에 따라 사용할 수 있습니다.

Spring Boot를 사용하면 "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다. 최소한의 소란으로 시작할 수 있도록 Spring 플랫폼 및 타사 라이브러리에 대한 독단적인 관점을 취합니다. 대부분의 Spring Boot 애플리케이션에는 Spring 구성이 거의 필요하지 않습니다.

## 스프링 부트를 사용하는 이유

다음 프로젝트를 개발할 때 Spring Boot를 사용해야 하는 많은 이유가 있습니다. 다음은 가장 중요한 몇 가지 이유입니다.

* 그냥 실행할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 쉽게 만들 수 있습니다.
* Spring 플랫폼 및 타사 라이브러리에 대한 독단적인 관점을 취하므로 최소한의 소란으로 시작할 수 있습니다.
* 생산 준비가 된 응용 프로그램을 쉽게 만들 수 있습니다.
* 모든 프로젝트에서 사용할 수 있는 다양한 기능을 제공합니다.
* XML 구성이 필요하지 않습니다.

## 시작하기

이 섹션에서는 Spring Boot를 시작하는 방법을 보여줍니다. [Spring Initializr](https://start.spring.io/)를 사용하여 새로운 Spring Boot 프로젝트를 생성하는 것으로 시작하겠습니다. Spring Initializr는 새로운 Spring Boot 프로젝트를 쉽게 생성할 수 있게 해주는 웹 기반 도구입니다.

### 새 프로젝트 만들기

새 Spring Boot 프로젝트를 생성하려면 Spring Initializr 웹 도구를 사용할 수 있습니다. [Spring Initializr](https://start.spring.io/) 웹사이트로 이동하여 다음 옵션을 선택합니다.

* 프로젝트: `Gradle 프로젝트`
* 언어: `자바`
* 스프링 부트 버전: `2.1.3`
* 프로젝트 메타데이터:
  * 그룹: `com.example`
  * 아티팩트: `myproject`
  * 이름: `나의 프로젝트`
  * 설명 : `간단한 Spring Boot 프로젝트`
  * 패키지 이름: `com.example.myproject`
* 포장: '항아리'
* 자바 버전: `8`
* 종속성: `웹`

![새 Spring Boot 프로젝트 만들기](https://i.imgur.com/EuFcU3v.png)

"프로젝트 생성" 버튼을 클릭하여 새 Spring Boot 프로젝트가 포함된 zip 파일을 다운로드합니다.

### IDE로 프로젝트 가져오기

STS(Spring Tool Suite)는 Spring 기반 애플리케이션 개발에 널리 사용되는 IDE입니다. 이 섹션에서는 프로젝트를 STS로 가져오는 방법을 보여줍니다.

STS를 시작하고 `파일` -> `가져오기...`로 이동합니다. 옵션 목록에서 `Gradle 프로젝트`를 선택하고 `다음`을 클릭합니다.

![Gradle 프로젝트를 STS로 가져오기](https://i.imgur.com/vYIT6TK.png)

Spring Initializr에서 다운로드한 프로젝트의 위치를 찾아 '마침'을 클릭합니다.

![가져올 프로젝트 선택하기](https://i.imgur.com/WY6lNcu.png)

 STS는 프로젝트를 가져오고 다음과 유사한 프로젝트 구조를 만듭니다.

```
myproject
├── src
│   └── main
│       ├── java
│       │   └── com
│       │       └── example
│       │           └── myproject
│       │               └── Application.java
│       └── resources
│           ├── application.properties
│           └── static
│               └── index.html
├── build.gradle
└── settings.gradle
```

### 애플리케이션 실행

`gradlew` 명령을 사용하여 명령줄에서 애플리케이션을 실행할 수 있습니다.

```
$ ./gradlew bootRun
```

IDE에서 애플리케이션을 실행할 수도 있습니다. STS에서 `Application.java` 파일을 마우스 오른쪽 버튼으로 클릭하고 `Run As` -> `Spring Boot App`을 선택할 수 있습니다.

![STS에서 애플리케이션 실행하기](https://i.imgur.com/DY0SVqf.png)

응용 프로그램이 실행 중일 때 [http://localhost:8080/](http://localhost:8080/)에서 첫 페이지에 액세스할 수 있습니다.

![지원서 첫 페이지](https://i.imgur.com/i1aBG3g.png)

## 결론

이 기사에서는 Spring Boot를 시작하는 방법을 설명했습니다. Spring Initializr를 사용하여 새 프로젝트를 만들고 IDE로 가져왔습니다. 또한 응용 프로그램을 실행하는 방법도 보여 주었습니다.