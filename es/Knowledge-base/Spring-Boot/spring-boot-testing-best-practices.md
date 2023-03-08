---
title: Prácticas recomendadas para las pruebas de Spring Boot
description: 
published: true
date: 2023-02-07T08:32:42.805Z
tags: 
editor: markdown
dateCreated: 2023-02-07T08:32:40.829Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Testing Best Practices***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-testing-best-practices)
{.links-list}


# Mejores prácticas de prueba de arranque de primavera

Desarrollar y probar aplicaciones Spring Boot puede ser un desafío. En este artículo, repasaremos algunas de las mejores prácticas para probar aplicaciones Spring Boot.

## Examen de la unidad

Las pruebas unitarias son las pruebas más importantes en cualquier aplicación. Deben ser rápidos, confiables y fáciles de escribir y mantener.

 Spring Boot proporciona una serie de funciones que pueden facilitar las pruebas unitarias, como:

* La anotación `@DataJpaTest` se puede usar para probar los repositorios JPA. Esta anotación configurará una base de datos en memoria, inicializará Spring Data y JPA, y deshabilitará la configuración automática completa.

* La anotación `@WebMvcTest` se puede usar para probar los controladores Spring MVC. Esta anotación configurará un servidor web en memoria, inicializará Spring MVC y deshabilitará la configuración automática completa.

* La anotación `@MockBean` se puede usar para inyectar frijoles simulados en el contexto de la aplicación Spring. Esto es útil para simular dependencias que aún no están disponibles o aún no se han implementado por completo.

* La anotación `@TestPropertySource` se puede usar para configurar propiedades para usar en pruebas. Esto es útil para establecer propiedades que aún no están disponibles o que aún no se han implementado por completo.

### Reglas JUnit

Las reglas JUnit se pueden usar para simplificar las pruebas unitarias. Por ejemplo, la regla `@SpringBootTest` se puede usar para cargar un Spring ApplicationContext. La regla `@TestPropertySource` se puede usar para cargar propiedades desde un archivo de propiedades de prueba. La regla `@TempDir` se puede usar para crear un directorio temporal que se eliminará una vez finalizada la prueba.

### AfirmarJ

AssertJ es una poderosa biblioteca de aserciones que se puede usar para escribir pruebas unitarias más legibles y concisas.

## Pruebas de integración

Las pruebas de integración se utilizan para probar la interacción entre los diferentes componentes de la aplicación. Las pruebas de integración suelen ser más lentas que las pruebas unitarias y son más difíciles de escribir y mantener.

Spring Boot proporciona una serie de características que pueden facilitar las pruebas de integración, como:

* La anotación `@SpringBootTest` se puede usar para cargar un Spring ApplicationContext.

* La anotación `@Autowired` se puede usar para inyectar dependencias en la clase de prueba.

* La anotación `@MockBean` se puede usar para inyectar frijoles simulados en el contexto de la aplicación Spring. Esto es útil para simular dependencias que aún no están disponibles o aún no se han implementado por completo.

* La anotación `@TestPropertySource` se puede usar para configurar propiedades para usar en pruebas. Esto es útil para establecer propiedades que aún no están disponibles o que aún no se han implementado por completo.

### Plantilla de descanso de primavera

Spring RestTemplate se puede usar para realizar solicitudes HTTP a una aplicación Spring Boot. El RestTemplate se puede configurar para usar un HttpMessageConverter para convertir automáticamente el cuerpo de la respuesta al tipo deseado.

### AfirmarJ

AssertJ es una poderosa biblioteca de aserciones que se puede usar para escribir pruebas de integración más legibles y concisas.

## Pruebas de extremo a extremo

Las pruebas de extremo a extremo se utilizan para probar la aplicación desde la perspectiva del usuario. Las pruebas de un extremo a otro suelen ser lentas y más difíciles de escribir y mantener.

Spring Boot proporciona una serie de funciones que pueden facilitar las pruebas de extremo a extremo, como:

* La anotación `@SpringBootTest` se puede usar para cargar un Spring ApplicationContext.

* La anotación `@Autowired` se puede usar para inyectar dependencias en la clase de prueba.

* La anotación `@MockBean` se puede usar para inyectar frijoles simulados en el contexto de la aplicación Spring. Esto es útil para simular dependencias que aún no están disponibles o aún no se han implementado por completo.

* La anotación `@TestPropertySource` se puede usar para configurar propiedades para usar en pruebas. Esto es útil para establecer propiedades que aún no están disponibles o que aún no se han implementado por completo.

### Plantilla de descanso de primavera

Spring RestTemplate se puede usar para realizar solicitudes HTTP a una aplicación Spring Boot. El RestTemplate se puede configurar para usar un HttpMessageConverter para convertir automáticamente el cuerpo de la respuesta al tipo deseado.

### AfirmarJ

AssertJ es una poderosa biblioteca de aserciones que se puede usar para escribir pruebas integrales más legibles y concisas.

## Recursos externos

* [Pruebas unitarias en Spring Boot](https://spring.io/blog/2009/12/08/testing-in-spring-boot-apps/)
* [Pruebas de integración en Spring Boot](https://spring.io/blog/2014/05/07/spring-boot-java-config-integration-testing/)
* [Pruebas de un extremo a otro en Spring Boot](https://spring.io/blog/2016/04/15/testing-improvements-in-spring-boot-1-4/)