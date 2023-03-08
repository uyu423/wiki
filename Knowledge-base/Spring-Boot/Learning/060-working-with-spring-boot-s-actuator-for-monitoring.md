---
title: 060: 모니터링을 위한 Spring Boot의 액추에이터 작업
description: 
published: true
date: 2023-02-04T23:32:25.116Z
tags: 
editor: markdown
dateCreated: 2023-02-04T23:32:23.531Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [060: Working with Spring Boot's Actuator for Monitoring***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/060-working-with-spring-boot-s-actuator-for-monitoring)
{.links-list}


# 모니터링을 위한 Spring Boot의 Actuator

Spring Boot의 Actuator는 Spring Boot 애플리케이션을 모니터링하고 관리하기 위한 훌륭한 도구입니다. 이 게시물에서는 Actuator를 사용하여 애플리케이션의 상태와 성능을 모니터링하는 방법을 살펴보겠습니다.

## 액츄에이터란?

Actuator는 애플리케이션을 모니터링하고 관리하는 데 도움이 되는 프로덕션 준비 기능을 제공하는 Spring Boot 모듈입니다. Actuator를 사용하면 애플리케이션의 상태와 성능을 모니터링하고 맞춤형 엔드포인트를 생성하여 애플리케이션 상태에 대한 정보를 얻을 수 있습니다.

## 액추에이터는 어떻게 사용하나요?

Spring Boot 애플리케이션에서 Actuator를 사용하려면 `pom.xml`에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

종속성을 추가하면 Actuator의 기능을 사용할 수 있습니다.

## 애플리케이션 상태 모니터링

Actuator의 가장 중요한 기능 중 하나는 애플리케이션의 상태를 모니터링하는 기능입니다. 기본적으로 Actuator는 애플리케이션의 상태를 확인하는 데 사용할 수 있는 `/health` 엔드포인트를 노출합니다.

`/health` 엔드포인트는 다음 값 중 하나를 가질 수 있는 `status` 속성을 반환합니다.

- `UP`: 애플리케이션이 실행 중입니다.
- `DOWN`: 애플리케이션이 다운되었습니다.
- `OUT_OF_SERVICE`: 애플리케이션이 서비스되지 않습니다.

`/health` 엔드포인트는 애플리케이션의 상태에 대한 자세한 정보가 포함된 `details` 속성도 반환합니다. 예를 들어 `details` 속성에는 애플리케이션의 데이터베이스 연결 또는 현재 실행 중인 스레드 수에 대한 정보가 포함될 수 있습니다.

`/health` 엔드포인트 외에도 Actuator는 애플리케이션에 대한 정보를 가져오는 데 사용할 수 있는 `/info` 엔드포인트도 노출합니다. `/info` 엔드포인트는 빌드의 버전 번호 및 타임스탬프와 같은 애플리케이션 빌드에 대한 정보가 포함된 `build` 속성을 반환합니다.

## 애플리케이션 성능 모니터링

응용 프로그램의 상태를 모니터링하는 것 외에도 Actuator는 응용 프로그램의 성능을 모니터링하는 데 도움이 될 수 있습니다. Actuator는 `/metrics`, `/dump` 및 `/trace`와 같은 여러 성능 관련 엔드포인트를 노출합니다.

`/metrics` 엔드포인트는 처리된 요청 수, 평균 응답 시간 및 발생한 오류 수와 같은 여러 성능 관련 메트릭을 반환합니다.

`/dump` 엔드포인트는 디버깅 목적에 유용할 수 있는 애플리케이션의 스레드 덤프를 반환합니다.

`/trace` 엔드포인트는 애플리케이션의 흐름을 이해하는 데 유용할 수 있는 애플리케이션의 추적을 반환합니다.

## 커스텀 엔드포인트 생성

기본 제공 끝점 외에도 Actuator를 사용하면 사용자 지정 끝점을 만들 수도 있습니다. 사용자 지정 끝점을 만들려면 `Endpoint` 인터페이스를 구현하는 클래스를 만들어야 합니다.

예를 들어 다음 클래스는 `message` 속성을 반환하는 사용자 정의 `/myendpoint` 엔드포인트를 생성합니다.

```java
@Component
public class MyEndpoint implements Endpoint<Map<String, String>> {

    @Override
    public String getId() {
        return "/myendpoint";
    }

    @Override
    public Map<String, String> invoke() {
        Map<String, String> result = new HashMap<>();
        result.put("message", "Hello, world!");
        return result;
    }

    @Override
    public boolean isSensitive() {
        return false;
    }

}
```

## 결론

이 게시물에서는 Spring Boot의 Actuator를 사용하여 애플리케이션을 모니터링하는 방법을 살펴보았습니다. 액추에이터는 애플리케이션의 상태와 성능을 모니터링하기 위한 훌륭한 도구입니다. 또한 Actuator를 사용하면 애플리케이션에 대한 정보를 얻기 위해 사용자 지정 끝점을 만들 수 있습니다.