---
title: Proceso de configuración automática de Spring Boot
description: 
published: true
date: 2023-02-07T07:32:34.149Z
tags: 
editor: markdown
dateCreated: 2023-02-07T07:32:32.526Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Autoconfiguration Process***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-autoconfiguration-process)
{.links-list}


# Proceso de configuración automática de Spring Boot

La configuración automática de Spring Boot es un proceso que configura automáticamente una aplicación Spring en función de las dependencias que detecta en el classpath. Esta configuración automática se puede ajustar proporcionando una configuración explícita en forma de propiedades, variables de entorno y argumentos de línea de comandos.

Para comprender cómo funciona la configuración automática en Spring Boot, es necesario comprender el concepto de un perfil de Spring. Un perfil es un conjunto de opciones de configuración que se pueden activar en una aplicación Spring. De forma predeterminada, Spring Boot configurará una aplicación basada en el perfil "predeterminado". Sin embargo, se pueden activar otros perfiles usando la propiedad `spring.profiles.active`, configurando variables de entorno o usando argumentos de línea de comandos.

Cuando la configuración automática está habilitada en una aplicación Spring Boot, la aplicación Spring Boot intentará configurarse automáticamente en función de las dependencias que detecte en el classpath. Por ejemplo, si se detecta la dependencia `spring-boot-starter-data-jpa` en el classpath, Spring Boot configurará automáticamente un DataSource y EntityManagerFactory.

En algunos casos, puede ser necesario ajustar el proceso de configuración automática proporcionando una configuración explícita. Esto se puede hacer usando propiedades, variables de entorno y argumentos de línea de comandos.

Por ejemplo, para configurar la fuente de datos que usará EntityManagerFactory, se puede usar la propiedad `spring.datasource.url`.

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/test
```

Alternativamente, se puede usar la variable de entorno `DATASOURCE_URL`.

```
DATASOURCE_URL=jdbc:mysql://localhost:3306/test
```

Finalmente, se puede usar el argumento de la línea de comandos `--spring.datasource.url`.

```
--spring.datasource.url=jdbc:mysql://localhost:3306/test
```

Cuando se proporcionan varias fuentes de configuración, se evalúan en el siguiente orden:

1. Propiedades definidas en `application.properties` o `application.yml`.
2. Propiedades definidas en una clase `@Configuration`.
3. Variables de entorno.
4. Argumentos de la línea de comandos.

El proceso de configuración automática se puede desactivar mediante la anotación `spring.boot.autoconfigure.EnableAutoConfiguration`.

```java
@SpringBootApplication
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }

}
```

En el ejemplo anterior, la anotación `@EnableAutoConfiguration` se usa para habilitar la configuración automática. El atributo `exclude` se utiliza para excluir la clase `DataSourceAutoConfiguration`, que deshabilitará la configuración automática de DataSource.

También es posible deshabilitar la configuración automática para beans específicos usando la anotación `@Conditional`.

```java
@Configuration
@ConditionalOnProperty(name="spring.datasource.url", matchIfMissing=false)
public class DataSourceConfig {

    @Bean
    public DataSource dataSource() {
        // configure and return DataSource
    }

}
```

En el ejemplo anterior, la anotación `@ConditionalOnProperty` se usa para configurar condicionalmente la clase `DataSourceConfig`. El atributo `name` se usa para especificar el nombre de la propiedad que debe verificarse. El atributo `matchIfMissing` se usa para indicar si la condición debe coincidir si falta la propiedad. En este caso, la condición solo coincidirá si se define la propiedad `spring.datasource.url`.

El proceso de configuración automática se puede ajustar aún más proporcionando una configuración explícita en forma de propiedades, variables de entorno y argumentos de línea de comandos.