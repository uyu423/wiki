---
title: 041: Using Spring Boot with Apache Storm
description: 
published: true
date: 2023-02-04T07:32:23.253Z
tags: 
editor: markdown
dateCreated: 2023-02-04T07:32:17.930Z
---

- [041: Uso de Spring Boot con Apache Storm***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/041-using-spring-boot-with-apache-storm)
{.links-list}
- [041：将 Spring Boot 与 Apache Storm 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/041-using-spring-boot-with-apache-storm)
{.links-list}
- [041: 아파치 스톰과 함께 스프링 부트 사용하기***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/041-using-spring-boot-with-apache-storm)
{.links-list}


# Using Spring Boot with Apache Storm

In this post, we'll learn how to use Spring Boot with Apache Storm. We'll cover the following topics:

* What is Apache Storm?
* What is Spring Boot?
* How to use Spring Boot with Apache Storm

## What is Apache Storm?

Apache Storm is a free and open source distributed real-time computation system. Storm makes it easy to reliably process unbounded streams of data, doing for real-time processing what Hadoop did for batch processing.

Storm is simple, can be used with any programming language, and is a lot of fun to use!

## What is Spring Boot?

Spring Boot is a framework for easily creating stand-alone, production-grade Spring-based Applications that you can "just run". We take an opinionated view of the Spring platform and third-party libraries so you can get started with minimum fuss. Most Spring Boot applications need very little Spring configuration.

## How to use Spring Boot with Apache Storm

Now that we know what Storm and Spring Boot are, let's see how to use them together.

The first thing we need is a Maven dependency for Storm:

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>1.1.1</version>
    <scope>provided</scope>
</dependency>
```

We also need a dependency for Spring Boot:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

Now we can create a Spring Boot application:

```java
@SpringBootApplication
public class StormApplication {

    public static void main(String[] args) {
        SpringApplication.run(StormApplication.class, args);
    }

}
```

We can now create a Storm topology in our application:

```java
@Component
public class MyTopology {

    @Autowired
    private TopologyBuilder topologyBuilder;

    @PostConstruct
    public void init() {
        // ...
    }

}
```

And that's it! We now have a working Storm topology within our Spring Boot application.

## Additional Information

* For more information on Apache Storm, see the [Apache Storm website](https://storm.apache.org/).
* For more information on Spring Boot, see the [Spring Boot website](https://projects.spring.io/spring-boot/).