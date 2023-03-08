---
title: Prueba de arranque de primavera con Mockito
description: 
published: true
date: 2023-02-02T00:23:22.492Z
tags: 
editor: markdown
dateCreated: 2023-02-02T00:23:20.929Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Testing with Mockito***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-testing-with-mockito)
{.links-list}


# Prueba de arranque de primavera con Mockito

Spring Boot proporciona una excelente manera de escribir pruebas para su aplicación. En este artículo, veremos cómo usar Mockito para probar su aplicación Spring Boot.

Mockito es un poderoso marco de simulación para Java. Es muy popular en la comunidad de Spring. Mockito nos permite escribir pruebas que están aisladas del mundo exterior. Esto es muy importante cuando queremos probar nuestra lógica de negocio sin depender de servicios externos.

## Configurar Mockito

Primero, necesitamos agregar la dependencia de Mockito a nuestro `pom.xml`:

```xml
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>2.0.0-beta.19</version>
    <scope>test</scope>
</dependency>
```

Ahora podemos crear un `MockitoJUnitRunner` para ejecutar nuestras pruebas:

```java
import org.junit.runner.RunWith;
import org.mockito.runners.MockitoJUnitRunner;

@RunWith(MockitoJUnitRunner.class)
public class MyTest {
}
```

## Usar Mockito con Spring Boot

Mockito es muy fácil de usar con Spring Boot. Simplemente podemos anotar nuestra clase de prueba con `@MockBean` para crear un simulacro de Spring Bean:

```java
@RunWith(MockitoJUnitRunner.class)
public class MyTest {

    @MockBean
    private MyService myService;
}
```

Luego podemos usar Mockito para aplicar stub a los métodos de `MyService`:

```java
@RunWith(MockitoJUnitRunner.class)
public class MyTest {

    @MockBean
    private MyService myService;

    @Test
    public void testMyService() {
        // given
        given(myService.doSomething()).willReturn("Hello world!");

        // when
        String result = myService.doSomething();

        // then
        assertThat(result).isEqualTo("Hello world!");
    }
}
```

## Conclusión

En este artículo, hemos visto cómo usar Mockito para probar una aplicación Spring Boot. Mockito es una herramienta muy poderosa que puede ayudarnos a escribir mejores pruebas.