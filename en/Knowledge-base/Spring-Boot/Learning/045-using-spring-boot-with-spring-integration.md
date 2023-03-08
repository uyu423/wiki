---
title: 045: Using Spring Boot with Spring Integration
description: 
published: true
date: 2023-02-04T11:32:20.741Z
tags: 
editor: markdown
dateCreated: 2023-02-04T11:32:15.442Z
---

- [045: Uso de Spring Boot con Spring Integration***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/045-using-spring-boot-with-spring-integration)
{.links-list}
- [045：将 Spring Boot 与 Spring Integration 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/045-using-spring-boot-with-spring-integration)
{.links-list}
- [045: Spring 통합과 함께 Spring Boot 사용***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/045-using-spring-boot-with-spring-integration)
{.links-list}


# Using Spring Boot with Spring Integration

In this post, we'll take a look at how to use Spring Boot with Spring Integration. We'll go over the basics of Spring Integration and show how to use it with Spring Boot.

## What is Spring Integration?

Spring Integration is a framework that extends the Spring Framework to provide support for enterprise integration patterns. These patterns are used to facilitate the communication between different applications and systems. 

Spring Integration provides adapters for a variety of different technologies, such as JMS, HTTP, and FTP. It also provides support for message channels, message routers, and message transformers.

## Why use Spring Integration?

Spring Integration enables you to build enterprise-scale applications that are resilient and scalable. It helps you to avoid vendor lock-in by providing a consistent programming model across different technologies.

## Getting Started

In this section, we'll show you how to get started with Spring Integration. We'll go over the different dependencies that you'll need and show you how to configure Spring Integration.

### Dependencies

First, you'll need to add the following dependencies to your project:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-integration</artifactId>
    </dependency>
</dependencies>
```

These dependencies will pull in the necessary jars for Spring Integration.

### Configuration

Next, you'll need to configure Spring Integration. You can do this by adding the following to your `application.properties` file:

```properties
spring.integration.dsl.enabled=true
```

This will enable the Spring Integration Java DSL.

## Conclusion

In this post, we've taken a look at how to use Spring Boot with Spring Integration. We've gone over the basics of Spring Integration and shown how to get started with it.