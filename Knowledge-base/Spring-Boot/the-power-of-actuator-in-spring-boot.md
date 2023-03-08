---
title: Spring Boot에서 Actuator의 힘
description: 
published: true
date: 2023-02-17T18:02:13.056Z
tags: 
editor: markdown
dateCreated: 2023-01-30T08:58:13.473Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [The Power of Actuator in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-power-of-actuator-in-spring-boot)
{.links-list}


# Spring Boot에서 Actuator의 힘

소프트웨어 개발 맥락에서 액추에이터는 에너지를 동작으로 변환하는 장치입니다. Spring Boot Actuator는 애플리케이션을 모니터링하고 관리하는 데 도움이 되는 프로덕션 준비 기능을 제공하는 Spring Boot의 하위 프로젝트입니다. Spring Boot Actuator를 사용하면 프로덕션 환경에서 Spring Boot 애플리케이션을 쉽게 모니터링하고 관리할 수 있습니다.

 액추에이터 엔드포인트를 사용하면 애플리케이션을 모니터링하고 관리할 수 있습니다. 기본적으로 모든 엔드포인트는 보호되며 이를 노출하도록 보안을 구성해야 합니다. 이 기사에서는 가장 중요한 Spring Boot Actuator 끝점을 살펴보겠습니다.


## HTTP 끝점

HTTP 엔드포인트는 가장 기본적인 유형의 엔드포인트입니다. 버전 및 빌드 정보와 같은 애플리케이션 자체에 대한 정보를 노출합니다. HTTP 끝점에는 인증이나 승인이 필요하지 않습니다.

다음은 Spring Boot Actuator에서 기본적으로 사용 가능한 HTTP 끝점 목록입니다.

- `/info`: 임의의 애플리케이션 정보를 표시합니다.액추에이터는 임의의 정보를 노출하기 위해 임의의 엔드포인트에서 사용할 수 있는 `info` 맵을 빌드합니다.
- `/health`: 애플리케이션 상태 정보를 표시합니다. 이 정보는 모니터링 목적에 유용합니다. JSON, XML 또는 HTML 형식으로 검색할 수 있습니다.
- `/env`: Spring의 ConfigurableEnvironment에서 속성을 노출합니다.
- `/metrics`: 애플리케이션을 모니터링할 수 있는 다양한 미터, 카운터 및 게이지를 표시합니다.
- `/trace`: 추적 정보를 표시합니다(기본적으로 마지막 100개의 HTTP 요청).


## JMX 끝점

JMX 엔드포인트는 JMX MBeans를 통해 애플리케이션 관리 정보를 노출합니다. JMX 엔드포인트를 사용하여 프로덕션 환경에서 애플리케이션을 모니터링하고 관리할 수 있습니다.

다음은 Spring Boot Actuator에서 기본적으로 사용 가능한 JMX 엔드포인트 목록입니다.

- `/jolokia`: Jolokia 라이브러리를 사용하여 HTTP/JSON 프로토콜을 통해 JMX 빈을 노출합니다.
- `/logfile`: 로그 파일을 관리할 엔드포인트를 노출합니다.
- `/loggers`: 로거를 관리하기 위해 엔드포인트를 노출합니다.



## 관리 엔드포인트

관리 엔드포인트는 프로덕션 환경에서 애플리케이션을 관리하고 모니터링하는 데 사용됩니다. 관리 끝점을 사용하여 애플리케이션을 중지 및 다시 시작하고 로그 수준을 변경하는 등의 작업을 수행할 수 있습니다.

다음은 Spring Boot Actuator에서 기본적으로 사용 가능한 관리 엔드포인트 목록입니다.

- `/beans`: 애플리케이션에 있는 모든 Spring 빈의 전체 목록을 표시합니다.
- `/autoconfig`: Spring Boot가 애플리케이션을 자동 구성한 방법을 보여주는 자동 구성 보고서를 표시합니다.
- `/configprops`: 모든 @ConfigurationProperties 빈 목록을 표시합니다.
- `/dump`: 스레드 덤프를 수행합니다.
- `/mappings`: 모든 @RequestMapping 경로의 조합된 목록을 표시합니다.
- `/shutdown`: 응용 프로그램을 정상적으로 종료할 수 있습니다(기본적으로 활성화되지 않음).
- `/restart`: 응용 프로그램을 다시 시작할 수 있습니다(기본적으로 활성화되어 있지 않음).



 Spring Boot Actuator는 이 기사에서 다루지 않은 다른 많은 기능을 제공합니다. 전체 기능 목록은 Spring Boot Actuator 설명서를 참조하세요.