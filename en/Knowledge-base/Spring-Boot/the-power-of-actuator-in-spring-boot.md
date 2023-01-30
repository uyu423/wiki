---
title: The Power of Actuator in Spring Boot
description: 
published: true
date: 2023-01-30T08:22:14.888Z
tags: 
editor: markdown
dateCreated: 2023-01-30T08:22:14.888Z
---

- [Spring Boot에서 Actuator의 힘***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/the-power-of-actuator-in-spring-boot)
{.links-list}




# The Power of Actuator in Spring Boot

If you've ever built a Spring Boot application, then you've likely used the Actuator. The Actuator is a tool that can help you monitor and manage your Spring Boot application. In this post, we'll take a look at what the Actuator is and how it can be used to power your Spring Boot application.

What is the Actuator?

The Actuator is a tool that can be used to monitor and manage your Spring Boot application. The Actuator provides a number of endpoints that can be used to monitor and manage your application. For example, the Actuator can be used to monitor your application's health, to view metrics about your application, to view trace information, and to view configurable parameters.

How to Use the Actuator

The Actuator can be used in a number of ways. The simplest way to use the Actuator is to add it to your project as a dependency. The Actuator is available as a Maven dependency, so you can add it to your project by adding the following dependency to your pom.xml file:

<dependency>
<groupId>org.springframework.boot</groupId>
<artifactId>spring-boot-starter-actuator</artifactId>
</dependency>

Once you've added the Actuator dependency to your project, you can access the Actuator's endpoints by navigating to http://localhost:8080/actuator. The Actuator's endpoints are exposed at the /actuator context path.

The Health Endpoint

The Health endpoint is the most commonly used Actuator endpoint. The Health endpoint can be used to view information about the health of your application. The information returned by the Health endpoint is configured by the Spring Boot HealthIndicators that are registered with the application. By default, the Health endpoint will return information about the application's database connection, the application's disk space, and the application's log file.

The Metrics Endpoint

The Metrics endpoint can be used to view metrics about your application. The metrics that are available depend on the metrics that are configured for your application. By default, the Metrics endpoint will return information about the application's memory usage, the application's thread usage, and the application's garbage collector.

The Trace Endpoint

The Trace endpoint can be used to view trace information about your application. The trace information includes the time taken to process each request, the path of each request, and the status of each request.

The Config Endpoint

The Config endpoint can be used to view configurable parameters about your application. The configurable parameters that are available depend on the configuration of your application. By default, the Config endpoint will return information about the application's logging level and the application's database connection.

Conclusion

In this post, we've taken a look at the Actuator and how it can be used to power your Spring Boot application. The Actuator provides a number of endpoints that can be used to monitor and manage your application. The Health, Metrics, Trace, and Config endpoints are the most commonly used Actuator endpoints.