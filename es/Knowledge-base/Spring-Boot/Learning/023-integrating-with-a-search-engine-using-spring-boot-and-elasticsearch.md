---
title: 023: Integración con un motor de búsqueda usando Spring Boot y Elasticsearch
description: 
published: true
date: 2023-02-03T15:32:38.155Z
tags: 
editor: markdown
dateCreated: 2023-02-03T15:32:36.512Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [023: Integrating with a search engine using Spring Boot and Elasticsearch***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/023-integrating-with-a-search-engine-using-spring-boot-and-elasticsearch)
{.links-list}


# Integración con un motor de búsqueda usando Spring Boot y Elasticsearch

En esta publicación, aprenderemos cómo integrar una aplicación Spring Boot con un motor de búsqueda usando Elasticsearch.

## ¿Qué es Elasticsearch?

Elasticsearch es un motor de análisis y búsqueda RESTful distribuido basado en Apache Lucene. Proporciona un poderoso conjunto de funciones para implementar búsquedas de texto completo y análisis en grandes conjuntos de datos.

## ¿Por qué usar Elasticsearch?

Elasticsearch es una opción popular para implementar un motor de búsqueda debido a su facilidad de uso, escalabilidad y rendimiento.

## Configuración de Elasticsearch

Antes de que podamos comenzar a usar Elasticsearch, debemos configurarlo.

Hay dos formas de configurar Elasticsearch:

1. Descargue e instale Elasticsearch desde el [sitio web oficial] (https://www.elastic.co/downloads/elasticsearch).
2. Utilice la [imagen de Docker](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html).

Usaremos la imagen de Docker en esta publicación.

## Ejecutando Elasticsearch

Para ejecutar la imagen de Elasticsearch Docker, use el siguiente comando:

```
$ docker run -d -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.4.0
```

Esto iniciará un contenedor que ejecuta Elasticsearch 7.4.0 en el puerto 9200.

## Conexión a Elasticsearch

Ahora que Elasticsearch está funcionando, podemos comenzar a usarlo en nuestra aplicación Spring Boot.

Para conectarnos a Elasticsearch desde Spring Boot, necesitamos agregar la siguiente dependencia a nuestro `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-elasticsearch</artifactId>
</dependency>
```

Esta dependencia agregará las bibliotecas necesarias para conectarse y usar Elasticsearch en nuestra aplicación.

## Configuración de Elasticsearch

Una vez que tengamos la dependencia `spring-boot-starter-data-elasticsearch` en nuestro proyecto, debemos configurar Elasticsearch.

Podemos configurar Elasticsearch agregando las siguientes propiedades a nuestro archivo `application.properties`:

```properties
spring.data.elasticsearch.cluster-nodes=localhost:9300
spring.data.elasticsearch.cluster-name=docker-cluster
```

Esto configurará nuestra aplicación para conectarse al clúster de Elasticsearch que se ejecuta en `localhost:9300`.

## Creando una aplicación Spring Boot

Ahora que tenemos instalado y configurado Elasticsearch, podemos crear una aplicación Spring Boot que lo use.

Comenzaremos creando una clase `Usuario`:

```java
@Document(indexName = "user", type = "user")
public class User {

    @Id
    private String id;

    private String name;

    private Integer age;

    // getters and setters
}
```

Esta clase representa un usuario en nuestra aplicación. Note que lo hemos anotado con `@Document`. Esto le dice a Spring Data Elasticsearch que este es un documento que debe indexarse en Elasticsearch.

También hemos anotado el campo `id` con `@Id`. Esto le dice a Spring Data Elasticsearch que este es el identificador único para este documento.

A continuación, crearemos una interfaz `UserRepository`:

```java
public interface UserRepository extends ElasticsearchRepository<User, String> {

}
```

Esta interfaz amplía `ElasticsearchRepository`, que nos brinda un poderoso conjunto de métodos para interactuar con Elasticsearch.

Finalmente, crearemos una clase `UserService`:

```java
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public void saveUser(User user) {
        userRepository.save(user);
    }

    public void deleteUser(User user) {
        userRepository.delete(user);
    }

    public Iterable<User> getAllUsers() {
        return userRepository.findAll();
    }

    public User getUserById(String id) {
        return userRepository.findById(id).orElse(null);
    }
}
```

Esta clase proporciona métodos para crear, recuperar y eliminar usuarios en nuestra aplicación. Tenga en cuenta que lo hemos anotado con `@Service`. Esto le dice a Spring que este es un bean de servicio que debe ser administrado por el contenedor de Spring.

También hemos anotado el campo `userRepository` con `@Autowired`. Esto le dice a Spring que inyecte una instancia de `UserRepository` en este campo cuando se crea el bean.

## Creación e indexación de documentos

Ahora que tenemos nuestra aplicación Spring Boot configurada, podemos comenzar a crear e indexar documentos en Elasticsearch.

Comenzaremos creando una instancia de `Usuario`:

```java
User user = new User();
user.setId("1");
user.setName("John Doe");
user.setAge(20);
```

A continuación, guardaremos este usuario en nuestra base de datos:

```java
userService.saveUser(user);
```

Esto guardará al usuario en nuestra base de datos e indexará el documento en Elasticsearch.

## Búsqueda de documentos

Una vez que tenemos los documentos indexados en Elasticsearch, podemos comenzar a buscarlos.

Elasticsearch proporciona un potente DSL de consulta (lenguaje específico del dominio) para buscar documentos.

Podemos usar el método `search()` en nuestro `UserRepository` para ejecutar una consulta de búsqueda:

```java
SearchQuery searchQuery = new NativeSearchQueryBuilder()
        .withQuery(QueryBuilders.queryStringQuery("John Doe"))
        .build();

List<User> users = userRepository.search(searchQuery).getContent();
```

Esta consulta buscará todos los documentos que contengan la frase "John Doe".

El método `search()` devuelve un objeto `SearchResponse`, que contiene los resultados de la consulta de búsqueda. Podemos usar el método `getContent()` para obtener una lista de objetos `Usuario` que coincidan con la consulta de búsqueda.

## Actualización de documentos

También podemos usar Elasticsearch para actualizar documentos.

Para actualizar un documento, primero debemos recuperarlo de la base de datos:

```java
User user = userService.getUserById("1");
```

A continuación, actualizaremos el documento:

```java
user.setAge(21);
```

Finalmente, guardaremos el documento actualizado en la base de datos:

```java
userService.saveUser(user);
```

Esto actualizará el documento en la base de datos y en Elasticsearch.

## Eliminación de documentos

También podemos usar Elasticsearch para eliminar documentos.

Para eliminar un documento, primero debemos recuperarlo de la base de datos:

```java
User user = userService.getUserById("1");
```

A continuación, eliminaremos el documento:

```java
userService.deleteUser(user);
```

Esto eliminará el documento de la base de datos y de Elasticsearch.

## Conclusión

En esta publicación, hemos aprendido cómo integrar una aplicación Spring Boot con un motor de búsqueda usando Elasticsearch. También aprendimos cómo crear, indexar, actualizar y eliminar documentos en Elasticsearch.