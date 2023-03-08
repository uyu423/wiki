---
title: 034: Using Spring Boot with Spring Cloud Config
description: 
published: true
date: 2023-02-04T02:32:33.243Z
tags: 
editor: markdown
dateCreated: 2023-02-04T02:32:31.608Z
---

- [034: Uso de Spring Boot con Spring Cloud Config***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/034-using-spring-boot-with-spring-cloud-config)
{.links-list}
- [034：将 Spring Boot 与 Spring Cloud Config 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/034-using-spring-boot-with-spring-cloud-config)
{.links-list}
- [034: Spring Cloud 구성과 함께 Spring Boot 사용***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/034-using-spring-boot-with-spring-cloud-config)
{.links-list}


# Using Spring Boot with Spring Cloud Config

Spring Cloud Config provides server and client-side support for externalized configuration in a distributed system. The Config Server can be easily used with Spring Boot applications through the @EnableConfigServer annotation.

In this post, we'll take a look at how to use the Config Server with a Spring Boot application. We'll also look at how to use the Config Client to connect to the Config Server and fetch the configuration.

## Setting up the Config Server

The first thing we need to do is set up the Config Server. We can do this using the @EnableConfigServer annotation on our Spring Boot application:

```java
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {

    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}
```

This will enable the Config Server on our application. By default, the Config Server will serve configuration from a file located in the application's classpath.

We can also configure the Config Server to fetch configuration from a Git repository. For example, we can add the following to our application.properties file:

```properties
spring.cloud.config.server.git.uri=https://github.com/spring-cloud/spring-cloud-config
spring.cloud.config.server.git.searchPaths=config-repo
```

This will tell the Config Server to fetch configuration from the spring-cloud-config GitHub repository, in the config-repo directory.

## Setting up the Config Client

Now that we have our Config Server set up, we can set up our Config Client. The Config Client is a Spring Boot application that fetches configuration from the Config Server.

We can set up the Config Client using the @EnableConfigClient annotation:

```java
@SpringBootApplication
@EnableConfigClient
public class ConfigClientApplication {

    public static void main(String[] args) {
        SpringApplication.run(ConfigClientApplication.class, args);
    }
}
```

This will enable the Config Client on our application. By default, the Config Client will connect to the Config Server at http://localhost:8888.

We can also configure the Config Client to connect to a different Config Server. For example, we can add the following to our application.properties file:

```properties
spring.cloud.config.uri=http://config-server:8888
```

This will tell the Config Client to connect to the Config Server at http://config-server:8888.

## Fetching Configuration

Once we have our Config Server and Config Client set up, we can fetch configuration from the Config Server. The Config Client will fetch the configuration and make it available to our application.

For example, we can add the following to our application.properties file:

```properties
spring.cloud.config.name=my-app
```

This will tell the Config Client to fetch the configuration for the my-app application. The configuration will be made available to our application through the Spring Environment.

We can also fetch configuration for specific profiles. For example, we can add the following to our application.properties file:

```properties
spring.cloud.config.name=my-app
spring.cloud.config.profile=dev
```

This will tell the Config Client to fetch the configuration for the my-app application with the dev profile. The configuration will be made available to our application through the Spring Environment.

## Conclusion

In this post, we've looked at how to use the Config Server with a Spring Boot application. We've also looked at how to use the Config Client to connect to the Config Server and fetch the configuration.