---
title: Heroku에 스프링 부트 배포
description: 
published: true
date: 2023-02-07T12:32:31.890Z
tags: 
editor: markdown
dateCreated: 2023-02-07T12:32:29.639Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Deployment on Heroku***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-deployment-on-heroku)
{.links-list}


# Heroku에 스프링 부트 배포

Heroku는 여러 프로그래밍 언어를 지원하는 서비스형 클라우드 플랫폼(PaaS)입니다. 이러한 언어 중 하나는 Java입니다. 이 기사에서는 Heroku에서 Spring Boot 애플리케이션을 배포하는 방법에 대해 설명합니다.

## 스프링부트란?

Spring Boot는 마이크로 서비스를 생성하는 데 사용되는 Java 기반 프레임워크입니다. Pivotal Team에서 개발했으며 무료 오픈 소스 프로젝트입니다.

## 헤로쿠란?

Heroku는 여러 프로그래밍 언어를 지원하는 서비스형 클라우드 플랫폼(PaaS)입니다.

Heroku는 개발자가 애플리케이션을 배포, 관리 및 확장할 수 있는 PaaS(Platform as a Service)입니다. Heroku는 간단하고 사용하기 쉬우며 소규모 애플리케이션을 위한 무료 플랜을 제공합니다.

## 전제 조건

시작하기 전에 다음이 필요합니다.

- Heroku 계정
- 텍스트 편집기
- JDK 8 이상
- 메이븐 3.3.9 이상

## 스프링 부트 애플리케이션 만들기

먼저 Spring Boot 애플리케이션을 만들어야 합니다. Spring Initializr를 사용하여 이를 수행할 수 있습니다.

Spring Initializr는 Spring Boot 애플리케이션을 만들 수 있게 해주는 웹 애플리케이션입니다. 그것은 당신을 위한 프로젝트 구조를 생성하고 필요한 의존성을 추가할 것입니다.

Spring Boot 애플리케이션을 생성하려면 https://start.spring.io/로 이동하고 다음을 선택합니다.

- 언어: 자바
- 스프링 부트 버전: 2.4.4
- 프로젝트: 메이븐 프로젝트
- 포장: 항아리
- 자바 버전: 8
- 그룹: com.heroku
- 아티팩트: 데모

프로젝트 생성을 클릭하여 프로젝트를 다운로드합니다.

## 프로필 생성

Procfile은 시작 시 앱에서 실행되는 명령이 포함된 텍스트 파일입니다. Procfile은 애플리케이션의 루트 디렉터리에 있어야 합니다.

확장명 없이 Procfile이라는 파일을 만들고 다음 줄을 추가합니다.

    웹: java -jar target/demo-0.0.1-SNAPSHOT.jar

## Heroku 앱 만들기

Procfile을 생성하면 Heroku 앱을 생성할 수 있습니다.

Heroku 계정에 로그인하고 새로 만들기 -> 새 앱 만들기를 클릭합니다.

다음 정보를 입력하십시오.

- 앱 이름: 데모
- 지역: 유럽

앱 만들기를 클릭합니다.

## Heroku에 앱 배포

앱이 생성되면 Spring Boot 애플리케이션을 Heroku에 배포할 수 있습니다.

Heroku는 배포에 Git을 사용하므로 Heroku Git 리포지토리에 코드를 푸시해야 합니다.

먼저 Heroku Git 리포지토리를 로컬 리포지토리에 원격으로 추가해야 합니다. 이렇게 하려면 다음 명령을 실행합니다.

    $ heroku git:remote - 데모

그런 다음 다음 명령을 사용하여 코드를 Heroku Git 리포지토리로 푸시할 수 있습니다.

    $ git push 헤로쿠 마스터

코드가 푸시되면 Heroku는 애플리케이션을 빌드하고 배포합니다.

다음 명령을 사용하여 로그를 볼 수 있습니다.

    $ heroku 로그 --tail

## 결론

이 기사에서는 Heroku에서 Spring Boot 애플리케이션을 배포하는 방법에 대해 설명했습니다.