---
title: 079: Spring Boot 애플리케이션에서 비동기 처리 구현
description: 
published: true
date: 2023-02-05T10:32:15.843Z
tags: 
editor: markdown
dateCreated: 2023-02-05T10:32:14.253Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [079: Implementing Asynchronous Processing in a Spring Boot Application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/079-implementing-asynchronous-processing-in-a-spring-boot-application)
{.links-list}


# 079: Spring Boot 애플리케이션에서 비동기 처리 구현

비동기 처리는 병렬 또는 비차단 방식으로 작업을 처리하는 방법입니다. Spring Boot 애플리케이션에서 비동기 처리를 사용하여 장기 실행 작업을 별도의 스레드로 오프로드하여 성능을 향상시킬 수 있습니다.

이 게시물에서는 Spring Boot 애플리케이션에서 비동기 처리를 구현하는 방법을 살펴보겠습니다. Spring Boot에서 사용할 수 있는 다양한 유형의 비동기 처리를 살펴보는 것으로 시작하겠습니다. 그런 다음 비동기 처리를 사용하도록 Spring Boot를 구성하는 방법을 살펴보겠습니다. 마지막으로 Spring Boot 애플리케이션에서 비동기 처리를 사용하기 위한 몇 가지 팁을 살펴보겠습니다.

## 비동기 처리 유형

Spring Boot에서 사용할 수 있는 두 가지 유형의 비동기 처리가 있습니다.

* 병렬 처리: 작업이 병렬로 실행되는 일종의 비동기 처리입니다. 병렬 처리는 작업을 여러 스레드에 분산하여 장기 실행 작업의 성능을 향상시키는 데 사용할 수 있습니다.

* Non-blocking 처리: 작업이 non-blocking 방식으로 실행되는 일종의 비동기 처리입니다. 비차단 처리는 장기 실행 작업이 완료될 때까지 기다릴 필요가 없도록 하여 애플리케이션의 응답성을 향상시키는 데 사용할 수 있습니다.

## 비동기 처리 구성

Spring Boot 애플리케이션에서 비동기 처리를 사용하려면 태스크 실행기를 사용하도록 애플리케이션을 구성해야 합니다. 작업 실행기는 병렬 또는 비차단 방식으로 작업을 실행하는 구성 요소입니다.

Spring Boot는 다양한 유형의 비동기 처리에 사용할 수 있는 다양한 작업 실행기를 제공합니다. 예를 들어 SimpleAsyncTaskExecutor는 병렬 처리에 사용할 수 있고 CallableProcessingInterceptor는 비차단 처리에 사용할 수 있습니다.

작업 실행기를 사용하도록 애플리케이션을 구성하려면 다음 속성을 application.properties 파일에 추가해야 합니다.

spring.task.executor.pool.size=10

이 속성은 작업 실행기 풀의 크기를 구성합니다. 작업 실행자 풀은 병렬 또는 비차단 방식으로 작업을 실행하는 데 사용됩니다.

## 비동기 처리 사용 팁

Spring Boot 애플리케이션에서 비동기 처리를 사용할 때 염두에 두어야 할 몇 가지 사항이 있습니다.

* 동기 방식 사용 금지: 비동기 처리를 사용하는 경우 동기 방식을 사용하지 마십시오. 동기 메서드는 작업을 실행 중인 스레드를 차단할 수 있으므로 작업을 완료하는 데 시간이 오래 걸릴 수 있습니다.

* 태스크 실행자 사용: 비동기 처리를 사용할 때 반드시 태스크 실행자를 사용하십시오. 작업 실행자는 작업을 여러 스레드에 분산하여 장기 실행 작업의 성능을 향상시키는 데 도움이 될 수 있습니다.

* 콜백 사용 : 비동기 처리 사용 시 반드시 콜백을 사용하세요. 콜백은 장기 실행 작업이 완료될 때까지 기다릴 필요가 없도록 하여 애플리케이션의 응답성을 개선하는 데 도움이 될 수 있습니다.