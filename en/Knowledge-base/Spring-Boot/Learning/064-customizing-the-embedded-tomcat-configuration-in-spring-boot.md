---
title: 064: Customizing the Embedded Tomcat Configuration in Spring Boot
description: 
published: true
date: 2023-02-02T16:23:30.484Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:23:28.850Z
---

- [064: Personalización de la configuración de Tomcat integrada en Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/064-customizing-the-embedded-tomcat-configuration-in-spring-boot)
{.links-list}
- [064: 在 Spring Boot 中自定义嵌入式 Tomcat 配置***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/064-customizing-the-embedded-tomcat-configuration-in-spring-boot)
{.links-list}
- [064: Spring Boot에서 Embedded Tomcat 구성 사용자 지정***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/064-customizing-the-embedded-tomcat-configuration-in-spring-boot)
{.links-list}


# Customizing the Embedded Tomcat Configuration in Spring Boot

Spring Boot provides a number of features that can be used to customize the embedded Tomcat configuration. In this post, we'll take a look at a few of the most important configuration options.

## Configuring the HTTP Port

The first thing you might want to do is change the HTTP port that Tomcat is running on. By default, Tomcat will run on port 8080, but you can change this by setting the ```server.port``` property in your application.properties file:

```properties
server.port=8081
```

## Configuring the Tomcat Session timeout

Another common customization is to change the session timeout. By default, Tomcat will use a 30-minute session timeout, but you can change this by setting the ```server.session-timeout``` property:

```properties
server.session-timeout=1
```

## Configuring the Tomcat Access Log

Tomcat will also create an access log that contains information about all of the requests that are made to the server. By default, this log is located in the ```logs``` directory, but you can change the location by setting the ```server.tomcat.accesslog.directory``` property:

```properties
server.tomcat.accesslog.directory=/var/log/tomcat
```

## Configuring the Tomcat URI Encoding

By default, Tomcat will use the ISO-8859-1 character set for URI encoding. However, you can change this by setting the ```server.tomcat.uri-encoding``` property:

```properties
server.tomcat.uri-encoding=UTF-8
```

## Configuring the Tomcat Connector

Tomcat uses a connector to receive requests and send responses. By default, Tomcat will use the AJP connector, but you can change this by setting the ```server.tomcat.protocol-header``` property:

```properties
server.tomcat.protocol-header=org.apache.coyote.http11.Http11NioProtocol
```

## Configuring the Tomcat Context Path

The context path is the path that is used to access your application. By default, this is set to ```/```, but you can change it by setting the ```server.context-path``` property:

```properties
server.context-path=/myapp
```

## Configuring Tomcat SSL

Tomcat also supports SSL for secure communications. To configure SSL, you will need to set the ```server.ssl.key-store```, ```server.ssl.key-store-password```, ```server.ssl.key-alias```, and ```server.ssl.key-alias-password``` properties. For more information about configuring SSL in Tomcat, see the [Tomcat SSL Configuration How-To](https://tomcat.apache.org/tomcat-8.5-doc/ssl-howto.html).

## Conclusion

In this post, we've looked at a few of the most important ways to customize the embedded Tomcat configuration in Spring Boot. By changing a few simple properties, you can change the way Tomcat runs to better suit your needs.