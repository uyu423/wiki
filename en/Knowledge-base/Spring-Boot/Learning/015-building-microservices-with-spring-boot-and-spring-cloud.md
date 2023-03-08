---
title: 015: Building microservices with Spring Boot and Spring Cloud
description: 
published: true
date: 2023-02-03T09:36:37.795Z
tags: 
editor: markdown
dateCreated: 2023-02-03T09:36:32.955Z
---

- [015: Creación de microservicios con Spring Boot y Spring Cloud***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/015-building-microservices-with-spring-boot-and-spring-cloud)
{.links-list}
- [015：使用 Spring Boot 和 Spring Cloud 构建微服务***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/015-building-microservices-with-spring-boot-and-spring-cloud)
{.links-list}
- [015: Spring Boot 및 Spring Cloud로 마이크로서비스 구축***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/015-building-microservices-with-spring-boot-and-spring-cloud)
{.links-list}


# Introduction

Microservices are a popular architectural style for building cloud-native applications. They are small, self-contained units that can be deployed independently and composed into complex applications.

Spring Boot is a popular framework for building microservices. It makes it easy to create stand-alone, production-grade Spring-based applications that can be "just run".

Spring Cloud is an ecosystem of open-source tools for building microservices. It provides libraries for common patterns used in distributed systems, such as service discovery, circuit breakers, and distributed tracing.

In this post, we'll learn how to build microservices with Spring Boot and Spring Cloud. We'll start with a simple example of a "hello world" microservice, then we'll add in service discovery and load balancing with Spring Cloud Netflix Eureka and Ribbon. Finally, we'll add distributed tracing with Spring Cloud Sleuth.

# Building a "Hello World" Microservice

Let's start by creating a simple "hello world" microservice. We'll use the Spring Initializr to generate a project with the following dependencies:

- Web
- Actuator

The Web dependency adds support for building web applications with Spring MVC. The Actuator dependency adds support for monitoring and managing our application.

Once the project is generated, we can open it in our IDE and add a simple controller:

```java
@RestController
public class HelloController {

    @RequestMapping("/")
    public String hello() {
        return "Hello, world!";
    }

}
```

This controller has a single endpoint that returns a "Hello, world!" message.

To run our application, we can use the Spring Boot Maven plugin:

```
./mvnw spring-boot:run
```

Once the application is up and running, we can access the "hello world" endpoint at http://localhost:8080/.

# Adding Service Discovery

In a microservices architecture, services are typically deployed on a cluster of nodes. When a service is deployed, it needs to be registered with a service discovery server so that other services can find it.

Spring Cloud Netflix Eureka is a popular service discovery server. To add Eureka to our project, we can add the following dependency:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

Once the dependency is added, we can enable the Eureka server by adding the @EnableEurekaServer annotation to our main application class:

```java
@SpringBootApplication
@EnableEurekaServer
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

We can now start our application and access the Eureka dashboard at http://localhost:8761/.

# Adding Load Balancing

In a microservices architecture, it is common for a service to be deployed on multiple nodes. When a service is invoked, a load balancer is used to route the request to one of the nodes.

Spring Cloud Netflix Ribbon is a popular load balancer. To add Ribbon to our project, we can add the following dependency:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-ribbon</artifactId>
</dependency>
```

Once the dependency is added, we can configure Ribbon by adding the @RibbonClient annotation to our main application class:

```java
@SpringBootApplication
@EnableEurekaServer
@RibbonClient(name = "hello-service")
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

This annotation configures a Ribbon client for the "hello-service" service.

# Adding Distributed Tracing

In a microservices architecture, it can be difficult to troubleshoot issues because requests can be routed through multiple services. Distributed tracing can help by tracking requests as they flow through the system.

Spring Cloud Sleuth is a popular distributed tracing framework. To add Sleuth to our project, we can add the following dependency:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-sleuth</artifactId>
</dependency>
```

Once the dependency is added, Sleuth will automatically be configured to trace requests.

# Conclusion

In this post, we've learned how to build microservices with Spring Boot and Spring Cloud. We've started with a simple "hello world" microservice and added in service discovery, load balancing, and distributed tracing.