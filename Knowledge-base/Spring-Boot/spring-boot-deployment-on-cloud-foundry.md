---
title: Cloud Foundry에 Spring Boot 배포
description: 
published: true
date: 2023-02-02T14:57:41.458Z
tags: 
editor: markdown
dateCreated: 2023-02-02T14:57:39.804Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Deployment on Cloud Foundry***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-deployment-on-cloud-foundry)
{.links-list}


# Cloud Foundry에 스프링 부트 배포

Cloud Foundry에 Spring Boot 기반 애플리케이션을 배포하려는 개발자에게는 몇 가지 다른 옵션이 있습니다. 이 기사에서는 이러한 옵션 중 몇 가지를 살펴보고 각 옵션의 장단점에 대해 설명합니다.

## 항아리로 포장하기

Spring Boot 애플리케이션을 패키징하는 한 가지 옵션은 이를 jar 파일로 패키징하는 것입니다. 이는 Spring Boot 설명서에서 권장되는 접근 방식입니다.

Spring Boot 애플리케이션을 jar로 패키징하려면 `spring-boot-maven-plugin` 플러그인을 사용해야 합니다. 이 플러그인은 애플리케이션을 실행 가능한 jar 파일로 패키징합니다. 그런 다음 `cf push` 명령을 사용하여 이 jar 파일을 Cloud Foundry에 배포할 수 있습니다.

애플리케이션을 jar로 패키징하는 것의 한 가지 이점은 `java -jar` 명령을 사용하여 로컬에서 쉽게 실행할 수 있다는 것입니다. 이는 디버깅 목적에 도움이 될 수 있습니다.

jar로 패키징하는 것의 또 다른 장점은 `manifest.yml` 파일에서 애플리케이션에 필요한 모든 환경 변수를 지정할 수 있다는 것입니다. 이는 코드에서 환경별 값을 하드 코딩하지 않으려는 경우에 유용할 수 있습니다.

## 전쟁으로 패키징

Spring Boot 애플리케이션을 패키징하는 또 다른 옵션은 war 파일로 패키징하는 것입니다. 이는 Spring Boot 설명서에서 권장되는 접근 방식이 아니지만 옵션입니다.

Spring Boot 애플리케이션을 전쟁으로 패키징하려면 `spring-boot-starter-web` 종속성을 사용해야 합니다. 이 종속성은 애플리케이션을 전쟁으로 패키징하는 데 필요한 모든 라이브러리를 포함합니다.

그런 다음 `cf push` 명령을 사용하여 이 war 파일을 Cloud Foundry에 배포할 수 있습니다. 전쟁으로 패키징하는 것의 장점 중 하나는 `manifest.yml` 파일에서 애플리케이션에 필요한 모든 환경 변수를 지정할 수 있다는 것입니다. 이는 코드에서 환경별 값을 하드 코딩하지 않으려는 경우에 유용할 수 있습니다.

## Cloud Foundry Java 빌드팩 사용

Cloud Foundry는 Spring Boot 애플리케이션을 배포하는 데 사용할 수 있는 Java 빌드팩을 제공합니다. 이 빌드팩은 애플리케이션이 Spring Boot 애플리케이션임을 감지하고 그에 따라 구성합니다.

Cloud Foundry Java 빌드팩을 사용하려면 `manifest.yml` 파일에서 `java_buildpack`을 애플리케이션의 빌드팩으로 지정해야 합니다. 그런 다음 `cf push` 명령을 사용하여 애플리케이션을 배포할 수 있습니다.

Cloud Foundry Java 빌드팩을 사용하는 한 가지 이점은 애플리케이션을 jar 또는 war 파일에 패키징할 필요가 없다는 것입니다. 빌드팩이 이를 수행합니다.

Cloud Foundry Java 빌드팩을 사용하는 또 다른 이점은 `manifest.yml` 파일에서 애플리케이션에 필요한 모든 환경 변수를 지정할 수 있다는 것입니다. 이는 코드에서 환경별 값을 하드 코딩하지 않으려는 경우에 유용할 수 있습니다.

## 스프링 클라우드 커넥터 사용

Spring Cloud Connector는 Spring 애플리케이션에서 모든 Cloud Foundry 서비스를 사용할 수 있도록 하는 추상화 계층을 제공합니다. 이것은 현재 Cloud Foundry Java 빌드팩에서 지원하지 않는 서비스를 사용하려는 경우에 유용할 수 있습니다.

Spring Cloud Connector를 사용하려면 프로젝트에 `spring-cloud-spring-service-connector` 종속성을 추가해야 합니다. 그런 다음 `cf push` 명령을 사용하여 애플리케이션을 배포할 수 있습니다.

Spring Cloud Connectors를 사용하는 한 가지 이점은 애플리케이션을 jar 또는 war 파일에 패키징할 필요가 없다는 것입니다. 빌드팩이 이를 수행합니다.

Spring Cloud Connectors를 사용하는 또 다른 이점은 `manifest.yml` 파일에서 애플리케이션에 필요한 모든 환경 변수를 지정할 수 있다는 것입니다. 이는 코드에서 환경별 값을 하드 코딩하지 않으려는 경우에 유용할 수 있습니다.

## 결론

Cloud Foundry에 Spring Boot 애플리케이션을 배포하기 위한 몇 가지 옵션이 있습니다. 각 옵션에는 고유한 장점과 단점이 있습니다. 귀하의 애플리케이션에 가장 적합한 옵션을 결정하는 것은 귀하에게 달려 있습니다.