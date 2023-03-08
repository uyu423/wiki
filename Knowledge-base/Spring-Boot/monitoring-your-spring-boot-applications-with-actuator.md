---
title: Actuator로 Spring Boot 애플리케이션 모니터링
description: 
published: true
date: 2023-02-17T18:02:50.454Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:16:13.720Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Monitoring Your Spring Boot Applications with Actuator***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/monitoring-your-spring-boot-applications-with-actuator)
{.links-list}


# Actuator로 Spring Boot 애플리케이션 모니터링

모니터링은 모든 애플리케이션의 핵심 측면이며 Spring Boot는 Actuator를 사용하여 애플리케이션을 모니터링하는 간단한 방법을 제공합니다. Actuator는 다양한 모니터링 및 관리 엔드포인트를 제공하는 Spring Boot 모듈입니다. 이 기사에서는 Actuator를 사용하여 Spring Boot 애플리케이션을 모니터링하는 방법을 살펴보겠습니다.

## 액추에이터 엔드포인트 활성화

Actuator를 사용하려면 프로젝트에 `spring-boot-actuator` 종속성을 추가해야 합니다. 이 종속성을 `pom.xml` 파일에 추가할 수 있습니다.

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-actuator</artifactId>
  <version>2.1.2.RELEASE</version>
</dependency>
```

종속성을 추가한 후에는 `@EnableActuator` 주석을 `@SpringBootApplication` 클래스에 추가하여 Actuator 엔드포인트를 활성화할 수 있습니다.

```java
@SpringBootApplication
@EnableActuator
public class Application {

  public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
  }
}
```

## 애플리케이션 모니터링

Actuator가 활성화되면 `http://localhost:8080/{context-path}/actuator`로 이동하여 Actuator 엔드포인트에 액세스할 수 있습니다. `{context-path}`는 애플리케이션의 컨텍스트 경로입니다. 예를 들어 애플리케이션이 `http://localhost:8080/my-app`에서 실행 중인 경우 `http://localhost:8080/my-app/actuator`에서 Actuator 엔드포인트에 액세스할 수 있습니다.

액추에이터 엔드포인트를 사용하면 여러 가지 방법으로 애플리케이션을 모니터링할 수 있습니다. 예를 들어 애플리케이션의 상태, 메트릭 데이터, 구성 등을 모니터링할 수 있습니다.

### 애플리케이션 상태 모니터링

'health' 엔드포인트는 애플리케이션의 상태에 대한 정보를 제공합니다. `health` 엔드포인트에 액세스하려면 `http://localhost:8080/{context-path}/actuator/health`로 이동합니다.

'health' 엔드포인트는 애플리케이션의 상태에 대한 정보를 JSON 형식으로 반환합니다. JSON 형식에는 다음 정보가 포함됩니다.

- `상태`: 애플리케이션의 상태입니다. 가능한 값은 'UP' 또는 'DOWN'입니다.
- `details`: 애플리케이션의 상태 세부 정보입니다. 상태 세부 정보에는 애플리케이션의 개별 구성 요소에 대한 정보가 포함되어 있습니다.

다음은 `health` 엔드포인트 응답의 예입니다.

```json
{
  "status": "UP",
  "details": {
    "diskSpace": {
      "status": "UP",
      "details": {
        "total":49989655552,
        "free":3246466048,
        "threshold":10485760
      }
    }
  }
}
```

### 애플리케이션 지표 모니터링

`metrics` 엔드포인트는 애플리케이션의 메트릭에 대한 정보를 제공합니다. `metrics` 엔드포인트에 액세스하려면 `http://localhost:8080/{context-path}/actuator/metrics`로 이동합니다.

`metrics` 엔드포인트는 애플리케이션의 메트릭에 대한 정보를 JSON 형식으로 반환합니다. JSON 형식에는 다음 정보가 포함됩니다.

- `names`: 메트릭의 이름입니다.
- `values`: 메트릭 값입니다.

다음은 `metrics` 엔드포인트 응답의 예입니다.

```json
{
  "names": [
    "jvm.memory.max",
    "jvm.memory.used"
  ],
  "values": {
    "jvm.memory.max":49989655552,
    "jvm.memory.used":3246466048
  }
}
```

### 애플리케이션 구성 모니터링

`configprops` 엔드포인트는 애플리케이션의 구성 속성에 대한 정보를 제공합니다. `configprops` 엔드포인트에 액세스하려면 `http://localhost:8080/{context-path}/actuator/configprops`로 이동합니다.

`configprops` 엔드포인트는 애플리케이션의 구성 속성에 대한 정보를 JSON 형식으로 반환합니다. JSON 형식에는 다음 정보가 포함됩니다.

- `propertySources`: 애플리케이션의 속성 소스입니다.

다음은 `configprops` 엔드포인트 응답의 예입니다.

```json
{
  "propertySources": [
    {
      "name": "application.properties",
      "properties": {
        "server.port": "8080",
        "spring.application.name": "demo"
      }
    },
    {
      "name": "systemProperties",
      "properties": {
        "java.runtime.name": "OpenJDK Runtime Environment",
        "sun.boot.library.path": "/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.131-3.b12.el7_3.x86_64/jre/lib/boot",
        ...
      }
    },
    ...
  ]
}
```

## 결론

이 기사에서는 Actuator를 사용하여 Spring Boot 애플리케이션을 모니터링하는 방법을 살펴보았습니다. Actuator는 애플리케이션을 모니터링하는 간단하고 강력한 방법을 제공합니다. 액추에이터 엔드포인트를 사용하면 애플리케이션의 상태, 메트릭 및 구성에 대한 자세한 정보를 얻을 수 있습니다.