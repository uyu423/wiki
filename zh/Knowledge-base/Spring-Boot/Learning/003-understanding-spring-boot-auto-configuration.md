---
title: 003：了解Spring Boot自动配置
description: 
published: true
date: 2023-02-03T07:17:17.080Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:17:15.499Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [003: Understanding Spring Boot auto-configuration***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/003-understanding-spring-boot-auto-configuration)
{.links-list}


## 了解 Spring Boot 自动配置

Spring Boot 自动配置是一种基于项目中存在的依赖项自动配置 Spring 应用程序的功能。这意味着，例如，如果 Hibernate 在类路径上，Spring Boot 将自动设置数据源和实体管理器工厂。

自动配置功能在 Spring Boot 中默认启用。但是，可以通过将 spring.boot.autoconfigure.EnableAutoConfiguration 属性设置为 false 来禁用它。

启用自动配置后，Spring Boot 将尝试根据项目中存在的依赖项配置应用程序。例如，如果 Hibernate 在类路径上，Spring Boot 将自动配置数据源和实体管理器工厂。

当您开始使用 Spring Boot 时，自动配置可能是一个有用的功能。但是，随着应用程序的增长，您可能希望禁用应用程序某些部分的自动配置。

有关 Spring Boot 自动配置的更多信息，请参阅以下资源：

- [Spring Boot 中的自动配置功能](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-auto-configuration.html)

- [在 Spring Boot 中禁用自动配置](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-auto-configuration.html# boot-features-auto -配置排除）