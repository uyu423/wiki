---
title: Deploying Spring Boot Applications: Best Practices
description: 
published: true
date: 2023-02-17T18:02:41.008Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:59:25.893Z
---

- [Spring Boot 애플리케이션 배포: 모범 사례***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/deploying-spring-boot-applications-best-practices)
{.links-list}
- [Spring Boot アプリケーションのデプロイ: ベスト プラクティス***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/deploying-spring-boot-applications-best-practices)
{.links-list}
- [部署 Spring Boot 应用程序：最佳实践***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/deploying-spring-boot-applications-best-practices)
{.links-list}
 


# Deploying Spring Boot Applications: Best Practices

Spring Boot is a popular Java web framework that makes it easy to create production-grade, stand-alone Spring-based applications. In this article, we'll discuss some of the best practices for deploying Spring Boot applications.

## Table of Contents

1. [Creating a Spring Boot Application](#creating-a-spring-boot-application)
2. [Deploying a Spring Boot Application](#deploying-a-spring-boot-application)
    1. [Architecture](#architecture)
    2. [Web Servers](#web-servers)
3. [Conclusion](#conclusion)

## Creating a Spring Boot Application

Creating a Spring Boot application is simple. All you need is Java and a text editor. Spring Boot applications are typically packaged as jar files and can be run using the `java -jar` command. For example, the following command will start a Spring Boot application running on port 8080:

```java
java -jar my-spring-boot-app.jar
```

If you're using Maven, you can also use the `spring-boot:run` goal:

```
mvn spring-boot:run
```

You can also create a Spring Boot application using the Spring Initializr. The Spring Initializr is a web application that can generate a Spring Boot application based on your selections. Simply select the dependencies you want, and the Initializr will generate a project with those dependencies.

## Deploying a Spring Boot Application

Deploying a Spring Boot application is easy. Unlike traditional Java web applications, there is no need to configure a servlet container or application server. However, there are a few things to keep in mind when deploying a Spring Boot application.

### Architecture

Spring Boot applications are typically deployed as stand-alone jar files. This makes it easy to deploy and run Spring Boot applications on any platform that supports Java.

Spring Boot applications can also be deployed as war files. However, this is not the recommended deployment approach, as it requires a servlet container or application server to run the application.

### Web Servers

Spring Boot applications can be deployed to a variety of web servers. The most popular options are Apache Tomcat and Jetty.

Tomcat is the most widely used web server for Java applications. Tomcat is a servlet container, and can run War files. Tomcat is available as both a standalone server and an embeddable servlet container.

Jetty is a widely used open source web server. Jetty is a servlet container, and can run War files. Jetty is available as both a standalone server and an embeddable servlet container.

## Conclusion

Deploying a Spring Boot application is easy. Spring Boot applications can be deployed to a variety of web servers, and do not require a servlet container or application server.