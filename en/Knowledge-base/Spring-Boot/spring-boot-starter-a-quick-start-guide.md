---
title: Spring Boot Starter: A Quick Start Guide
description: 
published: true
date: 2023-02-17T18:02:32.733Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:31:10.377Z
---

- [Spring Boot Starter: 빠른 시작 가이드***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-starter-a-quick-start-guide)
{.links-list}


# Spring Boot Starter: A Quick Start Guide

With the ever-growing popularity of the [Spring Framework](https://spring.io/projects/spring-framework), it's no surprise that the [Spring Boot](https://spring.io/projects/spring-boot) project has also seen a rise in popularity. Spring Boot makes it easy to create stand-alone, production-grade Spring-based applications that you can "just run." 

In this article, we'll give you a quick start guide to [Spring Boot starters](https://docs.spring.io/spring-boot/docs/current/reference/html/using-boot-build-systems.html#using-boot-starter). We'll show you how starters can simplify your Maven or Gradle configuration. We'll also give you some examples of common starters that you might use. By the end of this article, you should have a good understanding of what starters are and how you can use them in your own applications.

## What is a Starter?

A starter is a template that contains all the dependencies that you need to get a particular task done. For example, if you want to build a web application, you might use the `web` starter. This starter would include all of the dependencies that you need for a web application, such as a web server, a template engine, and so on. 

Starters are designed to eliminate the need for you to manually manage dependencies. With a starter, you simply include the starter in your application, and the dependencies will be automatically managed for you. 

## Maven and Gradle Configuration

If you're using Maven, you can use starters by adding the following dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
</dependency>
```

If you're using Gradle, you can use starters by adding the following dependency to your `build.gradle` file:

```groovy
dependencies {
    compile group: 'org.springframework.boot', name: 'spring-boot-starter'
}
```

## Web Starter

The `web` starter is the most common starter used by Spring Boot applications. It includes all of the dependencies that you need to create a web application. This includes a web server, a template engine, and so on. 

The `web` starter also includes the `spring-boot-starter-tomcat` dependency. This dependency is used to provide an embedded Tomcat server. This is the server that will be used to run your web application. 

To use the `web` starter, add the following dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

Or, if you're using Gradle, add the following dependency to your `build.gradle` file:

```groovy
dependencies {
    compile group: 'org.springframework.boot', name: 'spring-boot-starter-web'
}
```

## JPA Starter

The `jpa` starter is used to add support for the Java Persistence API (JPA). JPA is a Java specification for accessing, persisting, and managing data in a relational database. 

The `jpa` starter includes the `hibernate-entitymanager` dependency. Hibernate is a popular JPA implementation. The `hibernate-entitymanager` dependency is used to provide a JPA implementation. 

To use the `jpa` starter, add the following dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

Or, if you're using Gradle, add the following dependency to your `build.gradle` file:

```groovy
dependencies {
    compile group: 'org.springframework.boot', name: 'spring-boot-starter-data-jpa'
}
```

## JDBC Starter

The `jdbc` starter is used to add support for the Java Database Connectivity API (JDBC). JDBC is a Java specification for accessing and managing data in a relational database. 

The `jdbc` starter includes the `tomcat-jdbc` dependency. Tomcat JDBC is a JDBC driver used to connect to a relational database. 

To use the `jdbc` starter, add the following dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
```

Or, if you're using Gradle, add the following dependency to your `build.gradle` file:

```groovy
dependencies {
    compile group: 'org.springframework.boot', name: 'spring-boot-starter-jdbc'
}
```

## Test Starter

The `test` starter is used to add support for testing Spring Boot applications. The `test` starter includes the `junit` and `mockito-core` dependencies. JUnit is a popular Java testing framework. Mockito is a popular Java mocking framework. 

To use the `test` starter, add the following dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
</dependency>
```

Or, if you're using Gradle, add the following dependency to your `build.gradle` file:

```groovy
dependencies {
    testCompile group: 'org.springframework.boot', name: 'spring-boot-starter-test'
}
```

## Conclusion

In this article, we've given you a quick start guide to Spring Boot starters. We've shown you how starters can simplify your Maven or Gradle configuration. We've also given you some examples of common starters that you might use. By the end of this article, you should have a good understanding of what starters are and how you can use them in your own applications.