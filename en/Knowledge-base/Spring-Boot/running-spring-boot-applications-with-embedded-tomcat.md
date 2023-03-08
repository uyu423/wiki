---
title: Running Spring Boot Applications with Embedded Tomcat
description: 
published: true
date: 2023-02-17T18:02:38.240Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:54:39.273Z
---

- [임베디드 Tomcat으로 Spring Boot 애플리케이션 실행***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/running-spring-boot-applications-with-embedded-tomcat)
{.links-list}


For a long time, the Apache Tomcat team has maintained a [page](https://tomcat.apache.org/tomcat-7.0-doc/embedded-howto.html) with instructions on how to embed Tomcat in a wider range of applications. The page covers a few popular application servers, but not Spring Boot. Recently, the Tomcat team [moved](https://tomcat.apache.org/tomcat-9.0-doc/setup.html) the embedded documentation to the main Tomcat documentation site and [added](https://tomcat.apache.org/tomcat-9.0-doc/faq/index.html) a section on frequently asked questions about Tomcat.

There are a few ways to embed Tomcat in a Spring Boot application. The easiest way is to add the `spring-boot-starter-tomcat` dependency to your project, and Spring Boot will automatically configure Tomcat for you. Spring Boot also supports a few [other Embedded Containers](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-web-applications.html#boot-features-embedded-container-support).

If you want more control over the configuration of Tomcat, you can add the `tomcat-embed-core` dependency to your project, and Spring Boot will auto-configure a `TomcatEmbeddedServletContainerFactory` for you. You can then customize the factory by setting properties on it. For example, you can [set the port](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/context/embedded/tomcat/TomcatEmbeddedServletContainerFactory.html#setPort-int-) that Tomcat listens on.

If you need even more control, you can [instantiate](https://tomcat.apache.org/tomcat-9.0-doc/setup.html#Instantiating_Tomcat) a `Tomcat` instance yourself and [add](https://tomcat.apache.org/tomcat-9.0-doc/setup.html#Adding_Connectors_and_Services_ Programmatically) connectors and services to it. Spring Boot can then [wrap](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/context/embedded/tomcat/TomcatEmbeddedServletContainerFactory.html#getTomcatEmbeddedServletContainer-org.apache.catalina.startup.Tomcat-) the Tomcat instance in a `TomcatEmbeddedServletContainer`.

Here is a sample project that shows how to embed Tomcat in a Spring Boot application:

https://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-tomcat-multi-connectors

The sample project has two connectors configured: an HTTP connector on port 8080, and an AJP connector on port 8009. The AJP connector is commented out by default. To use it, uncomment the `<!--` and `-->` tags around the `<Connector>` element in `src/main/resources/application.properties`.

You can then build and run the sample application with the following command:

```
$ ./mvnw spring-boot:run
```

The application will start up on port 8080. You can access the application at http://localhost:8080/. You can also access the application through the AJP connector at http://localhost:8009/.

## References

- [Apache Tomcat Documentation -Embedded HOW-TO](https://tomcat.apache.org/tomcat-7.0-doc/embedded-howto.html)
- [Apache Tomcat Documentation - Setup](https://tomcat.apache.org/tomcat-9.0-doc/setup.html)
- [Apache Tomcat Documentation - FAQ](https://tomcat.apache.org/tomcat-9.0-doc/faq/index.html)
- [Spring Boot Documentation - Developing Web Applications](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-web-applications.html#boot-features-embedded-container-support)
- [Spring Boot API Documentation - TomcatEmbeddedServletContainerFactory](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/context/embedded/tomcat/TomcatEmbeddedServletContainerFactory.html)
- [Spring Boot API Documentation - TomcatEmbeddedServletContainer](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/context/embedded/tomcat/TomcatEmbeddedServletContainer.html)
- [Sample Spring Boot Application with Embedded Tomcat](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-tomcat-multi-connectors)