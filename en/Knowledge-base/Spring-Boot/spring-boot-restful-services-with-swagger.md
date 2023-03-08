---
title: Spring Boot RESTful Services with Swagger
description: 
published: true
date: 2023-02-03T18:17:28.234Z
tags: 
editor: markdown
dateCreated: 2023-02-03T18:17:23.327Z
---

- [Servicios RESTful de Spring Boot con Swagger***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-restful-services-with-swagger)
{.links-list}
- [带有 Swagger 的 Spring Boot RESTful 服务***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-restful-services-with-swagger)
{.links-list}
- [Swagger를 사용한 Spring Boot RESTful 서비스***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-restful-services-with-swagger)
{.links-list}


# Spring Boot RESTful Services with Swagger

With the ever-growing popularity of microservices, it's important for services to be able to communicate with each other. In a microservices architecture, each service is a self-contained unit which exposes a REST API for communication.

Swagger is a tool that can help in both creating and documenting such REST APIs. It's especially useful for Spring Boot based applications because it comes with a number of features that can automatically generate documentation based on the code.

In this article, we'll take a look at how to use Swagger 2 for a Spring Boot application to document its REST API.

## What is Swagger?

Swagger is a tool that can help in both creating and documenting REST APIs. It's especially useful for Spring Boot based applications because it comes with a number of features that can automatically generate documentation based on the code.

Swagger2 is an open source project used to describe and document RESTful APIs. It's created by the team behind the original Swagger tool (now called Swagger 1.0).

Swagger2 uses so-called "OpenAPI Specification" (formerly known as "Swagger Specification") to define a standard, language-agnostic interface to REST APIs. This interface can then be used by various tools to enable features such as documentation, client code generation and server stub generation.

## How to use Swagger with Spring Boot?

Springfox is a tool that provides automated JSON API documentation for Spring-based applications. It's used to create documentation for RESTful services written in Spring.

Springfox works by examining an application, once, at runtime to infer API semantics based on spring configurations, class structure and various annotations. It then generates documentation in JSON or YAML format and provides a UI to browse the documentation.

To use Springfox in your Spring Boot application, you need to add the following dependency to your `pom.xml`:

```xml
<dependency>
  <groupId>io.springfox</groupId>
  <artifactId>springfox-boot-starter</artifactId>
  <version>2.9.2</version>
</dependency>
```

You also need to configure Springfox by creating a `@Configuration` class and annotating it with `@EnableSwagger2`. For example:

```java
@Configuration
@EnableSwagger2
public class SwaggerConfig {
}
```

This will enable Swagger and the UI will be available at `http://localhost:8080/swagger-ui.html`.

## Swagger UI

Swagger UI is a user interface that can be used to browse and test the APIs exposed by a service. It's automatically generated from the OpenAPI Specification and provides a way to interact with the API without writing any code.

The UI is available at `http://localhost:8080/swagger-ui.html` when you run the application.

![Swagger UI](https://i.imgur.com/5GgUjNu.png)

## Customizing the Swagger UI

The Swagger UI can be customized by adding query parameters to the `index.html` file. For example, to change the URL of the API, you can add the `url` query parameter:

`http://localhost:8080/swagger-ui.html?url=http://localhost:8080/v2/api-docs`

To change the API key, you can add the `apiKey` query parameter:

`http://localhost:8080/swagger-ui.html?apiKey=XXXXXXXXXXXXXXXXXXXXXXX`

## Customizing the OpenAPI Specification

The OpenAPI Specification can be customized by providing a `@Configuration` bean of type `Docket`. For example, to change the path of the API, you can do the following:

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

This will change the path of the API from `/v2/api-docs` to `/api-docs`.

To change the host of the API, you can do the following:

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

## Conclusion

In this article, we've looked at how to use Swagger 2 for a Spring Boot application to document its REST API. We've also seen how to customize the Swagger UI and the OpenAPI Specification.