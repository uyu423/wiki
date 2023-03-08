---
title: 003: Understanding Spring Boot auto-configuration
description: 
published: true
date: 2023-02-03T07:17:20.302Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:17:15.505Z
---

- [003: comprensión de la configuración automática de Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/003-understanding-spring-boot-auto-configuration)
{.links-list}
- [003：了解Spring Boot自动配置***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/003-understanding-spring-boot-auto-configuration)
{.links-list}
- [003: Spring Boot 자동 구성 이해***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/003-understanding-spring-boot-auto-configuration)
{.links-list}


##Understanding Spring Boot auto-configuration

Spring Boot auto-configuration is a feature that automatically configures Spring applications based on the dependencies present in the project. This means that, for example, if Hibernate is on the classpath, Spring Boot will automatically set up a DataSource and entity manager factory.

The auto-configuration feature is enabled by default in Spring Boot. However, it can be disabled by setting the spring.boot.autoconfigure.EnableAutoConfiguration property to false.

When auto-configuration is enabled, Spring Boot will attempt to configure the application based on the dependencies present in the project. For example, if Hibernate is on the classpath, Spring Boot will automatically configure a DataSource and entity manager factory.

Auto-configuration can be a useful feature when you are getting started with Spring Boot. However, as your application grows, you will likely want to disable auto-configuration for certain parts of the application.

For more information on Spring Boot auto-configuration, see the following resources:

- [The auto-configuration feature in Spring Boot](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-auto-configuration.html)

- [Disabling auto-configuration in Spring Boot](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-auto-configuration.html#boot-features-auto-configuration-exclude)