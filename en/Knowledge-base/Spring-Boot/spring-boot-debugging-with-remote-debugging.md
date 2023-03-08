---
title: Spring Boot Debugging with Remote Debugging
description: 
published: true
date: 2023-02-02T20:57:28.873Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:57:27.238Z
---

- [Depuración de Spring Boot con depuración remota***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-debugging-with-remote-debugging)
{.links-list}
- [使用远程调试进行 Spring Boot 调试***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-debugging-with-remote-debugging)
{.links-list}
- [원격 디버깅을 사용한 스프링 부트 디버깅***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-debugging-with-remote-debugging)
{.links-list}


# Introduction

Developers often need to debug their code in order to find and fix errors. Spring Boot applications can be debugged in a number of ways, including using a remote debugger. In this article, we will explore how to debug Spring Boot applications using a remote debugger.

# What is remote debugging?

Remote debugging is a process that allows a developer to debug a program that is running on a remote machine. In order to do this, the developer needs to have access to the remote machine and be able to connect to it using a debugger.

# How to debug a Spring Boot application using a remote debugger

There are a few steps that need to be followed in order to debug a Spring Boot application using a remote debugger. We will go through each of these steps in detail.

## 1. Make sure that the application is running in debug mode

The first step is to make sure that the Spring Boot application is running in debug mode. This can be done by adding the following line to the application.properties file:

```
spring.boot.devtools.remote.debug=true
```

## 2. Start the remote debugger

The next step is to start the remote debugger. This can be done by running the following command:

```
java -Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=8000,suspend=n -jar myapp.jar
```

Replace myapp.jar with the name of your Spring Boot application.

## 3. Connect to the remote debugger

The final step is to connect to the remote debugger. This can be done using a debugger such as Eclipse or IntelliJ. In Eclipse, go to the Debug perspective and select Remote Java Application. In the Connect tab, select the project that contains the Spring Boot application. In the Connect tab, select the project that contains the Spring Boot application. In the Connect tab, select the project that contains the Spring Boot application. In the Connect tab, select the project that contains the Spring Boot application. In the Connect tab, select the project that contains the Spring Boot application. 

In IntelliJ, go to Run > Edit Configurations. In the Remote tab, select the project that contains the Spring Boot application. In the Connect tab, select the project that contains the Spring Boot application.

# Conclusion

In this article, we have explored how to debug a Spring Boot application using a remote debugger. We have also gone through the steps that need to be followed in order to do this.