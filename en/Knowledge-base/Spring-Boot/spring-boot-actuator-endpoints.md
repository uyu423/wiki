---
title: Spring Boot Actuator Endpoints
description: 
published: true
date: 2023-02-07T06:32:19.838Z
tags: 
editor: markdown
dateCreated: 2023-02-07T06:32:13.923Z
---

- [Puntos finales del actuador Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-actuator-endpoints)
{.links-list}
- [Spring Boot 执行器端点***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-actuator-endpoints)
{.links-list}
- [스프링 부트 액추에이터 끝점***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-actuator-endpoints)
{.links-list}


# Spring Boot Actuator Endpoints

Spring Boot Actuator Endpoints allow us to monitor and manage our Spring Boot application. In this article, we'll take a look at what these endpoints are and how we can use them.

## What is an Actuator Endpoint?

An Actuator Endpoint is a URL that is exposed by a Spring Boot application that can be used to monitor and manage the application. These endpoints provide information about the application, such as the health of the application, the version of the application, etc.

## Endpoints

There are several Actuator Endpoints that are available in Spring Boot. Some of these endpoints are:

### /info

This endpoint provides information about the application. This information is configured in the `application.properties` file.

### /health

This endpoint provides information about the health of the application. This information is gathered by the HealthIndicator beans that are registered in the application.

### /metrics

This endpoint provides information about the metrics of the application. This information is gathered by the Metrics beans that are registered in the application.

### /trace

This endpoint provides information about the traces of the application. This information is gathered by the TraceRepository beans that are registered in the application.

## Enabling Actuator Endpoints

Actuator Endpoints are not enabled by default in Spring Boot. We can enable them by adding the `spring-boot-actuator` dependency to our project.

## Security

We can secure our Actuator Endpoints by adding Spring Security to our project. We can do this by adding the `spring-boot-starter-security` dependency to our project.

## Conclusion

In this article, we've looked at what Spring Boot Actuator Endpoints are and how we can use them. We've also seen how we can enable and secure these endpoints.