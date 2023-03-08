---
title: 002: Setting up a Spring Boot project
description: 
published: true
date: 2023-02-03T07:05:20.341Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:05:18.593Z
---

- [002: Configuración de un proyecto Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/002-setting-up-a-spring-boot-project)
{.links-list}
- [002：设置一个Spring Boot项目***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/002-setting-up-a-spring-boot-project)
{.links-list}
- [002: 스프링 부트 프로젝트 설정***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/002-setting-up-a-spring-boot-project)
{.links-list}


# Setting up a Spring Boot project

In this post, we'll go over how to set up a Spring Boot project.

Spring Boot is a popular framework for building web applications and services. It is built on top of the Spring framework and makes it easy to create stand-alone, production-grade Spring-based applications.

## Prerequisites

Before we get started, there are a few things you'll need to have in order to follow along:

- Java 8 or above
- A text editor or IDE
- Maven 3.3.9 or above

## Creating a project

There are a few different ways to create a Spring Boot project. In this post, we'll be using the [Spring Initializr](https://start.spring.io/) to generate a project.

Head over to the Spring Initializr website and fill in the form with the following information:

- Project: Maven Project
- Language: Java
- Spring Boot Version: 2.1.7

Click the "Generate Project" button and a zip file will be downloaded. Extract the contents of the zip file to a directory of your choice.

## Importing the project

In your text editor or IDE, import the project as a Maven project. If you're using Eclipse, you can do this by going to File -> Import -> Existing Maven Projects.

## Running the project

Now that the project is set up, we can run it.

There are a few different ways to run a Spring Boot application. The simplest way is to use the Maven plugin:

```
mvn spring-boot:run
```

You should see output similar to the following:

```
[INFO] Scanning for projects...
[INFO] 
[INFO] ------------------------------------------------------------------------
[INFO] Building myproject 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] >>> spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) > test-compile @ myproject >>>
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ myproject ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /Users/user/Documents/workspace-sts-3.9.10.RELEASE/myproject/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ myproject ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] >>> spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) > compile @ myproject >>>
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ myproject ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /Users/user/Documents/workspace-sts-3.9.10.RELEASE/myproject/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ myproject ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] >>> spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) > test-compile @ myproject >>>
[INFO] 
[INFO] <<< spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) < test-compile @ myproject <<<
[INFO] 
[INFO] 
[INFO] --- spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) @ myproject ---
[INFO] Attaching agents: []

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.1.7.RELEASE)

2019-06-07 23:58:45.583  INFO 86848 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2019-06-07 23:58:45.602  INFO 86848 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2019-06-07 23:58:45.602  INFO 86848 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.22]
2019-06-07 23:58:45.697  INFO 86848 --- [ost-startStop-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2019-06-07 23:58:45.697  INFO 86848 --- [ost-startStop-1] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 100 ms
2019-06-07 23:58:46.069  INFO 86848 --- [ost-startStop-1] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2019-06-07 23:58:46.145  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.ServletRegistrationBean  : Servlet dispatcherServlet mapped to [/]
2019-06-07 23:58:46.149  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'characterEncodingFilter' to: [/*]
2019-06-07 23:58:46.149  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'hiddenHttpMethodFilter' to: [/*]
2019-06-07 23:58:46.149  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'httpPutFormContentFilter' to: [/*]
2019-06-07 23:58:46.149  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'requestContextFilter' to: [/*]
2019-06-07 23:58:46.839  INFO 86848 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Shutting down ExecutorService 'applicationTaskExecutor'
2019-06-07 23:58:46.841  INFO 86848 --- [           main] o.apache.catalina.core.StandardService   : Stopping service [Tomcat]
2019-06-07 23:58:46.857  INFO 86848 --- [           main] ConditionEvaluationReportLoggingListener : 

Error starting ApplicationContext. To display the conditions report re-run your application with 'debug' enabled.
2019-06-07 23:58:46.862 ERROR 86848 --- [           main] o.s.boot.SpringApplication               : Application run failed

org.springframework.boot.context.event.ApplicationFailedEvent[source=org.springframework.boot.SpringApplication@4f4f4f4f]

```

If you see this output, it means the project is up and running!