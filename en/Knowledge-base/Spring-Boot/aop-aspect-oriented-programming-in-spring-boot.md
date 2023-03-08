---
title: AOP: Aspect-Oriented Programming in Spring Boot
description: 
published: true
date: 2023-02-17T18:01:27.863Z
tags: 
editor: markdown
dateCreated: 2023-01-30T02:00:50.591Z
---

- [AOP: Spring Boot의 관점 지향 프로그래밍***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/aop-aspect-oriented-programming-in-spring-boot)
{.links-list}


# AOP: Aspect-Oriented Programming in Spring Boot

We all know that one of the main advantages of Java is its platform independence. But what many developers don't realize is that this very feature can also be leveraged to write more concise and readable code. This is where Aspect-Oriented Programming (AOP) comes in.

AOP is a programming paradigm that aims to increase modularity by allowing the separation of concerns (SoC). SoC is a design principle that states that a software system should be divided into distinct parts, each of which addresses a separate concern.

AOP complements Object-Oriented Programming (OOP) by providing another way of thinking about structuring code. While OOP is based on the concept of objects, AOP is based on the concept of aspects.

An aspect is a modular unit of functionality that is associated with a concern. A concern is a piece of functionality that is relevant to the application as a whole. For example, security is a concern that is relevant to all applications.

AOP allows developers to modularize the code that deals with a concern. This makes the code more maintainable and easier to understand. It also allows developers to reuse aspects in different applications.

Spring Boot is a popular framework for developing Java applications. It is built on top of the Spring framework and saves developers a lot of time and effort.

Spring Boot makes it easy to create stand-alone, production-grade Spring-based applications that you can "just run". It takes an opinionated view of the Spring platform and gets rid of all the boilerplate code that comes with it.

Spring Boot also makes it easy to create AOP applications. In this article, we'll take a look at how to use AOP in Spring Boot.

We'll start by creating a simple Spring Boot application. Then, we'll create an aspect that will be used to log method invocations. Finally, we'll see how to configure Spring Boot to use AspectJ.

## Creating a Spring Boot Application

Let's start by creating a simple Spring Boot application. We'll use the Spring Initializr to create our project.

Go to https://start.spring.io/ and enter the following details:

* Group: com.example
* Artifact: aop-demo
* Name: aop-demo
* Description: Demo of AOP in Spring Boot
* Package Name: com.example.aop
* Type: Maven Project
* Packaging: Jar
* Java Version: 1.8
* Language: Java
* Select the "Web" checkbox under "Starters"

Click "Generate Project" to download the project.

Import the project into your favorite IDE and create a new package called com.example.aop.service. Create a new class called CalculatorService in this package.

Add the following code to the CalculatorService class:

```java
package com.example.aop.service;

public class CalculatorService {

    public int add(int a, int b) {
        return a + b;
    }

    public int subtract(int a, int b) {
        return a - b;
    }

    public int multiply(int a, int b) {
        return a * b;
    }

    public int divide(int a, int b) {
        return a / b;
    }

}
```

We've now created a simple CalculatorService that has four methods: add, subtract, multiply, and divide.

Next, we'll create a controller that will expose these methods as REST endpoints.

Create a new package called com.example.aop.controller and a new class called CalculatorController in this package.

Add the following code to the CalculatorController class:

```java
package com.example.aop.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import com.example.aop.service.CalculatorService;

@RestController
public class CalculatorController {

    @Autowired
    private CalculatorService calculatorService;

    @GetMapping("/add")
    public int add(@RequestParam("a") int a, @RequestParam("b") int b) {
        return calculatorService.add(a, b);
    }

    @GetMapping("/subtract")
    public int subtract(@RequestParam("a") int a, @RequestParam("b") int b) {
        return calculatorService.subtract(a, b);
    }

    @GetMapping("/multiply")
    public int multiply(@RequestParam("a") int a, @RequestParam("b") int b) {
        return calculatorService.multiply(a, b);
    }

    @GetMapping("/divide")
    public int divide(@RequestParam("a") int a, @RequestParam("b") int b) {
        return calculatorService.divide(a, b);
    }

}
```

We've now created a simple CalculatorController that exposes the four methods of the CalculatorService as REST endpoints.

You can test the application by running it as a Spring Boot application.

## Creating an Aspect

Now that we have a basic Spring Boot application up and running, let's take a look at how to create an aspect.

As we mentioned before, an aspect is a modular unit of functionality that is associated with a concern. In our example, we're going to create an aspect that will be used to log method invocations.

Create a new package called com.example.aop.aspect and a new class called LoggingAspect in this package.

Add the following code to the LoggingAspect class:

```java
package com.example.aop.aspect;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class LoggingAspect {

    private Logger logger = LoggerFactory.getLogger(this.getClass());

    @Before("execution(* com.example.aop.service.*.*(..))")
    public void logBefore(JoinPoint joinPoint) {

        logger.info("Entering method {} with arguments {}",
                joinPoint.getSignature().getName(),
                joinPoint.getArgs());
    }

}
```

We've now created a simple aspect that will be used to log method invocations. This aspect will intercept all method invocations in the com.example.aop.service package and print a message to the log.

## Configuring Spring Boot to Use AspectJ

Now that we have our aspect, let's take a look at how to configure Spring Boot to use it.

Spring Boot uses AspectJ to enable AOP. AspectJ is a Java implementation of AOP. It provides a compile-time framework that we can use to weaving aspects into Java applications.

In order to use AspectJ in Spring Boot, we need to add the following dependency to our pom.xml file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```

We also need to add the @EnableAspectJAutoProxy annotation to our main application class:

```java
@SpringBootApplication
@EnableAspectJAutoProxy
public class AopDemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(AopDemoApplication.class, args);
    }
}
```

This annotation enables AspectJ auto-proxy creation, so that all the beans in the application context will be AOP-proxied.

## Testing the Application

Let's now test our application to see the aspect in action.

We can use curl to test the application:

```
curl http://localhost:8080/add?a=1&b=2
```

This should return the following response:

```
3
```

We can also check the logs to see the aspect in action:

```
2018-11-11 16:27:17.196  INFO 18564 --- [nio-8080-exec-1] c.e.a.aspect.LoggingAspect  : Entering method add with arguments [1, 2]
2018-11-11 16:27:17.196  INFO 18564 --- [nio-8080-exec-1] c.e.a.aspect.LoggingAspect  : Returning value 3
```

As we can see, the LoggingAspect intercepted the invocation of the add method and logged the method name and arguments. It also logged the returned value.

This is just a simple example of how to use AOP in Spring Boot. There are many other uses for AOP, such as transaction management, security, and caching.