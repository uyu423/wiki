---
title: 057: comprensión y configuración de las propiedades de Spring Boot
description: 
published: true
date: 2023-02-04T20:32:18.720Z
tags: 
editor: markdown
dateCreated: 2023-02-04T20:32:17.137Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [057: Understanding and Configuring Spring Boot's Properties***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/057-understanding-and-configuring-spring-boot-s-properties)
{.links-list}


# Propiedades de arranque de primavera

En esta publicación, veremos las propiedades de Spring Boot. Aprenderemos qué son, cómo configurarlos y cómo se pueden usar para personalizar el comportamiento de las aplicaciones Spring Boot.

## ¿Qué son las propiedades de Spring Boot?

Las propiedades de Spring Boot se utilizan para configurar las aplicaciones de Spring Boot. Se pueden usar para establecer valores para varias configuraciones de Spring Boot, como el nombre de la aplicación, el puerto del servidor, etc.

Las propiedades se pueden configurar de varias maneras, como en un archivo de propiedades, a través de variables de entorno o mediante programación.

## Cómo configurar las propiedades de Spring Boot

Las propiedades de Spring Boot se pueden configurar de varias maneras.

La forma más común es utilizar un archivo de propiedades. Spring Boot buscará un archivo llamado `application.properties` en el classpath. Este archivo se puede usar para anular cualquiera de las propiedades predeterminadas de Spring Boot.

Por ejemplo, el siguiente archivo `application.properties` establecería el puerto del servidor en 8080:

```
server.port=8080
```

Otra forma de configurar las propiedades de Spring Boot es mediante variables de entorno. Spring Boot buscará variables de entorno que comiencen con `spring.` y las usará para anular las propiedades correspondientes.

Por ejemplo, la siguiente variable de entorno establecería el puerto del servidor en 8080:

```
spring.server.port=8080
```

Finalmente, las propiedades de Spring Boot también se pueden configurar mediante programación. Esto se puede hacer creando una clase `@Configuration` y usando la anotación `@ConfigurationProperties`.

Por ejemplo, la siguiente clase `@Configuration` asignaría la propiedad `server.port` a un campo `serverPort`:

```java
@Configuration
@ConfigurationProperties(prefix="server")
public class ServerConfig {

    private int port;

    public int getPort() {
        return port;
    }

    public void setPort(int port) {
        this.port = port;
    }

}
```

## Personalización de aplicaciones Spring Boot

Las propiedades de Spring Boot se pueden usar para personalizar el comportamiento de las aplicaciones de Spring Boot.

Por ejemplo, la propiedad `spring.main.banner-mode` se puede usar para deshabilitar el banner de Spring Boot:

```
spring.main.banner-mode=off
```

La propiedad `spring.jpa.show-sql` se puede usar para habilitar el registro de SQL para JPA:

```
spring.jpa.show-sql=true
```

La propiedad `spring.thymeleaf.cache` se puede usar para habilitar el almacenamiento en caché de plantillas de Thymeleaf:

```
spring.thymeleaf.cache=true
```

Etcétera.

## Conclusión

En esta publicación, hemos aprendido sobre las propiedades de Spring Boot. Hemos visto cómo configurarlos, cómo se pueden usar para personalizar el comportamiento de las aplicaciones Spring Boot y dónde encontrar más información sobre ellos.