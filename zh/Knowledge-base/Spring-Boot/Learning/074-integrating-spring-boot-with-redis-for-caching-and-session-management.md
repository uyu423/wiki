---
title: 074：将 Spring Boot 与 Redis 集成以进行缓存和会话管理
description: 
published: true
date: 2023-02-02T15:23:31.022Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:23:29.446Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [074: Integrating Spring Boot with Redis for Caching and Session Management***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/074-integrating-spring-boot-with-redis-for-caching-and-session-management)
{.links-list}


# 介绍

在本文中，我们将学习如何将 Spring Boot 与 Redis 集成以进行缓存和会话管理。

缓存是一种将经常访问的数据存储在内存中以便在需要时可以快速检索的技术。会话管理是存储和检索有关用户会话的数据的过程，例如用户的偏好或他们购物车中的项目。

缓存和会话管理都可用于提高 Web 应用程序的性能。 Redis 是缓存和会话管理的流行选择，因为它速度快、可扩展且易于使用。

# 安装 Redis

在开始使用 Redis 之前，我们需要安装它。 Redis 可用于所有主要操作系统，因此您可以将其安装在您的开发机器、服务器或云环境中。

如果您使用的是 Linux，则可以从发行版的包管理器安装 Redis。例如，在 Ubuntu 上，您可以使用 apt：

```
sudo apt install redis-server
```

如果您使用的是 macOS，则可以使用 Homebrew 安装 Redis：

```
brew install redis
```

如果您使用的是 Windows，则可以从 Microsoft Store 安装 Redis：

```
Get-AppxPackage -AllUsers -Name Microsoft.Portable.Redis | Foreach {Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml"}
```

安装 Redis 后，您可以通过运行以下命令来启动服务器：

```
redis-server
```

# 配置 Spring Boot

现在我们已经安装了 Redis，我们可以配置 Spring Boot 来使用它。首先，我们需要将 spring-boot-starter-data-redis starter 添加到我们的项目中。这个 starter 将引入我们在 Spring Boot 中使用 Redis 所需的依赖项。

如果您使用的是 Maven，则可以将启动器添加到 pom.xml 文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

如果您使用的是 Gradle，则可以将启动程序添加到您的 build.gradle 文件中：

```groovy
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-data-redis'
}
```

启动器添加到我们的项目后，我们需要配置 Spring Boot 以连接到我们的 Redis 服务器。我们可以通过将以下属性添加到我们的 application.properties 文件来做到这一点：

```
spring.redis.host=localhost
spring.redis.port=6379
```

# 使用 Redis 缓存

现在我们已经配置了 Redis，我们可以开始使用它进行缓存了。缓存是一种将经常访问的数据存储在内存中以便在需要时可以快速检索的技术。

例如，假设我们有一个显示产品列表的 Web 应用程序。每次加载页面时，应用程序都需要从数据库中获取产品列表。这可能很慢，尤其是当数据库很大或位于远程位置时。

我们可以通过在 Redis 中缓存产品列表来加快页面速度。首次加载页面时，应用程序将从数据库中获取产品列表并将其存储在 Redis 中。对该页面的后续请求将从 Redis 中检索产品列表，这比从数据库中获取它要快得多。

要在 Spring Boot 中使用 Redis 进行缓存，我们需要在我们的主应用程序类中添加 @EnableCaching 注解：

```java
@SpringBootApplication
@EnableCaching
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

我们还需要创建一个缓存管理器。缓存管理器负责管理我们应用程序中的缓存。 Spring Boot 提供了一个 RedisCacheManager 可以用来管理 Redis 缓存。

我们可以通过使用@Bean 和@Primary 注释一个bean 来创建一个RedisCacheManager：

```java
@Bean
@Primary
public CacheManager cacheManager(RedisConnectionFactory connectionFactory) {
    return RedisCacheManager.create(connectionFactory);
}
```

# 使用 Redis 进行会话管理

除了缓存，Redis 还可以用于会话管理。会话管理是存储和检索有关用户会话的数据的过程，例如用户的偏好或他们购物车中的项目。

当用户登录到 Web 应用程序时，将创建一个会话。此会话用于跟踪用户使用应用程序时的活动。例如，当用户将商品添加到他们的购物车时，会话用于将商品存储在购物车中。

当用户注销或会话过期时，会话数据被销毁。

会话管理很重要，因为它允许我们存储有关用户会话的数据，而不必将其存储在数据库中。这可以提高性能，因为从数据库中检索数据可能很慢。

要在 Spring Boot 中使用 Redis 进行会话管理，我们需要将以下属性添加到我们的 application.properties 文件中：

```
server.servlet.session.store-type=redis
```

此属性告诉 Spring Boot 使用 Redis 来存储会话数据。

# 结论

在本文中，我们学习了如何将 Spring Boot 与 Redis 集成以进行缓存和会话管理。我们还学习了如何安装 Redis 和配置 Spring Boot 以使用它。