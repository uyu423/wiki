---
title: 019：在 Spring Boot 中创建和使用自定义配置
description: 
published: true
date: 2023-02-03T11:32:32.407Z
tags: 
editor: markdown
dateCreated: 2023-02-03T11:32:30.807Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [019: Creating and using custom configurations in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/019-creating-and-using-custom-configurations-in-spring-boot)
{.links-list}


# 在 Spring Boot 中创建和使用自定义配置

在开发 Spring Boot 应用程序时，您可能需要创建和使用自定义配置。这可以通过在 `src/main/resources` 文件夹中创建一个名为 `application.yml` 的文件来完成。

在此文件中，您可以指定任何自定义配置值。例如，您可以指定您的应用程序将在其上运行的端口：

```yaml
server:
  port: 8080
```

您还可以在单个键下指定多个配置值。例如，您可以同时指定端口和上下文路径：

```yaml
server:
  port: 8080
  context-path: /myapp
```

如果需要使用多个配置文件，可以使用 spring.config.location 属性指定要加载的文件：

```yaml
spring:
  config:
    location: classpath:application.yml,classpath:custom.yml
```

在上面的示例中，将首先加载 application.yml 文件，然后是 custom.yml 文件。

也可以使用系统属性或环境变量指定 `spring.config.location` 属性。例如，您可以在启动应用程序时设置 `spring.config.location` 系统属性：

```
java -jar myapp.jar --spring.config.location=classpath:application.yml,classpath:custom.yml
```

或者，您可以设置“SPRING_CONFIG_LOCATION”环境变量：

```
SPRING_CONFIG_LOCATION=classpath:application.yml,classpath:custom.yml java -jar myapp.jar
```

## 指定配置值

在 Spring Boot 中指定配置值的方法有很多种。最常见的方法是使用 application.yml 文件，如上一节所示。

指定配置值的另一种方法是使用系统属性或环境变量。例如，您可以在启动应用程序时设置 `server.port` 系统属性：

```
java -jar myapp.jar --server.port=8080
```

或者，您可以设置“SERVER_PORT”环境变量：

```
SERVER_PORT=8080 java -jar myapp.jar
```

您还可以使用 Java 系统属性指定配置值。例如，您可以在 application.yml 文件中设置 server.port 系统属性：

```yaml
server:
  port: ${SERVER_PORT}
```

## 访问配置值

指定配置值后，您可以使用“@Value”注释在代码中访问它们：

```java
@Value("${server.port}")
private int port;
```

在上面的示例中，“port”变量将填充“server.port”配置属性的值。

如果您需要访问多个配置值，您可以创建一个带有“@ConfigurationProperties”注解的类：

```java
@ConfigurationProperties(prefix = "server")
public class ServerProperties {

    private int port;
    private String contextPath;

    // getters and setters
}
```

在上面的示例中，`port` 和 `contextPath` 变量将分别填充为 `server.port` 和 `server.context-path` 配置属性的值。

然后，您可以将 `ServerProperties` 类的一个实例注入到您的代码中：

```java
@Autowired
private ServerProperties serverProperties;
```

## 结论

在本文中，您学习了如何在 Spring Boot 中创建和使用自定义配置。您还学习了如何指定配置值以及如何在代码中访问它们。