---
title: Spring Boot Autoconfiguration Process
description: 
published: true
date: 2023-02-07T07:32:38.393Z
tags: 
editor: markdown
dateCreated: 2023-02-07T07:32:32.572Z
---

- [Proceso de configuración automática de Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-autoconfiguration-process)
{.links-list}
- [Spring Boot 自动配置过程***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-autoconfiguration-process)
{.links-list}
- [스프링 부트 자동 구성 프로세스***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-autoconfiguration-process)
{.links-list}


# Spring Boot Autoconfiguration Process

Spring Boot auto-configuration is a process that automatically configures a Spring application based on the dependencies it detects on the classpath. This auto-configuration can be fine-tuned by providing explicit configuration in the form of properties, environment variables, and command-line arguments.

In order to understand how auto-configuration works in Spring Boot, it is necessary to understand the concept of a Spring profile. A profile is a set of configuration settings that can be activated in a Spring application. By default, Spring Boot will configure an application based on the `default` profile. However, other profiles can be activated by using the `spring.profiles.active` property, setting environment variables, or by using command-line arguments.

When auto-configuration is enabled in a Spring Boot application, the Spring Boot application will attempt to automatically configure itself based on the dependencies it detects on the classpath. For example, if the `spring-boot-starter-data-jpa` dependency is detected on the classpath, Spring Boot will automatically configure a DataSource and EntityManagerFactory.

In some cases, it may be necessary to fine-tune the auto-configuration process by providing explicit configuration. This can be done by using properties, environment variables, and command-line arguments.

For example, to configure the datasource that will be used by the EntityManagerFactory, the `spring.datasource.url` property can be used.

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/test
```

Alternatively, the `DATASOURCE_URL` environment variable can be used.

```
DATASOURCE_URL=jdbc:mysql://localhost:3306/test
```

Finally, the `--spring.datasource.url` command-line argument can be used.

```
--spring.datasource.url=jdbc:mysql://localhost:3306/test
```

When multiple sources of configuration are provided, they are evaluated in the following order:

1. Properties defined in `application.properties` or `application.yml`.
2. Properties defined in an `@Configuration` class.
3. Environment variables.
4. Command-line arguments.

The auto-configuration process can be disabled by using the `spring.boot.autoconfigure.EnableAutoConfiguration` annotation.

```java
@SpringBootApplication
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }

}
```

In the above example, the `@EnableAutoConfiguration` annotation is used to enable auto-configuration. The `exclude` attribute is used to exclude the `DataSourceAutoConfiguration` class, which will disable auto-configuration of the DataSource.

It is also possible to disable auto-configuration for specific beans by using the `@Conditional` annotation.

```java
@Configuration
@ConditionalOnProperty(name="spring.datasource.url", matchIfMissing=false)
public class DataSourceConfig {

    @Bean
    public DataSource dataSource() {
        // configure and return DataSource
    }

}
```

In the above example, the `@ConditionalOnProperty` annotation is used to conditionally configure the `DataSourceConfig` class. The `name` attribute is used to specify the name of the property that should be checked. The `matchIfMissing` attribute is used to indicate whether the condition should match if the property is missing. In this case, the condition will only match if the `spring.datasource.url` property is defined.

The auto-configuration process can be further fine-tuned by providing explicit configuration in the form of properties, environment variables, and command-line arguments.