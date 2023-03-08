---
title: 074: Integración de Spring Boot con Redis para el almacenamiento en caché y la gestión de sesiones
description: 
published: true
date: 2023-02-02T15:23:31.059Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:23:29.451Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [074: Integrating Spring Boot with Redis for Caching and Session Management***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/074-integrating-spring-boot-with-redis-for-caching-and-session-management)
{.links-list}


# Introducción

En esta publicación, aprenderemos cómo integrar Spring Boot con Redis para el almacenamiento en caché y la administración de sesiones.

El almacenamiento en caché es una técnica que almacena datos a los que se accede con frecuencia en la memoria para que puedan recuperarse rápidamente cuando sea necesario. La gestión de sesiones es el proceso de almacenar y recuperar datos sobre la sesión de un usuario, como las preferencias del usuario o los artículos en su carrito de compras.

Tanto el almacenamiento en caché como la gestión de sesiones se pueden utilizar para mejorar el rendimiento de una aplicación web. Redis es una opción popular tanto para el almacenamiento en caché como para la administración de sesiones porque es rápido, escalable y fácil de usar.

# Instalando Redis

Antes de que podamos comenzar a usar Redis, debemos instalarlo. Redis está disponible para todos los principales sistemas operativos, por lo que puede instalarlo en su máquina de desarrollo, servidor o entorno de nube.

Si está utilizando Linux, puede instalar Redis desde el administrador de paquetes de su distribución. Por ejemplo, en Ubuntu, puede usar apt:

```
sudo apt install redis-server
```

Si usa macOS, puede instalar Redis usando Homebrew:

```
brew install redis
```

Si usa Windows, puede instalar Redis desde Microsoft Store:

```
Get-AppxPackage -AllUsers -Name Microsoft.Portable.Redis | Foreach {Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml"}
```

Una vez que Redis esté instalado, puede iniciar el servidor ejecutando el siguiente comando:

```
redis-server
```

# Configuración de Spring Boot

Ahora que tenemos Redis instalado, podemos configurar Spring Boot para usarlo. Primero, debemos agregar el iniciador spring-boot-starter-data-redis a nuestro proyecto. Este iniciador extraerá las dependencias que necesitamos para usar Redis con Spring Boot.

Si está utilizando Maven, puede agregar el iniciador a su archivo pom.xml:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

Si está utilizando Gradle, puede agregar el iniciador a su archivo build.gradle:

```groovy
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-data-redis'
}
```

Una vez que se agrega el iniciador a nuestro proyecto, debemos configurar Spring Boot para conectarnos a nuestro servidor Redis. Podemos hacer esto agregando las siguientes propiedades a nuestro archivo application.properties:

```
spring.redis.host=localhost
spring.redis.port=6379
```

# Almacenamiento en caché con Redis

Ahora que tenemos Redis configurado, podemos comenzar a usarlo para el almacenamiento en caché. El almacenamiento en caché es una técnica que almacena datos a los que se accede con frecuencia en la memoria para que puedan recuperarse rápidamente cuando sea necesario.

Por ejemplo, supongamos que tenemos una aplicación web que muestra una lista de productos. Cada vez que se carga la página, la aplicación necesita obtener la lista de productos de la base de datos. Esto puede ser lento, especialmente si la base de datos es grande o está ubicada de forma remota.

Podemos acelerar la página almacenando en caché la lista de productos en Redis. Cuando la página se carga por primera vez, la aplicación obtendrá la lista de productos de la base de datos y la almacenará en Redis. Las solicitudes posteriores de la página recuperarán la lista de productos de Redis, que es mucho más rápido que obtenerla de la base de datos.

Para usar Redis para el almacenamiento en caché en Spring Boot, debemos agregar la anotación @EnableCaching a nuestra clase de aplicación principal:

```java
@SpringBootApplication
@EnableCaching
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

También necesitamos crear un administrador de caché. Un administrador de caché es responsable de administrar los cachés en nuestra aplicación. Spring Boot proporciona un RedisCacheManager que se puede usar para administrar cachés de Redis.

Podemos crear un RedisCacheManager anotando un bean con @Bean y @Primary:

```java
@Bean
@Primary
public CacheManager cacheManager(RedisConnectionFactory connectionFactory) {
    return RedisCacheManager.create(connectionFactory);
}
```

# Gestión de sesiones con Redis

Además del almacenamiento en caché, Redis también se puede utilizar para la gestión de sesiones. La gestión de sesiones es el proceso de almacenar y recuperar datos sobre la sesión de un usuario, como las preferencias del usuario o los artículos en su carrito de compras.

Cuando un usuario inicia sesión en una aplicación web, se crea una sesión. Esta sesión se usa para rastrear la actividad del usuario mientras usa la aplicación. Por ejemplo, cuando un usuario agrega un artículo a su carrito de compras, la sesión se usa para almacenar el artículo en el carrito.

Cuando el usuario cierra sesión o la sesión caduca, los datos de la sesión se destruyen.

La gestión de sesiones es importante porque nos permite almacenar datos sobre la sesión de un usuario sin tener que almacenarlos en la base de datos. Esto puede mejorar el rendimiento porque la recuperación de datos de la base de datos puede ser lenta.

Para usar Redis para la administración de sesiones en Spring Boot, debemos agregar la siguiente propiedad a nuestro archivo application.properties:

```
server.servlet.session.store-type=redis
```

Esta propiedad le dice a Spring Boot que use Redis para almacenar datos de sesión.

# Conclusión

En esta publicación, aprendimos cómo integrar Spring Boot con Redis para el almacenamiento en caché y la administración de sesiones. También aprendimos cómo instalar Redis y configurar Spring Boot para usarlo.