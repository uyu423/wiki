---
title: 091: Integrating Spring Boot with Apache Zookeeper for Coordination and Synchronization
description: 
published: true
date: 2023-02-05T21:32:26.380Z
tags: 
editor: markdown
dateCreated: 2023-02-05T21:32:20.814Z
---

- [091: Integración de Spring Boot con Apache Zookeeper para coordinación y sincronización***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/091-integrating-spring-boot-with-apache-zookeeper-for-coordination-and-synchronization)
{.links-list}
- [091：将 Spring Boot 与 Apache Zookeeper 集成以进行协调和同步***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/091-integrating-spring-boot-with-apache-zookeeper-for-coordination-and-synchronization)
{.links-list}
- [091: 조정 및 동기화를 위해 Apache Zookeeper와 Spring Boot 통합***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/091-integrating-spring-boot-with-apache-zookeeper-for-coordination-and-synchronization)
{.links-list}


# 091: Integrating Spring Boot with Apache Zookeeper for Coordination and Synchronization

Apache Zookeeper is a distributed coordination service for distributed systems. It is used to manage large distributed systems. Spring Boot is a popular Java framework for developing microservices.

In this post, we will learn how to integrate Spring Boot with Apache Zookeeper. We will use Zookeeper to coordinate and synchronize our Spring Boot microservices.

## Installing Apache Zookeeper

Before we can start using Zookeeper, we need to install it. We can install Zookeeper using Homebrew on macOS:

```
$ brew install zookeeper
```

Or we can download the Zookeeper binary release from the [Apache Zookeeper website](https://zookeeper.apache.org/).

## Starting Apache Zookeeper

Once Zookeeper is installed, we can start it using the following command:

```
$ zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties
```

## Creating a Spring Boot Project

We can create a Spring Boot project using the [Spring Initializr](https://start.spring.io/). We will use the following dependencies:

* Web
* Actuator
* Lombok

## Configuring Spring Boot

We need to configure our Spring Boot application to use Zookeeper. We can do this by adding the following properties to our `application.properties` file:

```properties
spring.cloud.zookeeper.connect-string=localhost:2181
spring.cloud.zookeeper.discovery.instance-id=${spring.application.name}
spring.cloud.zookeeper.discovery.root=/${spring.application.name}
spring.cloud.zookeeper.discovery.service-name=${spring.application.name}
spring.cloud.zookeeper.discovery.enabled=true
```

## Creating a Spring Boot Service

We can create a Spring Boot service using the `@SpringBootApplication` annotation:

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## Adding a Rest Controller

We can add a Rest controller to our service using the `@RestController` annotation:

```java
@RestController
public class GreetingController {

    @GetMapping("/greeting")
    public String greeting() {
        return "Hello, world!";
    }

}
```

## Testing the Service

We can test our service by sending a `GET` request to the `/greeting` endpoint:

```
$ curl localhost:8080/greeting
Hello, world!
```

## Registering the Service with Zookeeper

Once our service is up and running, we need to register it with Zookeeper. We can do this using the `@DiscoveryClient` annotation:

```java
@SpringBootApplication
@DiscoveryClient
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## Accessing the Service from another Service

Once our service is registered with Zookeeper, we can access it from another service. We can do this by injecting a `DiscoveryClient` into our controller:

```java
@RestController
public class GreetingController {

    @Autowired
    private DiscoveryClient discoveryClient;

    @GetMapping("/greeting")
    public String greeting() {
        List<ServiceInstance> instances = discoveryClient.getInstances("greeting-service");
        if (instances.isEmpty()) {
            return "Hello, world!";
        }
        String url = instances.get(0).getUri().toString();
        return "Hello, world! (from " + url + ")";
    }

}
```

## Conclusion

In this post, we learned how to integrate Spring Boot with Apache Zookeeper. We used Zookeeper to coordinate and synchronize our Spring Boot microservices.