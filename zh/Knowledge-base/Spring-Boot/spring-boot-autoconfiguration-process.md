---
title: Spring Boot 自动配置过程
description: 
published: true
date: 2023-02-07T07:32:34.106Z
tags: 
editor: markdown
dateCreated: 2023-02-07T07:32:32.524Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot Autoconfiguration Process***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-autoconfiguration-process)
{.links-list}


# Spring Boot 自动配置过程

Spring Boot 自动配置是一个基于在类路径上检测到的依赖项自动配置 Spring 应用程序的过程。可以通过以属性、环境变量和命令行参数的形式提供显式配置来微调此自动配置。

为了理解自动配置在 Spring Boot 中是如何工作的，有必要理解 Spring 配置文件的概念。配置文件是一组可以在 Spring 应用程序中激活的配置设置。默认情况下，Spring Boot 将根据“默认”配置文件配置应用程序。但是，可以通过使用“spring.profiles.active”属性、设置环境变量或使用命令行参数来激活其他配置文件。

当在 Spring Boot 应用程序中启用自动配置时，Spring Boot 应用程序将尝试根据它在类路径上检测到的依赖项自动配置自己。例如，如果在类路径上检测到 `spring-boot-starter-data-jpa` 依赖项，Spring Boot 将自动配置 DataSource 和 EntityManagerFactory。

在某些情况下，可能需要通过提供显式配置来微调自动配置过程。这可以通过使用属性、环境变量和命令行参数来完成。

例如，要配置 EntityManagerFactory 将使用的数据源，可以使用 `spring.datasource.url` 属性。

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/test
```

或者，可以使用 `DATASOURCE_URL` 环境变量。

```
DATASOURCE_URL=jdbc:mysql://localhost:3306/test
```

最后，可以使用 `--spring.datasource.url` 命令行参数。

```
--spring.datasource.url=jdbc:mysql://localhost:3306/test
```

当提供多个配置源时，它们将按以下顺序进行评估：

1. 在 `application.properties` 或 `application.yml` 中定义的属性。
2. 在“@Configuration”类中定义的属性。
3.环境变量。
4. 命令行参数。

可以使用 spring.boot.autoconfigure.EnableAutoConfiguration 注释禁用自动配置过程。

```java
@SpringBootApplication
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }

}
```

在上面的示例中，@EnableAutoConfiguration 注释用于启用自动配置。 `exclude` 属性用于排除 `DataSourceAutoConfiguration` 类，这将禁用 DataSource 的自动配置。

也可以通过使用 @Conditional 注释来禁用特定 bean 的自动配置。

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

在上面的示例中，@ConditionalOnProperty 注释用于有条件地配置 DataSourceConfig 类。 `name` 属性用于指定应检查的属性的名称。 `matchIfMissing` 属性用于指示如果属性缺失，条件是否应该匹配。在这种情况下，只有定义了 spring.datasource.url 属性时，条件才会匹配。

通过以属性、环境变量和命令行参数的形式提供显式配置，可以进一步微调自动配置过程。