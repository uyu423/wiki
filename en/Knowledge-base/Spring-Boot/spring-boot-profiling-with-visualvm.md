---
title: Spring Boot Profiling with VisualVM
description: 
published: true
date: 2023-01-31T20:57:37.246Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:57:35.629Z
---

- [VisualVM을 사용한 스프링 부트 프로파일링***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-profiling-with-visualvm)
{.links-list}
- [VisualVM を使用した Spring Boot プロファイリング***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/spring-boot-profiling-with-visualvm)
{.links-list}
- [使用 VisualVM 进行 Spring Boot 分析***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-profiling-with-visualvm)
{.links-list}



# Spring Boot Profiling with VisualVM

Spring Boot is a great framework for building microservices and other production-grade applications. One of the benefits of using Spring Boot is that it comes with an embedded Tomcat server, which makes it easy to deploy your application as a standalone jar.

However, one of the drawbacks of using an embedded server is that it can be difficult to troubleshoot performance issues. In this article, we'll take a look at how to use VisualVM to profile a Spring Boot application.

## What is VisualVM?

VisualVM is a tool that provides a graphical interface for viewing detailed information about Java applications. It can be used to monitor and troubleshoot applications running on the JVM.

## Installing VisualVM

VisualVM is included in the Oracle JDK, so if you have the JDK installed, you already have VisualVM. If you don't have the JDK installed, you can download VisualVM from the [Oracle website](https://www.oracle.com/java/technologies/visualvm.html).

## Profiling a Spring Boot Application

Now that we have VisualVM installed, let's take a look at how to use it to profile a Spring Boot application.

First, we need to start our Spring Boot application. We'll use the [Spring PetClinic](https://github.com/spring-projects/spring-petclinic) sample application for this example.

Once the application is up and running, we can open VisualVM and connect to the running application. To do this, click on the "File" menu and select "Add JMX Connection".

![VisualVM Add JMX Connection](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-add-jmx-connection.png)

In the "Add JMX Connection" dialog, enter the host and port of the running application. The default host is "localhost" and the default port is "1099".

![VisualVM Add JMX Connection Dialog](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-add-jmx-connection-dialog.png)

Click "OK" to connect to the running application.

Once VisualVM is connected to the running application, you should see the application in the "Applications" tab.

![VisualVM Applications Tab](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-applications-tab.png)

To start profiling the application, select the application in the "Applications" tab and click the "Profile" button.

![VisualVM Profile Button](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-profile-button.png)

In the "Profile Application" dialog, select the "CPU" profiling type and click "Start".

![VisualVM Profile Application Dialog](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-profile-application-dialog.png)

Once the profiling session has started, you can use VisualVM to view the thread activity, memory usage, and other information about the running application.

![VisualVM Monitor Tab](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-monitor-tab.png)

When you're finished profiling the application, you can stop the profiling session by selecting the "File" menu and selecting "Exit".

## Conclusion

In this article, we've seen how to use VisualVM to profile a Spring Boot application. VisualVM is a powerful tool that can be used to troubleshoot performance issues in Spring Boot applications.