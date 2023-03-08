---
title: 019: Creating and using custom configurations in Spring Boot
description: 
published: true
date: 2023-02-03T11:32:35.706Z
tags: 
editor: markdown
dateCreated: 2023-02-03T11:32:30.814Z
---

- [019: Creación y uso de configuraciones personalizadas en Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/019-creating-and-using-custom-configurations-in-spring-boot)
{.links-list}
- [019：在 Spring Boot 中创建和使用自定义配置***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/019-creating-and-using-custom-configurations-in-spring-boot)
{.links-list}
- [019: Spring Boot에서 사용자 정의 구성 생성 및 사용***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/019-creating-and-using-custom-configurations-in-spring-boot)
{.links-list}


# Creating and using custom configurations in Spring Boot

When developing a Spring Boot application, you may need to create and use custom configurations. This can be done by creating a file called `application.yml` in the `src/main/resources` folder.

In this file, you can specify any custom configuration values. For example, you could specify the port that your application will run on:

```yaml
server:
  port: 8080
```

You can also specify multiple configuration values under a single key. For example, you could specify both the port and context path:

```yaml
server:
  port: 8080
  context-path: /myapp
```

If you need to use more than one configuration file, you can specify the files to be loaded by using the `spring.config.location` property:

```yaml
spring:
  config:
    location: classpath:application.yml,classpath:custom.yml
```

In the example above, the `application.yml` file will be loaded first, followed by the `custom.yml` file.

It's also possible to specify the `spring.config.location` property using system properties or environment variables. For example, you could set the `spring.config.location` system property when starting your application:

```
java -jar myapp.jar --spring.config.location=classpath:application.yml,classpath:custom.yml
```

Alternatively, you could set the `SPRING_CONFIG_LOCATION` environment variable:

```
SPRING_CONFIG_LOCATION=classpath:application.yml,classpath:custom.yml java -jar myapp.jar
```

## Specifying configuration values

There are many ways to specify configuration values in Spring Boot. The most common way is to use the `application.yml` file, as shown in the previous section.

Another way to specify configuration values is to use system properties or environment variables. For example, you could set the `server.port` system property when starting your application:

```
java -jar myapp.jar --server.port=8080
```

Alternatively, you could set the `SERVER_PORT` environment variable:

```
SERVER_PORT=8080 java -jar myapp.jar
```

You can also specify configuration values using Java system properties. For example, you could set the `server.port` system property in your `application.yml` file:

```yaml
server:
  port: ${SERVER_PORT}
```

## Accessing configuration values

Once you've specified your configuration values, you can access them in your code using the `@Value` annotation:

```java
@Value("${server.port}")
private int port;
```

In the example above, the `port` variable will be populated with the value of the `server.port` configuration property.

If you need to access multiple configuration values, you can create a `@ConfigurationProperties`-annotated class:

```java
@ConfigurationProperties(prefix = "server")
public class ServerProperties {

    private int port;
    private String contextPath;

    // getters and setters
}
```

In the example above, the `port` and `contextPath` variables will be populated with the values of the `server.port` and `server.context-path` configuration properties, respectively.

You can then inject an instance of the `ServerProperties` class into your code:

```java
@Autowired
private ServerProperties serverProperties;
```

## Conclusion

In this article, you've learned how to create and use custom configurations in Spring Boot. You've also learned how to specify configuration values and how to access them in your code.