---
title: 011: Actuator로 Spring Boot 애플리케이션 모니터링 및 관리
description: 
published: true
date: 2023-02-03T09:04:41.913Z
tags: 
editor: markdown
dateCreated: 2023-02-03T09:04:36.913Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [011: Monitoring and managing a Spring Boot application with Actuator***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/011-monitoring-and-managing-a-spring-boot-application-with-actuator)
{.links-list}


# Actuator로 Spring Boot 애플리케이션 모니터링 및 관리

Actuator는 Spring Boot 애플리케이션을 모니터링하고 관리하는 데 사용할 수 있는 도구입니다. 다음을 포함하여 애플리케이션을 모니터링하고 관리하는 데 사용할 수 있는 여러 기능을 제공합니다.

- 건강 체크
- 지표
- 로깅
- 구성
- 끝점

이 게시물에서는 Actuator를 사용하여 Spring Boot 애플리케이션을 모니터링하고 관리하는 데 중점을 둘 것입니다. 먼저 Spring Boot 애플리케이션에서 Actuator를 구성하는 방법을 살펴보겠습니다. 그런 다음 Actuator의 상태 확인 기능을 사용하여 애플리케이션의 상태를 모니터링하는 방법을 살펴보겠습니다. 마지막으로 Actuator의 메트릭 기능을 사용하여 애플리케이션의 성능을 모니터링하는 방법을 살펴보겠습니다.

## Spring Boot 애플리케이션에서 Actuator 구성

Actuator는 Spring Boot 애플리케이션에서 기본적으로 활성화되지 않습니다. Actuator를 활성화하려면 프로젝트에 다음 종속성을 추가해야 합니다.

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

종속성을 추가한 후에는 application.properties 파일에 다음 속성을 추가하여 Actuator를 활성화할 수 있습니다.

```
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
```

첫 번째 속성인 management.endpoints.web.exposure.include는 모든 Actuator 끝점을 노출합니다. 두 번째 속성인 management.endpoint.health.show-details는 상태 확인 엔드포인트에 애플리케이션 상태에 대한 자세한 정보가 포함되도록 합니다.

## 액추에이터의 건강 체크 기능 사용하기

Actuator의 상태 확인 기능을 사용하여 애플리케이션의 상태를 모니터링할 수 있습니다. 기본적으로 Actuator는 데이터베이스, 디스크 공간 및 JMS에 대한 검사를 포함하여 다양한 내장 상태 검사를 제공합니다.

내장된 상태 확인 외에도 자체 사용자 지정 상태 확인을 추가할 수도 있습니다. 사용자 지정 상태 확인을 추가하려면 HealthIndicator 인터페이스를 구현하는 클래스를 만들어야 합니다. 예를 들어 다음 클래스는 MyService라는 서비스에 대한 상태 확인을 구현합니다.

```java
public class MyServiceHealthIndicator implements HealthIndicator {

   @Override
   public Health health() {
      // check the health of our service
      // if the service is healthy, return a Health.Builder with a status of UP
      // if the service is not healthy, return a Health.Builder with a status of DOWN
   }
}
```

사용자 지정 상태 확인을 만든 후에는 Spring에 등록해야 합니다. 클래스에 @Component 주석을 추가하여 이를 수행할 수 있습니다. 예를 들어:

```java
@Component
public class MyServiceHealthIndicator implements HealthIndicator {

   @Override
   public Health health() {
      // check the health of our service
      // if the service is healthy, return a Health.Builder with a status of UP
      // if the service is not healthy, return a Health.Builder with a status of DOWN
   }
}
```

## Actuator의 측정 기능 사용

액추에이터의 메트릭 기능을 사용하여 애플리케이션의 성능을 모니터링할 수 있습니다. 기본적으로 Actuator는 데이터베이스, JMS 및 웹 요청에 대한 메트릭을 포함하여 여러 내장 메트릭을 제공합니다.

기본 제공 메트릭 외에도 고유한 사용자 정의 메트릭을 추가할 수 있습니다. 사용자 지정 메트릭을 추가하려면 MetricWriter 인터페이스를 구현하는 클래스를 만들어야 합니다. 예를 들어 다음 클래스는 MyService라는 서비스에 대한 메트릭을 구현합니다.

```java
public class MyServiceMetricWriter implements MetricWriter {

   @Override
   public void write(Metric<?> metric) {
      // write the metric to our monitoring system
   }
}
```

사용자 지정 메트릭을 만든 후에는 Spring에 등록해야 합니다. 클래스에 @Component 주석을 추가하여 이를 수행할 수 있습니다. 예를 들어:

```java
@Component
public class MyServiceMetricWriter implements MetricWriter {

   @Override
   public void write(Metric<?> metric) {
      // write the metric to our monitoring system
   }
}
```

## 결론

이번 포스트에서는 Actuator를 사용하여 Spring Boot 애플리케이션을 모니터링하고 관리하는 방법을 살펴보았습니다. Spring Boot 애플리케이션에서 Actuator를 구성하는 방법과 Actuator의 상태 확인 및 메트릭 기능을 사용하여 애플리케이션의 상태와 성능을 모니터링하는 방법을 살펴보았습니다.