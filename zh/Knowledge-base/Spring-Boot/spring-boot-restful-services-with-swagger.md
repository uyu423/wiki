---
title: 带有 Swagger 的 Spring Boot RESTful 服务
description: 
published: true
date: 2023-02-03T18:17:24.954Z
tags: 
editor: markdown
dateCreated: 2023-02-03T18:17:23.322Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot RESTful Services with Swagger***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-restful-services-with-swagger)
{.links-list}


# 带有 Swagger 的 Spring Boot RESTful 服务

随着微服务的日益普及，服务之间能够相互通信变得非常重要。在微服务架构中，每个服务都是一个独立的单元，它公开了一个用于通信的 REST API。

Swagger 是一种可以帮助创建和记录此类 REST API 的工具。它对于基于 Spring Boot 的应用程序特别有用，因为它具有许多可以根据代码自动生成文档的功能。

在本文中，我们将了解如何将 Swagger 2 用于 Spring Boot 应用程序以记录其 REST API。

## 什么是招摇？

Swagger 是一种可以帮助创建和记录 REST API 的工具。它对于基于 Spring Boot 的应用程序特别有用，因为它具有许多可以根据代码自动生成文档的功能。

Swagger2 是一个开源项目，用于描述和记录 RESTful API。它由最初的 Swagger 工具（现在称为 Swagger 1.0）背后的团队创建。

Swagger2 使用所谓的“OpenAPI 规范”（以前称为“Swagger 规范”）来为 REST API 定义标准的、与语言无关的接口。然后，各种工具可以使用此接口来启用文档、客户端代码生成和服务器存根生成等功能。

## 如何在 Spring Boot 中使用 Swagger？

Springfox 是一个为基于 Spring 的应用程序提供自动化 JSON API 文档的工具。它用于为用 Spring 编写的 RESTful 服务创建文档。

Springfox 的工作方式是在运行时检查应用程序一次，以根据 spring 配置、类结构和各种注释推断 API 语义。然后它会生成 JSON 或 YAML 格式的文档，并提供一个 UI 来浏览文档。

要在您的 Spring Boot 应用程序中使用 Springfox，您需要将以下依赖项添加到您的 `pom.xml`：

```xml
<dependency>
  <groupId>io.springfox</groupId>
  <artifactId>springfox-boot-starter</artifactId>
  <version>2.9.2</version>
</dependency>
```

您还需要通过创建一个“@Configuration”类并使用“@EnableSwagger2”对其进行注释来配置 Springfox。例如：

```java
@Configuration
@EnableSwagger2
public class SwaggerConfig {
}
```

这将启用 Swagger，用户界面将在 http://localhost:8080/swagger-ui.html 可用。

## 招摇的用户界面

Swagger UI 是一个用户界面，可用于浏览和测试服务公开的 API。它是根据 OpenAPI 规范自动生成的，提供了一种无需编写任何代码即可与 API 交互的方法。

当您运行应用程序时，UI 位于“http://localhost:8080/swagger-ui.html”。

![招摇用户界面](https://i.imgur.com/5GgUjNu.png)

## 自定义 Swagger UI

可以通过将查询参数添加到“index.html”文件来自定义 Swagger UI。例如，要更改 API 的 URL，您可以添加 `url` 查询参数：

`http://localhost:8080/swagger-ui.html?url=http://localhost:8080/v2/api-docs`

要更改 API 密钥，您可以添加 `apiKey` 查询参数：

`http://localhost:8080/swagger-ui.html?apiKey=XXXXXXXXXXXXXXXXXXXXXXX`

## 自定义 OpenAPI 规范

可以通过提供类型为“Docket”的“@Configuration”bean 来自定义 OpenAPI 规范。例如，要更改 API 的路径，您可以执行以下操作：

```java
@Bean
public Docket api() {
    return new Docket(DocumentationType.SWAGGER_2)
        .select()
        .apis(RequestHandlerSelectors.any())
        .paths(PathSelectors.any())
        .build()
        .pathMapping("/");
}
```

这会将 API 的路径从“/v2/api-docs”更改为“/api-docs”。

要更改 API 的主机，您可以执行以下操作：

```java
@Bean
public Docket api() {
    return new Docket(DocumentationType.SWAGGER_2)
        .host("example.com")
        .select()
        .apis(RequestHandlerSelectors.any())
        .paths(PathSelectors.any())
        .build();
}
```

## 结论

在本文中，我们研究了如何将 Swagger 2 用于 Spring Boot 应用程序以记录其 REST API。我们还了解了如何自定义 Swagger UI 和 OpenAPI 规范。