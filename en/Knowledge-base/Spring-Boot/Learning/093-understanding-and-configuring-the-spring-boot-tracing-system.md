---
title: 093: Understanding and Configuring the Spring Boot Tracing System
description: 
published: true
date: 2023-02-04T20:55:21.150Z
tags: 
editor: markdown
dateCreated: 2023-02-04T20:55:15.928Z
---

- [093: comprensión y configuración del sistema de seguimiento Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/093-understanding-and-configuring-the-spring-boot-tracing-system)
{.links-list}
- [093：了解和配置 Spring Boot 跟踪系统***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/093-understanding-and-configuring-the-spring-boot-tracing-system)
{.links-list}
- [093: 스프링 부트 추적 시스템 이해 및 구성***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/093-understanding-and-configuring-the-spring-boot-tracing-system)
{.links-list}


# 093: Understanding and Configuring the Spring Boot Tracing System

Spring Boot provides a tracing system that can be used to collect and view information about the requests that are flowing through a system. This can be useful for debugging purposes, or for monitoring the performance of a system.

In this post, we'll take a look at how to configure the Spring Boot tracing system, and how to use it to collect information about request processing.

## Configuring the Spring Boot Tracing System

The Spring Boot tracing system is configured using the `spring.sleuth` property in the `application.properties` file. The following properties can be used to configure the tracing system:

- `spring.sleuth.sampler.probability`: The probability that a request will be sampled. The default value is 1.0, which means that all requests will be sampled.

- `spring.sleuth.sampler.spans`: The maximum number of spans that can be created for a single request. The default value is 100.

- `spring.sleuth.trace-id128`: If set to true, 128-bit trace IDs will be generated. The default value is false.

- `spring.sleuth.web.skip-pattern`: A regular expression that is used to determine which requests should not be traced. The default value is `/health`

More information about these properties can be found in the [Spring Boot documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-tracing.html#boot-features-tracing-spring-sleuth).

## Collecting Tracing Information

The Spring Boot tracing system can be used to collect information about request processing. This information can be collected in two ways:

- By logging the information to a file
- By sending the information to a [Zipkin](https://zipkin.io/) server

### Logging Tracing Information to a File

The Spring Boot tracing system can be configured to log tracing information to a file. This can be done by setting the `spring.sleuth.log.file` property in the `application.properties` file. The following is an example of how to configure the tracing system to log information to a file:

```
spring.sleuth.log.file=traces.log
```

### Sending Tracing Information to a Zipkin Server

The Spring Boot tracing system can be configured to send tracing information to a Zipkin server. This can be done by setting the `spring.sleuth.zipkin.baseUrl` property in the `application.properties` file. The following is an example of how to configure the tracing system to send information to a Zipkin server:

```
spring.sleuth.zipkin.baseUrl=http://localhost:9411
```

## Viewing Tracing Information

### Logging Tracing Information to a File

If the tracing system is configured to log information to a file, the information can be viewed by opening the file in a text editor. The information will be logged in the [JSON](https://www.json.org/) format.

### Sending Tracing Information to a Zipkin Server

If the tracing system is configured to send information to a Zipkin server, the information can be viewed by opening the Zipkin server in a web browser. The Zipkin server will provide a graphical interface for viewing the tracing information.

## Conclusion

In this post, we've looked at how to configure the Spring Boot tracing system, and how to use it to collect information about request processing. We've also seen how to view the tracing information that is collected by the system.