---
title: Propiedades de configuración de Spring Boot
description: 
published: true
date: 2023-02-01T21:23:40.584Z
tags: 
editor: markdown
dateCreated: 2023-02-01T21:23:38.944Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Configuration Properties***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-configuration-properties)
{.links-list}


# Introducción

Como desarrollador, probablemente sea consciente de la importancia de la configuración en su aplicación. Los archivos de configuración proporcionan una forma de establecer valores que controlan cómo se comporta su aplicación. Spring Boot facilita el trabajo con las propiedades de configuración al proporcionar un conjunto de herramientas para trabajar con ellas.

En este artículo, veremos qué son las propiedades de configuración de Spring Boot y cómo trabajar con ellas. También veremos algunos de los errores que puede encontrar al trabajar con propiedades de configuración.

# ¿Cuáles son las propiedades de configuración de Spring Boot?

Las propiedades de configuración de Spring Boot son pares clave/valor que se pueden usar para configurar aplicaciones de Spring Boot. Se pueden usar para establecer valores para varias configuraciones de aplicaciones, como la cadena de conexión de la base de datos, el nombre de la aplicación y el puerto del servidor. Las propiedades de configuración se pueden establecer de varias maneras diferentes, incluso a través de variables de entorno, propiedades del sistema y argumentos de línea de comandos.

# ¿Cómo trabajar con las propiedades de configuración de Spring Boot?

Spring Boot proporciona varias formas de trabajar con las propiedades de configuración. En esta sección, veremos algunas de las formas más comunes de trabajar con propiedades de configuración.

## Uso de @ConfigurationProperties

Una forma de trabajar con las propiedades de configuración es usar la anotación `@ConfigurationProperties`. Esta anotación se puede usar en una clase para vincular las propiedades de configuración a los campos de la clase. Por ejemplo, la siguiente clase vincularía la propiedad `spring.datasource.url` al campo `url`:

```java
@ConfigurationProperties(prefix = "spring.datasource")
public class DataSourceConfig {
    private String url;
 
    public String getUrl() {
        return url;
    }
 
    public void setUrl(String url) {
        this.url = url;
    }
}
```

Para usar esta clase, deberá agregarla como un bean en su aplicación Spring Boot:

```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
 
    @Bean
    public DataSourceConfig dataSourceConfig() {
        return new DataSourceConfig();
    }
}
```

## Usando la abstracción del entorno

Otra forma de trabajar con propiedades de configuración es usar la abstracción `Environment`. Esta abstracción proporciona una forma de acceder a las propiedades de configuración sin tener que conocer los nombres de las propiedades específicas. Por ejemplo, el siguiente código obtendría el valor de la propiedad `spring.datasource.url`:

```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
 
    @Autowired
    private Environment environment;
 
    @PostConstruct
    public void init() {
        String dataSourceUrl = environment.getProperty("spring.datasource.url");
    }
}
```

## Usando la anotación @Value

Otra forma de trabajar con las propiedades de configuración es usar la anotación `@Value`. Esta anotación se puede usar en campos para inyectar valores de propiedad de configuración. Por ejemplo, el siguiente código inyectaría el valor de la propiedad `spring.datasource.url` en el campo `url`:

```java
@SpringBootApplication
public class Application {
    @Value("${spring.datasource.url}")
    private String url;
 
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

# Errores de propiedad de configuración de Spring Boot

Hay algunos errores que puede encontrar al trabajar con las propiedades de configuración de Spring Boot. En esta sección, vamos a echar un vistazo a algunos de los más comunes.

## Las propiedades distinguen entre mayúsculas y minúsculas

Las propiedades de configuración de Spring Boot distinguen entre mayúsculas y minúsculas. Esto significa que la propiedad `spring.datasource.url` no es lo mismo que la propiedad `spring.datasource.URL`. Si tiene problemas para que una propiedad funcione, asegúrese de estar utilizando el caso correcto.

## Las propiedades no se resuelven hasta que se inicia la aplicación

Las propiedades de configuración de Spring Boot no se resuelven hasta que se inicia la aplicación. Esto significa que si intenta acceder a una propiedad en el método `principal` de su aplicación, no se resolverá. Por ejemplo, el siguiente código no funcionará:

```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        String dataSourceUrl = System.getProperty("spring.datasource.url");
        SpringApplication.run(Application.class, args);
    }
}
```

Para evitar esto, puede usar la anotación `@PostConstruct`. Esta anotación se puede usar en un método para indicar que se debe llamar después de que se hayan resuelto las propiedades. Por ejemplo:

```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
 
    @PostConstruct
    public void init() {
        String dataSourceUrl = System.getProperty("spring.datasource.url");
    }
}
```

## Las propiedades no se resuelven hasta que se inicializa el contexto de la aplicación

Otro problema a tener en cuenta es que las propiedades no se resuelven hasta que se inicializa el contexto de la aplicación. Esto significa que si intenta acceder a una propiedad en una clase `@Configuration`, no se resolverá. Por ejemplo, el siguiente código no funcionará:

```java
@Configuration
public class MyConfig {
    @Value("${spring.datasource.url}")
    private String url;
}
```

Para evitar esto, puede usar la abstracción `Environment`. Por ejemplo:

```java
@Configuration
public class MyConfig {
    @Autowired
    private Environment environment;
 
    @PostConstruct
    public void init() {
        String dataSourceUrl = environment.getProperty("spring.datasource.url");
    }
}
```

## Las propiedades no se resuelven hasta que la aplicación se inicia por completo

Otro problema a tener en cuenta es que las propiedades no se resuelven hasta que la aplicación se inicia por completo. Esto significa que si intenta acceder a una propiedad en un método `@Bean`, no se resolverá. Por ejemplo, el siguiente código no funcionará:

```java
@Configuration
public class MyConfig {
    @Bean
    public DataSource dataSource() {
        String url = System.getProperty("spring.datasource.url");
        // ...
    }
}
```

Para evitar esto, puede usar la abstracción `Environment`. Por ejemplo:

```java
@Configuration
public class MyConfig {
    @Autowired
    private Environment environment;
 
    @Bean
    public DataSource dataSource() {
        String url = environment.getProperty("spring.datasource.url");
        // ...
    }
}
```

# Conclusión

En este artículo, hemos analizado qué son las propiedades de configuración de Spring Boot y cómo trabajar con ellas. También hemos analizado algunos de los errores que puede encontrar al trabajar con propiedades de configuración.

Configurar las aplicaciones de Spring Boot puede ser complicado, pero esperamos que este artículo le haya brindado la información que necesita para comenzar.