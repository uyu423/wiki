---
title: Servicios RESTful de Spring Boot con Swagger
description: 
published: true
date: 2023-02-03T18:17:24.927Z
tags: 
editor: markdown
dateCreated: 2023-02-03T18:17:23.323Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot RESTful Services with Swagger***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-restful-services-with-swagger)
{.links-list}


# Servicios RESTful de Spring Boot con Swagger

Con la creciente popularidad de los microservicios, es importante que los servicios puedan comunicarse entre sí. En una arquitectura de microservicios, cada servicio es una unidad autónoma que expone una API REST para la comunicación.

Swagger es una herramienta que puede ayudar a crear y documentar dichas API REST. Es especialmente útil para las aplicaciones basadas en Spring Boot porque viene con una serie de funciones que pueden generar automáticamente documentación basada en el código.

En este artículo, veremos cómo usar Swagger 2 para una aplicación Spring Boot para documentar su API REST.

## ¿Qué es Swagger?

Swagger es una herramienta que puede ayudar a crear y documentar API REST. Es especialmente útil para las aplicaciones basadas en Spring Boot porque viene con una serie de funciones que pueden generar automáticamente documentación basada en el código.

Swagger2 es un proyecto de código abierto que se utiliza para describir y documentar las API RESTful. Es creado por el equipo detrás de la herramienta Swagger original (ahora llamada Swagger 1.0).

Swagger2 utiliza la llamada "Especificación de OpenAPI" (anteriormente conocida como "Especificación de Swagger") para definir una interfaz estándar independiente del idioma para las API REST. Esta interfaz puede ser utilizada por varias herramientas para habilitar características tales como documentación, generación de código de cliente y generación de stubs de servidor.

## ¿Cómo usar Swagger con Spring Boot?

Springfox es una herramienta que proporciona documentación API JSON automatizada para aplicaciones basadas en Spring. Se usa para crear documentación para servicios RESTful escrita en Spring.

Springfox funciona examinando una aplicación, una vez, en tiempo de ejecución para inferir la semántica de la API en función de las configuraciones de Spring, la estructura de clases y varias anotaciones. Luego genera documentación en formato JSON o YAML y proporciona una interfaz de usuario para explorar la documentación.

Para usar Springfox en su aplicación Spring Boot, debe agregar la siguiente dependencia a su `pom.xml`:

```xml
<dependency>
  <groupId>io.springfox</groupId>
  <artifactId>springfox-boot-starter</artifactId>
  <version>2.9.2</version>
</dependency>
```

También necesita configurar Springfox creando una clase `@Configuration` y anotándola con `@EnableSwagger2`. Por ejemplo:

```java
@Configuration
@EnableSwagger2
public class SwaggerConfig {
}
```

Esto habilitará Swagger y la interfaz de usuario estará disponible en `http://localhost:8080/swagger-ui.html`.

## Interfaz de usuario de Swagger

Swagger UI es una interfaz de usuario que se puede usar para explorar y probar las API expuestas por un servicio. Se genera automáticamente a partir de la especificación OpenAPI y proporciona una forma de interactuar con la API sin escribir ningún código.

La interfaz de usuario está disponible en `http://localhost:8080/swagger-ui.html` cuando ejecuta la aplicación.

![IU de Swagger](https://i.imgur.com/5GgUjNu.png)

## Personalización de la interfaz de usuario de Swagger

La interfaz de usuario de Swagger se puede personalizar agregando parámetros de consulta al archivo `index.html`. Por ejemplo, para cambiar la URL de la API, puede agregar el parámetro de consulta `url`:

`http://localhost:8080/swagger-ui.html?url=http://localhost:8080/v2/api-docs`

Para cambiar la clave API, puede agregar el parámetro de consulta `apiKey`:

`http://localhost:8080/swagger-ui.html?apiKey=XXXXXXXXXXXXXXXXXXXXXXX`

## Personalización de la especificación OpenAPI

La especificación OpenAPI se puede personalizar proporcionando un bean `@Configuration` de tipo `Docket`. Por ejemplo, para cambiar la ruta de la API, puede hacer lo siguiente:

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

Esto cambiará la ruta de la API de `/v2/api-docs` a `/api-docs`.

Para cambiar el host de la API, puede hacer lo siguiente:

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

## Conclusión

En este artículo, analizamos cómo usar Swagger 2 para una aplicación Spring Boot para documentar su API REST. También vimos cómo personalizar la interfaz de usuario de Swagger y la especificación OpenAPI.