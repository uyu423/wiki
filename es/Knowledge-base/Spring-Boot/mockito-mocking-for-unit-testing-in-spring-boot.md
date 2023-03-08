---
title: Mockito: Simulacro para pruebas unitarias en Spring Boot
description: 
published: true
date: 2023-02-01T17:48:04.870Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:48:00.829Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Mockito: Mocking for Unit Testing in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/mockito-mocking-for-unit-testing-in-spring-boot)
{.links-list}


# Mockito: Simulacro para pruebas unitarias en Spring Boot

La simulación es un concepto clave en las pruebas unitarias que permite a los desarrolladores centrarse en probar la funcionalidad de una unidad de código específica, en lugar de sus dependencias. En el contexto de las aplicaciones Spring Boot, Mockito se puede usar para simular beans y servicios para probar la funcionalidad de un componente específico sin necesidad de iniciar todo el contexto Spring.

En este artículo, veremos cómo usar Mockito para simular beans y servicios en una aplicación Spring Boot. También veremos cómo configurar Mockito para iniciar el contexto Spring automáticamente.

## ¿Qué es Mockito?

Mockito es un marco de prueba simulado popular para Java. Mockito permite a los desarrolladores crear y configurar objetos simulados para usar en pruebas unitarias. Mockito se puede usar para simular interfaces, clases e incluso clases y métodos finales.

## Burlarse de frijoles y servicios en Spring Boot

Burlarse de beans y servicios en Spring Boot es fácil con Mockito. En el siguiente ejemplo, imitaremos un bean llamado `myBean`:

```java
@MockBean
MyBean myBean;

@Test
public void testMyBean() {
    // configure mock object
    when(myBean.getName()).thenReturn("Mockito");
    
    // invoke method on mock object
    String name = myBean.getName();
    
    // verify results
    assertThat(name).isEqualTo("Mockito");
}
```

En el ejemplo anterior, usamos la anotación `@MockBean` para crear un objeto simulado de la clase `MyBean`. Luego usamos los métodos `when` y `thenReturn` para configurar el objeto simulado. Finalmente, invocamos el método `getName` en el objeto simulado y afirmamos que el valor devuelto es el esperado.

## Configurando Mockito en Spring Boot

Mockito se puede configurar en Spring Boot usando las dependencias `mockito-core` y `mockito-spring`. En el archivo `pom.xml`, agregue las siguientes dependencias:

```xml
<dependencies>
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-core</artifactId>
        <version>2.13.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-spring</artifactId>
        <version>1.9.5</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

La dependencia `mockito-core` contiene la biblioteca Mockito, mientras que la dependencia `mockito-spring` contiene la integración entre Mockito y Spring.

## Conclusión

En este artículo, hemos visto cómo usar Mockito para simular beans y servicios en una aplicación Spring Boot. También hemos visto cómo configurar Mockito para iniciar el contexto Spring automáticamente.