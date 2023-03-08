---
title: Integrando Hibernate con Spring Boot
description: 
published: true
date: 2023-02-06T07:32:35.445Z
tags: 
editor: markdown
dateCreated: 2023-02-06T07:32:29.632Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Integrating Hibernate with Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/integrating-hibernate-with-spring-boot)
{.links-list}


# Integrando Hibernate con Spring Boot

En este artículo, veremos cómo integrar Hibernate con el marco Spring Boot.

## ¿Qué es Hibernate?

Hibernate es un marco Java que simplifica el desarrollo de la persistencia de aplicaciones Java. Proporciona una poderosa herramienta de mapeo relacional de objetos para almacenar datos en una base de datos relacional.

## ¿Qué es Spring Boot?

Spring Boot es un marco basado en Java que proporciona una forma sencilla de crear aplicaciones basadas en Spring independientes y de grado de producción. Es una excelente opción para crear microservicios.

## ¿Por qué usar Hibernate con Spring Boot?

Hibernate es una opción popular para los desarrolladores de Java que desean usar una base de datos relacional con sus aplicaciones basadas en Spring. Es fácil de configurar y tiene una amplia gama de características, incluido el almacenamiento en caché de objetos y la optimización de consultas.

## Cómo integrar Hibernate con Spring Boot

Hay dos formas de integrar Hibernate con Spring Boot:

### 1. Utilice el soporte integrado de Hibernate de Spring Boot

Spring Boot proporciona soporte integrado para Hibernate. Simplemente puede agregar la siguiente dependencia al archivo `pom.xml` de su proyecto:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

Esto agregará todas las dependencias requeridas para Hibernate, incluidas las bibliotecas Hibernate Core y JPA (API de persistencia de Java).

### 2. Utilice el iniciador Spring Boot específico de Hibernate

Alternativamente, puede usar el iniciador Spring Boot específico de Hibernate, que proporciona un control más detallado sobre la configuración de Hibernate. Para usar este iniciador, agregue la siguiente dependencia al archivo `pom.xml` de su proyecto:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-hibernate</artifactId>
</dependency>
```

## Configuración de Hibernate con Spring Boot

Una vez que haya agregado las dependencias requeridas, puede configurar Hibernate agregando las siguientes propiedades a su archivo `application.properties`:

```properties
# Hibernate settings
spring.jpa.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
spring.jpa.hibernate.ddl-auto=update
```

La propiedad `spring.jpa.hibernate.dialect` configura el dialecto de Hibernate para su uso. Esto le dice a Hibernate cómo traducir los objetos Java a declaraciones SQL.

La propiedad `spring.jpa.hibernate.ddl-auto` configura el modo DDL automático de Hibernate. Esto le dice a Hibernate que genere automáticamente el esquema SQL requerido para las entidades. El modo `actualizar` actualizará el esquema si ha cambiado, pero no lo creará si no existe.

## Creando una entidad de Hibernate

Para crear una entidad de Hibernate, simplemente necesita crear una clase de Java que represente una tabla en su base de datos. Por ejemplo, el siguiente código define una entidad `Usuario`:

```java
@Entity
public class User {
 
    @Id
    @GeneratedValue
    private Long id;
 
    @Column(nullable = false)
    private String name;
 
    // ...
}
```

La anotación `@Entity` marca la clase como una entidad de Hibernate. La anotación `@Id` marca el campo `id` como la clave principal. La anotación `@Column` marca el campo `name` como una columna en la tabla de la base de datos.

## Creando un repositorio de Hibernate

Para crear un repositorio de Hibernate, simplemente necesita crear una interfaz que amplíe la interfaz `CrudRepository`. Por ejemplo, el siguiente código define un `UserRepository`:

```java
public interface UserRepository extends CrudRepository<User, Long> {
}
```

Este repositorio proporciona operaciones CRUD básicas para la entidad `Usuario`.

## Inyectando el repositorio en un servicio

Para inyectar el repositorio en un servicio, puede usar la anotación `@Autowired`. Por ejemplo, el siguiente código inyecta `UserRepository` en un `UserService`:

```java
@Service
public class UserService {
 
    @Autowired
    private UserRepository userRepository;
 
    // ...
}
```

## Usando el repositorio

Una vez que haya inyectado el repositorio en un servicio, puede usarlo para realizar operaciones CRUD en las entidades. Por ejemplo, el siguiente código crea un nuevo `Usuario`:

```java
@Service
public class UserService {
 
    @Autowired
    private UserRepository userRepository;
 
    public User create(String name) {
        User user = new User();
        user.setName(name);
        return userRepository.save(user);
    }
 
    // ...
}
```

## Referencias

- [Hibernar](https://hibernate.org/)
- [Arranque de primavera](https://spring.io/projects/spring-boot)
- [JPA de datos de primavera] (https://docs.spring.io/spring-data/jpa/docs/current/reference/html/# reference)
- [Spring Data Hibernate](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-sql.html# boot-features-hibernate)