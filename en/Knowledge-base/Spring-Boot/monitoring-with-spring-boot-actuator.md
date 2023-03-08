---
title: Monitoring with Spring Boot Actuator
description: 
published: true
date: 2023-02-07T01:32:50.955Z
tags: 
editor: markdown
dateCreated: 2023-02-07T01:32:45.197Z
---

- [Supervisión con actuador Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/monitoring-with-spring-boot-actuator)
{.links-list}
- [使用 Spring Boot Actuator 进行监控***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/monitoring-with-spring-boot-actuator)
{.links-list}
- [Spring Boot Actuator로 모니터링***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/monitoring-with-spring-boot-actuator)
{.links-list}



# Monitoring with Spring Boot Actuator

Spring Boot Actuator is a sub-project of the Spring Boot framework that provides production-ready features to help you monitor and manage your application. It also helps you to audited and health information about your application. Spring Boot Actuator is not enabled by default. You need to use the `@EnableAutoConfiguration` or `@SpringBootApplication` annotations to enable it.

## Enabling Spring Boot Actuator

To enable Spring Boot Actuator in your Spring Boot application, you need to add the `spring-boot-starter-actuator` dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

You can also enable Spring Boot Actuator in your application by adding the following properties to your `application.properties` file:

```properties
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
```

## Monitoring with Spring Boot Actuator

Spring Boot Actuator provides a number of production-ready endpoints that you can use to monitor and manage your application. The following table lists the most important endpoints:

| Endpoint | Description |
| --- | --- |
| `/health` | Displays application health information (defaults to `UP`). |
| `/info` | Displays arbitrary application info. |
| `/metrics` | Displays application metrics information. |
| `/trace` | Displays application trace information. |
| `/dump` | Performs a thread dump. |
| `/jolokia` | Exposes JMX beans over HTTP (requires `jolokia-core`). |
| `/logfile` | Returns the contents of the logfile (if logging is configured). |
| `/refresh` | Refresh application and configuration caches. |
| `/flyway` | Shows any Flyway database migrations that have been applied. |
| `/liquibase` | Shows any Liquibase database migrations that have been applied. |

The `/health` and `/info` endpoints are secured by default. To make them publicly accessible, you need to add the following properties to your `application.properties` file:

```properties
management.security.enabled=false
```

## Customizing Spring Boot Actuator

Spring Boot Actuator provides a number of ways that you can customize its behavior.

### Changing the Management Server Port

By default, Spring Boot Actuator uses port `8080` for the management server. You can change this by adding the following property to your `application.properties` file:

```properties
management.server.port=<port>
```

### Changing the Management Server Path

By default, Spring Boot Actuator uses the `/actuator` path for the management server. You can change this by adding the following property to your `application.properties` file:

```properties
management.server.servlet.path=/<path>
```

### Changing the Endpoint IDs

By default, Spring Boot Actuator uses the endpoint IDs from the table above. You can change these by adding the following property to your `application.properties` file:

```properties
management.endpoints.web.exposure.include=<endpoint1>,<endpoint2>,...
```

### Changing the Endpoint Paths

By default, Spring Boot Actuator uses the endpoint paths from the table above. You can change these by adding the following property to your `application.properties` file:

```properties
management.endpoint.<endpoint>.path=/<path>
```

### Changing the Endpoint Sensitive Information

By default, Spring Boot Actuator exposes sensitive information in the endpoint response bodies. You can change this by adding the following property to your `application.properties` file:

```properties
management.endpoint.health.show-details=<value>
```

Where `<value>` can be one of the following:

| Value | Description |
| --- | --- |
| `always` | Always show details. |
| `never` | Never show details. |
| `when_authorized` | Show details when the user is authorized. |

### Changing the Endpoint Security

By default, Spring Boot Actuator uses HTTP Basic authentication for the endpoints. You can change this by adding the following property to your `application.properties` file:

```properties
management.security.enabled=false
```

### Changing the Endpoint Username and Password

By default, Spring Boot Actuator uses the username `user` and password `password` for the endpoints. You can change these by adding the following properties to your `application.properties` file:

```properties
management.security.user.name=<username>
management.security.user.password=<password>
```

## Conclusion

In this article, we've looked at how to use the Spring Boot Actuator to monitor and manage your application. We've also seen how to customize the Actuator's behavior.