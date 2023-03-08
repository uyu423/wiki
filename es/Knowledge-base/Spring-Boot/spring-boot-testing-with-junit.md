---
title: Prueba de arranque de primavera con JUnit
description: 
published: true
date: 2023-02-07T19:32:31.718Z
tags: 
editor: markdown
dateCreated: 2023-02-07T19:32:25.888Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Testing with JUnit***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-testing-with-junit)
{.links-list}


# Prueba de arranque de primavera con JUnit

La prueba es una parte crítica de cualquier proceso de desarrollo de software. Ayuda a garantizar que su código funcione como se espera y ayuda a detectar errores desde el principio.

JUnit es un marco de prueba de unidad popular para Java. Spring Boot proporciona soporte de primera clase para pruebas JUnit. En este artículo, veremos cómo configurar y escribir pruebas Spring Boot con JUnit.

## Configuración

Para comenzar, deberá agregar las siguientes dependencias a su `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

La dependencia `spring-boot-starter-test` incluye varias bibliotecas útiles para escribir pruebas, incluidas JUnit, Hamcrest y Mockito.

## Pruebas de escritura

Las pruebas Spring Boot se pueden escribir en JUnit 4 o JUnit 5. En esta sección, veremos un ejemplo de cada uno.

### JUnidad 4

Aquí hay un ejemplo simple de una prueba JUnit 4:

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class MyTest {

    @Test
    public void test() {
        // test code goes here
    }

}
```

La anotación `@RunWith` se usa para especificar qué marco de prueba usar. La anotación `@SpringBootTest` le dice a Spring Boot que cargue el contexto de la aplicación para la prueba.

La anotación `@Test` se utiliza para marcar un método como método de prueba.

### JUnidad 5

Las pruebas JUnit 5 se parecen a las pruebas JUnit 4, pero con algunas diferencias clave:

```java
@SpringBootTest
public class MyTest {

    @Test
    public void test() {
        // test code goes here
    }

}
```

Primero, la anotación `@RunWith` ya no es necesaria. En segundo lugar, la anotación `@Test` ahora pertenece al paquete `org.junit.jupiter.api`.

JUnit 5 también presenta un nuevo conjunto de afirmaciones, que se pueden encontrar en la clase `org.junit.jupiter.api.Assertions`. Por ejemplo, la afirmación `assertEquals` se puede usar así:

```java
assertEquals(expected, actual);
```

## TestingSpringBootApplicationPruebas

Spring Boot proporciona una serie de anotaciones útiles para escribir pruebas. En esta sección, echaremos un vistazo a algunas de las anotaciones más utilizadas.

### @WebMvcTest

La anotación `@WebMvcTest` se usa para probar los controladores Spring MVC. Se puede usar así:

```java
@WebMvcTest(MyController.class)
public class MyControllerTest {

    @Autowired
    private MockMvc mvc;

    @Test
    public void test() {
        // test code goes here
    }

}
```

La anotación `@WebMvcTest` solo cargará los componentes necesarios para probar Spring MVC. Esto puede ser útil para reducir el tiempo que lleva cargar el contexto de la aplicación para las pruebas.

La anotación `@Autowired` se usa para inyectar el bean `MockMvc`. El bean `MockMvc` se puede usar para enviar solicitudes HTTP al controlador y verificar la respuesta.

### @DataJpaTest

La anotación `@DataJpaTest` se usa para probar los repositorios Spring Data JPA. Se puede usar así:

```java
@DataJpaTest
public class MyRepositoryTest {

    @Autowired
    private MyRepository repository;

    @Test
    public void test() {
        // test code goes here
    }

}
```

La anotación `@DataJpaTest` solo cargará los componentes necesarios para probar Spring Data JPA. Esto puede ser útil para reducir el tiempo que lleva cargar el contexto de la aplicación para las pruebas.

La anotación `@Autowired` se usa para inyectar el bean `MyRepository`. Este bean se puede utilizar para acceder a los datos de la base de datos.

### @RestClientTest

La anotación `@RestClientTest` se usa para probar los clientes de Spring RestTemplate. Se puede usar así:

```java
@RestClientTest(MyClient.class)
public class MyClientTest {

    @Autowired
    private MockRestTemplate template;

    @Test
    public void test() {
        // test code goes here
    }

}
```

La anotación `@RestClientTest` solo cargará los componentes necesarios para probar Spring RestTemplate. Esto puede ser útil para reducir el tiempo que lleva cargar el contexto de la aplicación para las pruebas.

La anotación `@Autowired` se usa para inyectar el bean `MockRestTemplate`. El bean `MockRestTemplate` se puede usar para enviar solicitudes HTTP al cliente y verificar la respuesta.

## Conclusión

En este artículo, hemos visto cómo configurar y escribir pruebas con Spring Boot y JUnit. También hemos visto algunas de las anotaciones más utilizadas para escribir pruebas.