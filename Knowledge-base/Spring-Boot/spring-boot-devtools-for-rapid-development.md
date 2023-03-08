---
title: 신속한 개발을 위한 Spring Boot DevTools
description: 
published: true
date: 2023-02-07T20:32:26.748Z
tags: 
editor: markdown
dateCreated: 2023-02-07T20:32:20.961Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot DevTools for Rapid Development***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-devtools-for-rapid-development)
{.links-list}


# 신속한 개발을 위한 Spring Boot DevTools

Spring Boot로 애플리케이션을 빠르게 개발하려는 개발자는 Spring Boot DevTools를 사용할 수 있습니다. 이 기사에서는 DevTools의 기능과 개발 프로세스 속도를 높이는 방법을 살펴봅니다.

## Spring Boot DevTools가 무엇인가요?

Spring Boot DevTools는 개발자가 Spring Boot 애플리케이션을 빠르게 개발하는 데 도움이 되는 도구 세트입니다. 이 도구는 클래스의 라이브 다시 로드, 애플리케이션 자동 다시 시작 및 디버깅 지원과 같은 기능을 제공합니다.

## DevTools는 빠른 개발에 어떻게 도움이 되나요?

DevTools는 시간을 절약하고 수동 개입의 필요성을 줄이는 기능을 제공하여 신속한 개발을 돕습니다. 예를 들어 클래스를 실시간으로 다시 로드하면 개발자가 코드를 변경하고 애플리케이션을 다시 시작하지 않고도 즉시 결과를 확인할 수 있습니다. 이렇게 하면 특히 작은 변경 사항을 적용할 때 많은 시간을 절약할 수 있습니다.

## DevTools의 다른 기능에는 어떤 것이 있나요?

실시간 재로딩 및 자동 재시작 외에도 DevTools는 디버깅 및 테스트 지원도 제공합니다. Eclipse 또는 IntelliJ IDEA의 디버깅 서버와 같은 원격 디버거에 연결하도록 DevTools를 구성할 수 있습니다. 이를 통해 개발자는 응용 프로그램을 서버에 배포하지 않고도 원격으로 디버깅할 수 있습니다.

DevTools는 테스트 실행에 대한 지원도 제공합니다. 코드가 변경되면 자동으로 테스트를 실행하도록 DevTools를 구성할 수 있습니다. 개발자가 테스트를 수동으로 실행할 필요가 없으므로 시간을 많이 절약할 수 있습니다.

## DevTools를 시작하려면 어떻게 해야 하나요?

DevTools는 Spring Boot 웹사이트(https://spring.io/tools)에서 다운로드할 수 있습니다. DevTools는 Eclipse, IntelliJ IDEA 및 NetBeans와 같은 모든 주요 IDE와 호환됩니다.

DevTools가 설치되면 프로젝트에 `spring-boot-devtools` 종속성을 추가하여 사용할 수 있습니다. DevTools는 `spring.devtools.restart.enabled` 및 `spring.devtools.livereload.enabled` 속성을 사용하여 구성할 수도 있습니다.

## 결론

Spring Boot DevTools는 Spring Boot 애플리케이션을 빠르게 개발하는 데 유용한 도구입니다. 이 도구는 라이브 다시 로드, 자동 다시 시작 및 디버깅 지원과 같은 기능을 제공합니다. DevTools는 Spring Boot 웹 사이트에서 다운로드할 수 있으며 프로젝트에 `spring-boot-devtools` 종속성을 추가하여 사용할 수 있습니다.