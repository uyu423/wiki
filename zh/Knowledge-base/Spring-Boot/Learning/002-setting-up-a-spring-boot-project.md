---
title: 002：设置一个Spring Boot项目
description: 
published: true
date: 2023-02-03T07:05:23.450Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:05:18.588Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [002: Setting up a Spring Boot project***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/002-setting-up-a-spring-boot-project)
{.links-list}


# 设置 Spring Boot 项目

在这篇文章中，我们将介绍如何设置 Spring Boot 项目。

Spring Boot 是用于构建 Web 应用程序和服务的流行框架。它建立在 Spring 框架之上，可以轻松创建独立的、生产级的基于 Spring 的应用程序。

## 先决条件

在我们开始之前，您需要做一些事情才能跟进：

- Java 8 或以上
- 文本编辑器或 IDE
- Maven 3.3.9 或以上版本

## 创建项目

有几种不同的方法可以创建 Spring Boot 项目。在这篇文章中，我们将使用 [Spring Initializr](https://start.spring.io/) 来生成一个项目。

前往 Spring Initializr 网站并使用以下信息填写表格：

- 项目：Maven 项目
- 语言：Java
- 春季启动版本：2.1.7

单击“生成项目”按钮，将下载一个 zip 文件。将 zip 文件的内容解压缩到您选择的目录中。

## 导入项目

在文本编辑器或 IDE 中，将项目导入为 Maven 项目。如果您使用的是 Eclipse，则可以通过转到文件 -> 导入 -> 现有 Maven 项目来执行此操作。

## 运行项目

现在项目已经设置好了，我们可以运行它了。

有几种不同的方法可以运行 Spring Boot 应用程序。最简单的方法是使用 Maven 插件：

```
mvn spring-boot:run
```

您应该看到类似于以下内容的输出：

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

如果您看到此输出，则表示该项目已启动并正在运行！