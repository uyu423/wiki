---
title: 072: Understanding and Using the Spring Boot Starters
description: 
published: true
date: 2023-02-05T05:32:19.263Z
tags: 
editor: markdown
dateCreated: 2023-02-05T05:32:13.938Z
---

- [072: Comprensión y uso de los arrancadores Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/072-understanding-and-using-the-spring-boot-starters)
{.links-list}
- [072：了解和使用 Spring Boot Starters***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/072-understanding-and-using-the-spring-boot-starters)
{.links-list}
- [072: 스프링 부트 스타터 이해 및 사용***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/072-understanding-and-using-the-spring-boot-starters)
{.links-list}


# 072: Understanding and Using the Spring Boot Starters

The Spring Boot Starters are a set of convenient dependency descriptors which can be included in your application. By including one of these in your project, you get a set of well-configured, ready-to-use dependencies which you can use to get your project up and running quickly and easily.

In this post, we'll take a look at what the Spring Boot Starters are, how they work, and how you can use them in your own projects.

## What are the Spring Boot Starters?

The Spring Boot Starters are a set of dependency descriptors which can be included in your project. These descriptors define a set of well-configured, ready-to-use dependencies which can be used to get your project up and running quickly and easily.

The Spring Boot Starters are divided into two groups: the Core Starters and the Web Starters. The Core Starters are the dependencies which are required for any Spring Boot application. The Web Starters are the dependencies which are required for any Spring Boot application which will be exposing a web interface.

## How do the Spring Boot Starters work?

The Spring Boot Starters work by providing a set of well-configured, ready-to-use dependencies. These dependencies can be used to get your project up and running quickly and easily.

Including a Spring Boot Starter in your project will automatically include any dependencies which are required by that Starter. For example, including the `spring-boot-starter-web` Starter in your project will automatically include the `spring-boot-starter-tomcat` Starter, as the `spring-boot-starter-web` Starter depends on the `spring-boot-starter-tomcat` Starter.

## How can I use the Spring Boot Starters in my own project?

Including a Spring Boot Starter in your own project is easy. Simply add the appropriate dependency to your project's `pom.xml` file.

For example, to include the `spring-boot-starter-web` Starter in your project, you would add the following dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

## Conclusion

In this post, we've taken a look at what the Spring Boot Starters are, how they work, and how you can use them in your own projects.