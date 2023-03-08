---
title: 011: Monitoring and managing a Spring Boot application with Actuator
description: 
published: true
date: 2023-02-03T09:04:38.769Z
tags: 
editor: markdown
dateCreated: 2023-02-03T09:04:36.921Z
---

- [011: Supervisión y gestión de una aplicación Spring Boot con Actuator***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/011-monitoring-and-managing-a-spring-boot-application-with-actuator)
{.links-list}
- [011：使用 Actuator 监控和管理 Spring Boot 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/011-monitoring-and-managing-a-spring-boot-application-with-actuator)
{.links-list}
- [011: Actuator로 Spring Boot 애플리케이션 모니터링 및 관리***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/011-monitoring-and-managing-a-spring-boot-application-with-actuator)
{.links-list}


#Monitoring and managing a Spring Boot application with Actuator

Actuator is a tool that can be used to monitor and manage a Spring Boot application. It provides a number of features that can be used to monitor and manage the application, including:

- Health check
- Metrics
- Logging
- Configuration
- Endpoints

In this post, we will focus on using Actuator to monitor and manage a Spring Boot application. We will first look at how to configure Actuator in a Spring Boot application. We will then look at how to use Actuator's health check feature to monitor the health of our application. Finally, we will look at how to use Actuator's metrics feature to monitor the performance of our application.

##Configuring Actuator in a Spring Boot application

Actuator is not enabled by default in a Spring Boot application. To enable Actuator, we need to add the following dependency to our project:

```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Once we have added the dependency, we can enable Actuator by adding the following properties to our application.properties file:

```
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
```

The first property, management.endpoints.web.exposure.include, exposes all of the Actuator endpoints. The second property, management.endpoint.health.show-details, ensures that the health check endpoint includes detailed information about the health of our application.

##Using Actuator's health check feature

Actuator's health check feature can be used to monitor the health of our application. By default, Actuator provides a number of built-in health checks, including checks for the database, disk space, and JMS.

In addition to the built-in health checks, we can also add our own custom health checks. To add a custom health check, we need to create a class that implements the HealthIndicator interface. For example, the following class implements a health check for a service that we have called MyService:

```java
public class MyServiceHealthIndicator implements HealthIndicator {

   @Override
   public Health health() {
      // check the health of our service
      // if the service is healthy, return a Health.Builder with a status of UP
      // if the service is not healthy, return a Health.Builder with a status of DOWN
   }
}
```

Once we have created our custom health check, we need to register it with Spring. We can do this by adding the @Component annotation to our class. For example:

```java
@Component
public class MyServiceHealthIndicator implements HealthIndicator {

   @Override
   public Health health() {
      // check the health of our service
      // if the service is healthy, return a Health.Builder with a status of UP
      // if the service is not healthy, return a Health.Builder with a status of DOWN
   }
}
```

##Using Actuator's metrics feature

Actuator's metrics feature can be used to monitor the performance of our application. By default, Actuator provides a number of built-in metrics, including metrics for the database, JMS, and web requests.

In addition to the built-in metrics, we can also add our own custom metrics. To add a custom metric, we need to create a class that implements the MetricWriter interface. For example, the following class implements a metric for a service that we have called MyService:

```java
public class MyServiceMetricWriter implements MetricWriter {

   @Override
   public void write(Metric<?> metric) {
      // write the metric to our monitoring system
   }
}
```

Once we have created our custom metric, we need to register it with Spring. We can do this by adding the @Component annotation to our class. For example:

```java
@Component
public class MyServiceMetricWriter implements MetricWriter {

   @Override
   public void write(Metric<?> metric) {
      // write the metric to our monitoring system
   }
}
```

##Conclusion

In this post, we have looked at how to use Actuator to monitor and manage a Spring Boot application. We have seen how to configure Actuator in a Spring Boot application and how to use Actuator's health check and metrics features to monitor the health and performance of our application.