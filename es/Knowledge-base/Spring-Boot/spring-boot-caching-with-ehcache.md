---
title: Caché Spring Boot con EhCache
description: 
published: true
date: 2023-02-07T16:32:42.008Z
tags: 
editor: markdown
dateCreated: 2023-02-07T16:32:36.252Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Caching with EhCache***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-caching-with-ehcache)
{.links-list}


# Almacenamiento en caché Spring Boot con EhCache

El almacenamiento en caché es una técnica común para mejorar el rendimiento y la escalabilidad de las aplicaciones. Se puede usar para almacenar en caché los datos a los que se accede con frecuencia en la memoria para que se puedan recuperar rápidamente sin tener que consultar la base de datos.

Cuando usamos Spring Boot, podemos usar la anotación @EnableCaching para habilitar EhCache en nuestra aplicación. En este artículo, veremos cómo configurar y usar EhCache con Spring Boot.

## Configuración de EhCache

Para configurar EhCache, necesitamos crear un archivo ehcache.xml en el directorio src/main/resources. El contenido del archivo debería verse así:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:noNamespaceSchemaLocation="ehcache.xsd"
         updateCheck="true"
         monitoring="autodetect"
         dynamicConfig="true">
    <diskStore path="java.io.tmpdir"/>
    <cache name="defaultCache"
           maxElementsInMemory="10000"
           overflowToDisk="true"
           eternal="false"
           timeToIdleSeconds="120"
           timeToLiveSeconds="120"
           diskPersistent="false"
           diskExpiryThreadIntervalSeconds="120"
           memoryStoreEvictionPolicy="LRU">
        <persistence strategy="localTempSwap"/>
    </cache>
</ehcache>
```

En el archivo ehcache.xml, hemos configurado un caché llamado "defaultCache". Esta caché será utilizada por nuestra aplicación para almacenar datos en caché. La memoria caché está configurada para usar un almacén de disco local para el desbordamiento y para hacer caducar las entradas a las que no se ha accedido en 120 segundos.

## Almacenamiento en caché con Spring Boot

Ahora que tenemos EhCache configurado, podemos usarlo en nuestra aplicación Spring Boot. Primero, debemos agregar la anotación @EnableCaching a nuestra clase de aplicación:

```java
@SpringBootApplication
@EnableCaching
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

A continuación, debemos anotar los métodos en nuestras clases de servicio que queremos almacenar en caché con la anotación @Cacheable:

```java
@Service
public class UserService {

    @Cacheable(value = "users")
    public List<User> getUsers() {
        // query database for users
        return users;
    }
}
```

En el código anterior, hemos anotado el método getUsers() con @Cacheable. Esto le dice a Spring que almacene en caché los resultados de este método en el caché de "usuarios".

Ahora, cuando llamemos al método getUsers(), la primera vez consultará la base de datos y devolverá los resultados. La segunda vez que lo llamemos, devolverá los resultados del caché.

## Actualización de datos en caché

Es importante tener en cuenta que cuando se actualizan los datos en la base de datos, los datos almacenados en caché no se actualizarán automáticamente. Para actualizar el caché, necesitamos usar la anotación @CacheEvict:

```java
@Service
public class UserService {

    @CacheEvict(value = "users", allEntries = true)
    public void updateUser(User user) {
        // update user in database
    }
}
```

En el código anterior, hemos anotado el método updateUser() con @CacheEvict. Esto le dice a Spring que elimine todas las entradas del caché de "usuarios" cuando se llama a este método.

Ahora, cuando llamemos al método updateUser(), la memoria caché se borrará y la próxima vez que llamemos al método getUsers(), consultará la base de datos y devolverá los resultados actualizados.

## Conclusión

En este artículo, hemos visto cómo configurar y usar EhCache con Spring Boot. El almacenamiento en caché puede ser una excelente manera de mejorar el rendimiento de su aplicación. Al almacenar en caché los datos a los que se accede con frecuencia en la memoria, puede evitar tener que consultar la base de datos cada vez.