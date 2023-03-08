---
title: 007: Integración con bases de datos usando Spring Boot e Hibernate
description: 
published: true
date: 2023-02-03T08:04:22.351Z
tags: 
editor: markdown
dateCreated: 2023-02-03T08:04:17.492Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [007: Integrating with databases using Spring Boot and Hibernate***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/007-integrating-with-databases-using-spring-boot-and-hibernate)
{.links-list}


# 007: Integración con bases de datos usando Spring Boot e Hibernate

## Introducción

En esta publicación, aprenderemos cómo integrarse con bases de datos utilizando Spring Boot e Hibernate. Cubriremos los siguientes temas:

* Configuración de Spring Boot para la integración de bases de datos
* Usar Hibernate para acceder a la base de datos
* Creación de una API REST para el acceso a la base de datos

## Configuración de Spring Boot para la integración de la base de datos

Spring Boot facilita la configuración y la conexión a bases de datos. En el archivo application.properties, podemos especificar el controlador de la base de datos, la URL, el nombre de usuario y la contraseña. Por ejemplo, para una base de datos MySQL, la configuración se vería así:

```
spring.datasource.driverClassName=com.mysql.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/test
spring.datasource.username=root
spring.datasource.password=password
```

## Usar Hibernate para acceder a la base de datos

Hibernate es una poderosa herramienta ORM que facilita el acceso y la consulta de bases de datos. En una aplicación Spring Boot, podemos usar la anotación @PersistenceContext de Hibernate para inyectar un EntityManager en nuestros beans. Por ejemplo:

```java
@Service
public class MyService {
    
    @PersistenceContext
    private EntityManager entityManager;
    
    public List<MyEntity> findAll() {
        return entityManager.createQuery("from MyEntity", MyEntity.class)
            .getResultList();
    }
}
```

## Crear una API REST para acceder a la base de datos

Podemos usar Spring MVC para crear fácilmente una API REST para acceder a la base de datos. Por ejemplo, podemos crear un controlador con un punto final para recuperar todas las entidades:

```java
@RestController
@RequestMapping("/api/v1/myentities")
public class MyEntityController {
    
    @Autowired
    private MyService myService;
    
    @GetMapping
    public List<MyEntity> findAll() {
        return myService.findAll();
    }
}
```

## Conclusión

En esta publicación, hemos aprendido cómo integrarse con bases de datos utilizando Spring Boot e Hibernate. Hemos visto cómo configurar Spring Boot para la integración de la base de datos y cómo usar Hibernate para el acceso a la base de datos. Finalmente, hemos creado una API REST para el acceso a la base de datos.