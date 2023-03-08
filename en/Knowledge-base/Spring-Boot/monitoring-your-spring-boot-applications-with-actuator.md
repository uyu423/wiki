---
title: Monitoring Your Spring Boot Applications with Actuator
description: 
published: true
date: 2023-02-17T18:02:47.784Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:16:13.717Z
---

- [Actuator로 Spring Boot 애플리케이션 모니터링***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/monitoring-your-spring-boot-applications-with-actuator)
{.links-list}
- [アクチュエーターを使用した Spring Boot アプリケーションのモニタリング***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/monitoring-your-spring-boot-applications-with-actuator)
{.links-list}
- [使用 Actuator 监控您的 Spring Boot 应用程序***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/monitoring-your-spring-boot-applications-with-actuator)
{.links-list}


# Monitoring Your Spring Boot Applications with Actuator

Monitoring is a key aspect of any application, and Spring Boot provides a simple way to monitor your application using Actuator. Actuator is a Spring Boot module that provides various monitoring and management endpoints. In this article, we'll take a look at how to use Actuator to monitor your Spring Boot application.

## Enabling Actuator Endpoints

To use Actuator, you need to add the `spring-boot-actuator` dependency to your project. You can add this dependency to your `pom.xml` file:

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-actuator</artifactId>
  <version>2.1.2.RELEASE</version>
</dependency>
```

Once you've added the dependency, you can enable Actuator endpoints by adding the `@EnableActuator` annotation to your `@SpringBootApplication` class:

```java
@SpringBootApplication
@EnableActuator
public class Application {

  public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
  }
}
```

## Monitoring Your Application

Once Actuator is enabled, you can access the Actuator endpoints by navigating to `http://localhost:8080/{context-path}/actuator`. The `{context-path}` is the context path of your application. For example, if your application is running on `http://localhost:8080/my-app`, you can access the Actuator endpoints at `http://localhost:8080/my-app/actuator`.

The Actuator endpoints enable you to monitor your application in several ways. For example, you can monitor the application's health, metric data, configuration, and so on. 

### Monitoring Application Health

The `health` endpoint provides information about the health of your application. To access the `health` endpoint, navigate to `http://localhost:8080/{context-path}/actuator/health`.

The `health` endpoint returns information about the health of your application in JSON format. The JSON format contains the following information:

- `status`: The status of the application. The possible values are `UP` or `DOWN`.
- `details`: The health details of the application. The health details contains information about the individual components of the application.

The following is an example `health` endpoint response:

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

### Monitoring Application Metrics

The `metrics` endpoint provides information about the metrics of your application. To access the `metrics` endpoint, navigate to `http://localhost:8080/{context-path}/actuator/metrics`.

The `metrics` endpoint returns information about the metrics of your application in JSON format. The JSON format contains the following information:

- `names`: The names of the metrics.
- `values`: The values of the metrics.

The following is an example `metrics` endpoint response:

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

### Monitoring Application Configuration

The `configprops` endpoint provides information about the configuration properties of your application. To access the `configprops` endpoint, navigate to `http://localhost:8080/{context-path}/actuator/configprops`.

The `configprops` endpoint returns information about the configuration properties of your application in JSON format. The JSON format contains the following information:

- `propertySources`: The property sources of the application.

The following is an example `configprops` endpoint response:

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

## Conclusion

In this article, we've looked at how to use Actuator to monitor your Spring Boot application. Actuator provides a simple and powerful way to monitor your application. By using the Actuator endpoints, you can get detailed information about the health, metrics, and configuration of your application.