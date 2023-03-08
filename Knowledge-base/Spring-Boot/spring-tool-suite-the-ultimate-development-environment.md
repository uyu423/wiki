---
title: Spring Tool Suite: 궁극의 개발 환경
description: 
published: true
date: 2023-02-06T05:32:27.851Z
tags: 
editor: markdown
dateCreated: 2023-02-06T05:32:26.239Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Tool Suite: The Ultimate Development Environment***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-tool-suite-the-ultimate-development-environment)
{.links-list}

      

# Spring Tool Suite: 궁극의 개발 환경

매우 다양한 옵션과 구성을 사용할 수 있으므로 개발 환경을 설정하는 것은 특히 IT 세계를 처음 접하는 사람들에게 어려운 작업이 될 수 있습니다. 그러나 이 프로세스를 훨씬 쉽게 만들 수 있는 하나의 도구가 있습니다. 바로 STS(Spring Tool Suite)입니다.

STS는 Spring 애플리케이션 개발을 위해 특별히 설계된 Eclipse 기반 IDE입니다. 다음을 포함하여 개발자 경험을 크게 향상시킬 수 있는 다양한 기능이 제공됩니다.

- 새로운 Spring Boot, MVC 및 Batch 프로젝트를 만들기 위한 프로젝트 템플릿.
- 프로젝트 메타데이터 자동 생성(예: pom.xml 파일).
- Java 클래스 및 자원의 동적 재로딩을 위한 기본 제공 지원.
- Maven 및 Gradle과 같은 널리 사용되는 빌드 도구와의 통합.
- 애플리케이션 로그의 출력을 보기 위한 콘솔 보기.

또한 STS는 다음과 같은 더 많은 기능을 추가할 수 있는 풍부한 플러그인을 제공합니다.

- Spring Cloud CLI: 로컬 시스템에서 Spring Cloud 애플리케이션을 개발, 테스트 및 배포할 수 있습니다.
- Spring Cloud Data Flow: Spring Cloud Streams를 사용하여 데이터 파이프라인을 구축하기 위한 도구입니다.
- Spring Cloud Security: Spring Cloud 애플리케이션에 보안 기능을 추가합니다.

이러한 모든 기능을 갖춘 STS는 경험 수준에 관계없이 모든 개발자에게 강력한 자산이 될 수 있습니다. 이 기사에서는 STS를 시작하는 방법과 STS의 가장 유용한 일부 기능에 대해 자세히 살펴보겠습니다.

## STS 설치

STS는 [Spring Tools 웹사이트](https://spring.io/tools)에서 다운로드할 수 있습니다. 사용 가능한 두 가지 버전이 있습니다.

- 핵심 STS 기능을 포함하는 **Standard** 에디션.
- **Ultimate** 에디션에는 Standard 에디션의 모든 기능과 클라우드 네이티브 애플리케이션 개발을 위한 추가 플러그인이 포함되어 있습니다.

이 기사에서는 Ultimate 버전을 사용합니다. ZIP 파일을 다운로드했으면 원하는 위치에 압축을 풀고 STS 실행 파일을 시작합니다.

## 새 프로젝트 만들기

STS를 처음 실행하면 시작 화면이 표시됩니다. 여기에서 새 프로젝트를 만들거나 기존 프로젝트를 가져오거나 디렉터리에서 프로젝트를 열도록 선택할 수 있습니다.

새 프로젝트를 만들 것이므로 "새 Spring Starter 프로젝트 만들기" 옵션을 선택합니다.

![STS 환영 화면](https://i.imgur.com/l7qE4Vx.png)

다음 화면에서 이름 및 위치와 같은 프로젝트에 대한 정보를 제공하라는 메시지가 표시됩니다. 또한 사용하려는 빌드 도구(Maven 또는 Gradle)와 만들려는 프로젝트 유형을 선택할 수 있습니다.

이 예제에서는 Maven 기반 Spring Boot 프로젝트를 생성합니다. 필요한 정보를 입력했으면 "마침" 버튼을 클릭합니다.

![새 프로젝트 화면](https://i.imgur.com/DY6rNcu.png)

 STS는 이제 프로젝트를 만들고 IDE에서 엽니다.

## IDE 살펴보기

STS IDE는 Eclipse를 기반으로 하므로 해당 IDE에 익숙하다면 편안하게 느낄 수 있을 것입니다. 그러나 언급할 가치가 있는 몇 가지 STS 관련 기능이 있습니다.

### 스프링 부트 대시보드

STS의 가장 유용한 기능 중 하나는 Spring Boot Dashboard입니다. 이것은 가장 일반적으로 사용되는 Spring Boot 기능에 대한 빠른 액세스를 제공하는 특수 보기입니다.

![스프링 부트 대시보드](https://i.imgur.com/uY0A8tV.png)

대시보드에서 애플리케이션의 종속성을 보고 관리하고, 애플리케이션을 시작 및 중지하고, 애플리케이션 로그를 보는 등의 작업을 수행할 수 있습니다.

### 스프링 부트 빈

STS의 또 다른 유용한 기능은 Spring Boot Beans 보기입니다. 이 뷰는 애플리케이션에 정의된 모든 빈과 해당 종속성을 보여줍니다.

![스프링부트콩](https://i.imgur.com/Lzq3G8I.png)

이는 응용 프로그램의 여러 부분이 서로 어떻게 조화를 이루는지 이해하는 데 도움이 되므로 응용 프로그램을 디버깅하는 데 유용한 도구가 될 수 있습니다.

### 스프링 부트 앱

Spring Boot 앱 보기는 Spring Boot 애플리케이션을 개발할 때 매우 유용할 수 있는 또 다른 STS 관련 기능입니다.

![스프링 부트 앱](https://i.imgur.com/DxvkVrA.png)

이 보기는 디버그 및 JMX 포트뿐만 아니라 로컬 시스템에서 실행 중인 모든 Spring Boot 애플리케이션을 표시합니다. 이는 디버깅 또는 모니터링 목적으로 원격 애플리케이션에 연결해야 할 때 매우 유용할 수 있습니다.

## 결론

이 기사에서는 Spring Tool Suite IDE의 가장 유용한 기능 중 일부를 살펴보았습니다. 또한 STS를 설치하고 새로운 Spring Boot 프로젝트를 생성하는 방법도 보았습니다.

이것은 STS가 제공해야 하는 것에 대한 간략한 소개일 뿐이지만 이 강력한 도구가 Spring 애플리케이션을 보다 효과적으로 개발하는 데 어떻게 도움이 되는지에 대한 좋은 아이디어를 제공해야 합니다.