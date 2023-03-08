---
title: 060: Working with Spring Boot's Actuator for Monitoring
description: 
published: true
date: 2023-02-04T23:32:28.792Z
tags: 
editor: markdown
dateCreated: 2023-02-04T23:32:23.533Z
---

- [060: Trabajar con el actuador Spring Boot para monitoreo***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/060-working-with-spring-boot-s-actuator-for-monitoring)
{.links-list}
- [060：使用 Spring Boot 的执行器进行监控***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/060-working-with-spring-boot-s-actuator-for-monitoring)
{.links-list}
- [060: 모니터링을 위한 Spring Boot의 액추에이터 작업***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/060-working-with-spring-boot-s-actuator-for-monitoring)
{.links-list}


# Spring Boot's Actuator for Monitoring 

Spring Boot's Actuator is a great tool for monitoring and managing your Spring Boot application. In this post, we'll take a look at how to use Actuator to monitor your application's health and performance.

## What is Actuator? 

Actuator is a Spring Boot module that provides production-ready features to help you monitor and manage your application. With Actuator, you can monitor your application's health, performance, and even create custom endpoint to get information about your application's state.

## How to use Actuator?

To use Actuator in your Spring Boot application, you need to add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Once you've added the dependency, you can start using Actuator's features.

## Monitoring your application's health

One of the most important features of Actuator is its ability to monitor your application's health. By default, Actuator exposes a `/health` endpoint that you can use to check your application's health.

The `/health` endpoint returns a `status` property that can have one of the following values:

- `UP`: The application is up and running.
- `DOWN`: The application is down.
- `OUT_OF_SERVICE`: The application is out of service.

The `/health` endpoint also returns a `details` property that contains more information about the application's health. For example, the `details` property might contain information about the application's database connection or the number of threads that are currently running.

In addition to the `/health` endpoint, Actuator also exposes a `/info` endpoint that you can use to get information about your application. The `/info` endpoint returns a `build` property that contains information about the application's build, such as the version number and the timestamp of the build.

## Monitoring your application's performance 

In addition to monitoring your application's health, Actuator can also help you monitor your application's performance. Actuator exposes a number of performance-related endpoint, such as `/metrics`, `/dump`, and `/trace`.

The `/metrics` endpoint returns a number of performance-related metrics, such as the number of requests that have been processed, the average response time, and the number of errors that have occurred.

The `/dump` endpoint returns a thread dump of the application, which can be useful for debugging purposes.

The `/trace` endpoint returns a trace of the application, which can be useful for understanding the application's flow.

## Creating custom endpoint 

In addition to the built-in endpoint, Actuator also allows you to create custom endpoint. To create a custom endpoint, you need to create a class that implements the `Endpoint` interface.

For example, the following class creates a custom `/myendpoint` endpoint that returns a `message` property:

```java
@Component
public class MyEndpoint implements Endpoint<Map<String, String>> {

    @Override
    public String getId() {
        return "/myendpoint";
    }

    @Override
    public Map<String, String> invoke() {
        Map<String, String> result = new HashMap<>();
        result.put("message", "Hello, world!");
        return result;
    }

    @Override
    public boolean isSensitive() {
        return false;
    }

}
```

##Conclusion 

In this post, we've looked at how to use Spring Boot's Actuator for monitoring your application. Actuator is a great tool for monitoring your application's health and performance. In addition, Actuator allows you to create custom endpoint to get information about your application.