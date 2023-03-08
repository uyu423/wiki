---
title: 063: Prueba de una aplicación Spring Boot con JUnit y Mockito
description: 
published: true
date: 2023-02-05T01:32:28.042Z
tags: 
editor: markdown
dateCreated: 2023-02-05T01:32:25.525Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [063: Testing a Spring Boot Application with JUnit and Mockito***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/063-testing-a-spring-boot-application-with-junit-and-mockito)
{.links-list}


# 063: Prueba de una aplicación Spring Boot con JUnit y Mockito

En esta publicación, aprenderemos cómo probar una aplicación Spring Boot con JUnit y Mockito.

Spring Boot facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción que puede "simplemente ejecutar". Usaremos Spring Boot en este ejemplo para hacer las cosas aún más fáciles.

JUnit es un marco de prueba popular para Java. Mockito es un marco de simulación para Java que le permite crear objetos simulados y métodos de código auxiliar.

## Configuración del proyecto

Primero, crearemos un nuevo proyecto Spring Boot usando [Spring Initializr](https://start.spring.io/). Llamaremos a nuestro proyecto `spring-boot-junit-mockito-example`.

![Inicializar resorte](https://i.imgur.com/HgflTDz.png)

A continuación, seleccionaremos las dependencias `Web` y `Actuator`. La dependencia `Web` agregará soporte para aplicaciones web y la dependencia `Actuator` agregará soporte para monitorear y administrar nuestra aplicación.

![Dependencias de Spring Initializr](https://i.imgur.com/sA6qEjK.png)

Una vez generado el proyecto, podemos importarlo a nuestro IDE favorito. Estoy usando [IntelliJ IDEA](https://www.jetbrains.com/idea/).

## Escribir las pruebas

Ahora que nuestro proyecto está configurado, podemos comenzar a escribir nuestras pruebas. Crearemos un nuevo directorio `src/test/java` y agregaremos un nuevo archivo `SpringBootJunitMockitoExampleApplicationTests.java`.

En este archivo, agregaremos una prueba simple que verifique que nuestra aplicación Spring Boot se pueda iniciar.

    @RunWith(SpringRunner.clase)
    @SpringBootTest
    clase pública SpringBootJunitMockitoExampleApplicationTests {
    
        @Prueba
        public void contextLoads() {
        }
    
    }

Anotamos nuestra clase de prueba con `@RunWith(SpringRunner.class)` y `@SpringBootTest`. La anotación `@RunWith` le dice a JUnit que use la clase `SpringRunner` para ejecutar nuestras pruebas. La anotación `@SpringBootTest` le dice a Spring Boot que cargue el contexto de nuestra aplicación.

El método de prueba `contextLoads()` verifica que el contexto se puede cargar.

Podemos ejecutar nuestras pruebas usando el comando `mvn test`.

![Ejecución de las pruebas](https://i.imgur.com/VkzcTGi.png)

## Escribir una prueba unitaria

Ahora que hemos verificado que nuestra aplicación se puede iniciar, podemos escribir una prueba unitaria. Una prueba unitaria es una prueba que verifica el comportamiento de una sola unidad de código, como un método.

Crearemos un nuevo directorio `src/test/java` y agregaremos un nuevo archivo `CalculatorTest.java`. En este archivo, agregaremos una prueba para el método `add()` de nuestra clase `Calculator`.

    @RunWith(MockitoJUnitRunner.clase)
    prueba de calculadora de clase pública {
    
        @InyectarMocks
        Calculadora calculadora privada;
    
        @Prueba
        public void testAdd() {
            afirmarEquals(5, calculadora.añadir(2, 3));
        }
    
    }

Anotamos nuestra clase de prueba con `@RunWith(MockitoJUnitRunner.class)`. Esto le dice a Mockito que use la clase `MockitoJUnitRunner` para ejecutar nuestras pruebas.

La anotación `@InjectMocks` inyecta objetos simulados en nuestra clase `Calculator`. La anotación `@Test` le dice a JUnit que el método `testAdd()` es una prueba.

En el método `testAdd()`, usamos el método `assertEquals()` para verificar que el método `add()` devuelve el valor esperado.

Podemos ejecutar nuestras pruebas usando el comando `mvn test`.

![Ejecución de las pruebas](https://i.imgur.com/5BQ7UgI.png)

## Escribir una prueba de integración

Ahora que hemos verificado que nuestra clase 'Calculadora' funciona como se esperaba, podemos escribir una prueba de integración. Una prueba de integración es una prueba que verifica el comportamiento de dos o más unidades de código.

Crearemos un nuevo directorio `src/test/java` y agregaremos un nuevo archivo `CalculatorIntegrationTest.java`. En este archivo, agregaremos una prueba para el método `add()` de nuestra clase `Calculator`.

    @RunWith(SpringRunner.clase)
    @SpringBootTest
    prueba de integración de calculadora de clase pública {
    
        @autocableado
        Calculadora calculadora privada;
    
        @Prueba
        public void testAdd() {
            afirmarEquals(5, calculadora.añadir(2, 3));
        }
    
    }

Anotamos nuestra clase de prueba con `@RunWith(SpringRunner.class)` y `@SpringBootTest`. La anotación `@RunWith` le dice a JUnit que use la clase `SpringRunner` para ejecutar nuestras pruebas. La anotación `@SpringBootTest` le dice a Spring Boot que cargue el contexto de nuestra aplicación.

La anotación `@Autowired` inyecta el bean `Calculator` en nuestra clase de prueba. La anotación `@Test` le dice a JUnit que el método `testAdd()` es una prueba.

En el método `testAdd()`, usamos el método `assertEquals()` para verificar que el método `add()` devuelve el valor esperado.

Podemos ejecutar nuestras pruebas usando el comando `mvn test`.

![Ejecución de las pruebas](https://i.imgur.com/p7Aj0bU.png)

## Conclusión

En esta publicación, hemos aprendido cómo probar una aplicación Spring Boot con JUnit y Mockito. También hemos visto cómo escribir pruebas unitarias y pruebas de integración.