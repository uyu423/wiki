---
title: Pruebas unitarias en Spring Boot con JUnit
description: 
published: true
date: 2023-02-01T17:27:43.850Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:27:41.272Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Unit Testing in Spring Boot with JUnit***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/unit-testing-in-spring-boot-with-junit)
{.links-list}


# Pruebas unitarias en Spring Boot con JUnit

La prueba unitaria es un método de prueba de software en el que las unidades/componentes individuales de un software se prueban para verificar que cada unidad funcione como se espera. Una unidad es la parte comprobable más pequeña de una aplicación. En Spring Boot, las pruebas unitarias generalmente se escriben usando JUnit.

JUnit es un marco de prueba popular para Java. Es un proyecto de código abierto alojado en Github. JUnit ha sido importante en el desarrollo del desarrollo basado en pruebas y es uno de una familia de marcos de trabajo de pruebas unitarias que se conoce colectivamente como xUnit que se originó con SUnit.

En este artículo, veremos cómo realizar una prueba unitaria de una aplicación Spring Boot utilizando JUnit. Escribiremos una prueba simple para probar un punto final RestController. El código de ejemplo de este artículo se puede encontrar en Github.

## Configuración del proyecto

Comenzaremos configurando un proyecto Spring Boot simple. Usaremos Spring Initializr para generar nuestro proyecto. Seleccionaremos las siguientes dependencias:

- Internet
- JPA
- Base de datos H2
- Lombok

Lombok es una biblioteca que se puede utilizar para reducir el código repetitivo en aplicaciones Java. Lo usaremos para reducir la cantidad de código que necesitamos escribir para nuestras pruebas.

Una vez que se genera el proyecto, podemos importarlo a nuestro IDE de elección. Usaré IntelliJ IDEA.

## Escribir la prueba unitaria

Ahora que tenemos nuestro proyecto configurado, podemos escribir nuestra prueba unitaria. Comenzaremos creando un nuevo paquete para nuestras pruebas, `com.example.demo.controller`. En este paquete, crearemos una nueva clase, `DemoControllerTest`.

Esta clase se anotará con `@RunWith(SpringRunner.class)` y `@WebMvcTest(DemoController.class)`. La anotación `@RunWith` le dice a JUnit que use la clase `SpringRunner` para ejecutar nuestras pruebas. La anotación `@WebMvcTest` se usa para probar los controladores Spring MVC. Configurará automáticamente Spring MVC y deshabilitará la configuración automática completa.

En nuestra clase `DemoControllerTest`, crearemos un campo `@Autowired` para nuestro objeto `MockMvc`. `MockMvc` se usa para realizar solicitudes HTTP a nuestro controlador y afirmar la respuesta. También crearemos un método `@Before` anotado con `@BeforeEach`. Este método se usará para inicializar nuestro objeto `MockMvc`.

```java
@RunWith(SpringRunner.class)
@WebMvcTest(DemoController.class)
public class DemoControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @BeforeEach
    public void setup() {
        mockMvc = MockMvcBuilders.webAppContextSetup(webApplicationContext)
                .build();
    }
}
```

En nuestro método `setup`, usamos los métodos de fábrica estáticos `MockMvcBuilders` para crear una instancia `MockMvc`. Usamos el método `webAppContextSetup` y pasamos nuestro `WebApplicationContext`. Esto creará una instancia `MockMvc` respaldada por un `WebApplicationContext`.

Ahora que tenemos configurado nuestro objeto `MockMvc`, podemos escribir nuestro método de prueba. Anotaremos nuestro método con `@Test`. En nuestro método de prueba, usaremos el objeto `MockMvc` para realizar una solicitud HTTP `GET` a nuestro punto final `/demo`. Entonces afirmaremos que el estado de la respuesta es `200 OK` y que el contenido de la respuesta contiene la cadena `¡Hola, mundo!`.

```java
@Test
public void testDemoEndpoint() throws Exception {
    mockMvc.perform(get("/demo"))
            .andExpect(status().isOk())
            .andExpect(content().string(containsString("Hello, world!")));
}
```

Usamos el método `perform` en nuestro objeto `MockMvc` para realizar una solicitud HTTP. Usamos el método `get` para crear una solicitud `GET`. Luego usamos los métodos `andExpect` para afirmar el estado y el contenido de la respuesta.

## Ejecutando la prueba

Ahora podemos ejecutar nuestra prueba. Podemos ejecutar nuestra prueba desde la línea de comandos usando el comando `./mvnw test`. También podemos ejecutar nuestra prueba desde nuestro IDE.

## Conclusión

En este artículo, hemos visto cómo realizar pruebas unitarias de una aplicación Spring Boot utilizando JUnit. Hemos escrito una prueba simple para probar un punto final RestController.