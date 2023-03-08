---
title: The Power of Actuator in Spring Boot
description: 
published: true
date: 2023-02-17T18:02:11.624Z
tags: 
editor: markdown
dateCreated: 2023-01-30T08:58:13.472Z
---

- [Spring Boot에서 Actuator의 힘***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/the-power-of-actuator-in-spring-boot)
{.links-list}


# The Power of Actuator in Spring Boot

In the context of software development, an actuator is a device that converts energy into motion. Spring Boot Actuator is a sub-project of Spring Boot that provides production-ready features to help monitor and manage application. With Spring Boot Actuator, we can easily monitor and manage our Spring Boot application in production environment.

 Actuator endpoints let us monitor and manage our application. By default, all endpoints are secured and we need to configure security to expose them. In this article, we will look at the most important Spring Boot Actuator endpoints.


## HTTP Endpoints

HTTP endpoints are the most basic type of endpoint. They expose information about the application itself, such as the version and build information. HTTP endpoints do not require any authentication or authorization.

The following is a list of HTTP endpoints that are available by default in Spring Boot Actuator:

- `/info`: Displays arbitrary application info.Actuator builds an `info` map that can be used by arbitrary endpoint to expose arbitrary information.
- `/health`: Shows application health information. The information is useful for monitoring purposes. It can be retrieved in JSON, XML or HTML format.
- `/env`: Exposes properties from Spring’s ConfigurableEnvironment.
- `/metrics`: Shows various meters, counters, and gauges that let us monitor our application.
- `/trace`: Displays trace information (by default, the last 100 HTTP requests).


## JMX Endpoints

JMX endpoints expose application management information through JMX MBeans. We can use JMX endpoints to monitor and manage our application in production environment.

The following is a list of JMX endpoints that are available by default in Spring Boot Actuator:

- `/jolokia`: Exposes JMX beans over HTTP/JSON protocol using Jolokia library.
- `/logfile`: Exposes endpoints to manage log file.
- `/loggers`: Exposes endpoints to manage loggers.



## Management Endpoints

Management endpoints are used to manage and monitor our application in production environment. We can use management endpoints to stop and restart our application, change log levels, etc.

The following is a list of management endpoints that are available by default in Spring Boot Actuator:

- `/beans`: Displays a complete list of all the Spring beans in our application.
- `/autoconfig`: Displays an auto-configuration report that shows how Spring Boot auto-configured our application.
- `/configprops`: Displays a list of all @ConfigurationProperties beans.
- `/dump`:Performs a thread dump.
- `/mappings`:Displays a collated list of all @RequestMapping paths.
- `/shutdown`: Allows the application to be gracefully shut down (not enabled by default).
- `/restart`: Allows the application to be restarted (not enabled by default).



 Spring Boot Actuator provides many other features that we have not covered in this article. For a complete list of features, please refer to the Spring Boot Actuator documentation.