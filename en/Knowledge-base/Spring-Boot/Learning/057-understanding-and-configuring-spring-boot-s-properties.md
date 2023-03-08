---
title: 057: Understanding and Configuring Spring Boot's Properties
description: 
published: true
date: 2023-02-04T20:32:22.439Z
tags: 
editor: markdown
dateCreated: 2023-02-04T20:32:17.137Z
---

- [057: comprensión y configuración de las propiedades de Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/057-understanding-and-configuring-spring-boot-s-properties)
{.links-list}
- [057：了解和配置 Spring Boot 的属性***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/057-understanding-and-configuring-spring-boot-s-properties)
{.links-list}
- [057: Spring Boot의 속성 이해 및 구성***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/057-understanding-and-configuring-spring-boot-s-properties)
{.links-list}


# Spring Boot Properties

In this post, we'll take a look at Spring Boot properties. We'll learn what they are, how to configure them, and how they can be used to customize the behavior of Spring Boot applications.

## What are Spring Boot Properties?

Spring Boot properties are used to configure Spring Boot applications. They can be used to set values for various Spring Boot settings, such as the application name, server port, and so on.

Properties can be configured in a number of ways, such as in a properties file, via environment variables, or programmatically.

## How to Configure Spring Boot Properties

Spring Boot properties can be configured in a number of ways.

The most common way is to use a properties file. Spring Boot will look for a file called `application.properties` in the classpath. This file can be used to override any of the default Spring Boot properties.

For example, the following `application.properties` file would set the server port to 8080:

```
server.port=8080
```

Another way to configure Spring Boot properties is via environment variables. Spring Boot will look for environment variables that start with `spring.` and use them to override any corresponding properties.

For example, the following environment variable would set the server port to 8080:

```
spring.server.port=8080
```

Finally, Spring Boot properties can also be configured programmatically. This can be done by creating a `@Configuration` class and using the `@ConfigurationProperties` annotation.

For example, the following `@Configuration` class would map the `server.port` property to a `serverPort` field:

```java
@Configuration
@ConfigurationProperties(prefix="server")
public class ServerConfig {

    private int port;

    public int getPort() {
        return port;
    }

    public void setPort(int port) {
        this.port = port;
    }

}
```

## Customizing Spring Boot Applications

Spring Boot properties can be used to customize the behavior of Spring Boot applications.

For example, the `spring.main.banner-mode` property can be used to disable the Spring Boot banner:

```
spring.main.banner-mode=off
```

The `spring.jpa.show-sql` property can be used to enable SQL logging for JPA:

```
spring.jpa.show-sql=true
```

The `spring.thymeleaf.cache` property can be used to enable Thymeleaf template caching:

```
spring.thymeleaf.cache=true
```

And so on.

## Conclusion

In this post, we've learned about Spring Boot properties. We've seen how to configure them, how they can be used to customize the behavior of Spring Boot applications, and where to find more information about them.