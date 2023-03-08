---
title: 005: Trabajar con Spring Boot y Spring Data JPA
description: 
published: true
date: 2023-02-03T07:43:44.957Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:43:43.290Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [005: Working with Spring Boot and Spring Data JPA***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/005-working-with-spring-boot-and-spring-data-jpa)
{.links-list}


# Trabajar con Spring Boot y Spring Data JPA

En esta publicación, veremos cómo trabajar con Spring Boot y Spring Data JPA.

Comenzaremos analizando qué es JPA y por qué querríamos usarlo. Luego, veremos cómo configurar Spring Boot para que funcione con JPA. Finalmente, escribiremos algunos programas de ejemplo simples para mostrar cómo usar JPA en una aplicación Spring Boot.

## ¿Qué es JPA?

JPA es la API de persistencia de Java. Es una especificación sobre cómo asignar objetos Java a una base de datos relacional.

Hay muchas implementaciones de JPA, la más popular es Hibernate. Cuando usa JPA, puede escribir su código contra la API de JPA y dejar que la implementación de JPA (como Hibernate) maneje los detalles del mapeo de sus objetos a la base de datos.

## ¿Por qué usar JPA?

Hay algunas razones por las que podría querer usar JPA en sus aplicaciones:

- **JPA es un estándar**. Esto significa que hay muchas implementaciones de JPA para elegir, y puede cambiar las implementaciones si lo necesita.

- **JPA es flexible**. Puede usar JPA con diferentes tipos de bases de datos y puede asignar sus objetos Java a la base de datos de diferentes maneras.

- **JPA es fácil de usar**. La API de JPA está diseñada para que sea fácil de usar, por lo que puede comenzar a usar JPA rápidamente.

## Configuración de Spring Boot para JPA

Spring Boot facilita la configuración de Spring para su uso con JPA. Todo lo que necesita hacer es agregar la dependencia spring-boot-starter-data-jpa a su proyecto.

Esta dependencia extraerá todas las dependencias JPA necesarias y también configurará Spring Boot para usar una implementación JPA (Hibernate, de forma predeterminada).

## Uso de JPA en Spring Boot

Ahora que tenemos Spring Boot configurado para usar JPA, escribamos algunos programas de ejemplo para mostrar cómo usar JPA en una aplicación Spring Boot.

### Ejemplo 1: Creación de una entidad JPA

Para usar JPA en su aplicación, debe crear una entidad JPA. Una entidad JPA es una clase de Java que se asigna a una tabla de base de datos.

Vamos a crear una entidad JPA simple:

```java
@Entity
public class Person {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    // ... getters and setters
}
```

Esta clase está asignada a la tabla `persona` en la base de datos. La anotación `@Entity` indica que se trata de una entidad JPA. La anotación `@Id` indica que el campo `id` es la clave principal de la entidad. La anotación `@GeneratedValue` le dice a JPA que genere una identificación única para cada entidad.

### Ejemplo 2: Creación de un repositorio JPA

Ahora que tenemos nuestra entidad JPA, necesitamos una forma de acceder a ella. Podemos hacer esto creando un repositorio JPA.

Un repositorio JPA es un repositorio Spring Data que se utiliza para acceder a las entidades JPA. Para crear un repositorio JPA, necesitamos crear una interfaz que amplíe la interfaz `JpaRepository`:

```java
public interface PersonRepository extends JpaRepository<Person, Long> {

}
```

Esta interfaz se utiliza para acceder a la entidad `Persona`. La interfaz `JpaRepository` proporciona muchos métodos para trabajar con entidades JPA, por lo que no necesitamos escribir ningún código para implementar esta interfaz.

### Ejemplo 3: uso de un repositorio JPA

Ahora que tenemos nuestra entidad y repositorio JPA, escribamos un programa que use el repositorio para crear, leer, actualizar y eliminar entidades.

Primero, inyectaremos `PersonRepository` en nuestro programa:

```java
@Autowired
private PersonRepository personRepository;
```

A continuación, usaremos el repositorio para crear una entidad `Persona`:

```java
Person person = new Person();
person.setName("John Doe");

personRepository.save(person);
```

Esto insertará una nueva fila en la tabla `persona`. El método `save` generará una identificación única para la entidad y la establecerá en la entidad.

Podemos usar el método `findById` para recuperar una entidad por su id:

```java
Person person = personRepository.findById(1L);
```

Podemos usar el método `findAll` para recuperar todas las entidades:

```java
List<Person> people = personRepository.findAll();
```

Podemos usar el método `deleteById` para eliminar una entidad:

```java
personRepository.deleteById(1L);
```

Y podemos usar el método `delete` para eliminar una entidad:

```java
personRepository.delete(person);
```

Estos son solo algunos de los métodos que están disponibles en la interfaz `JpaRepository`. Para obtener una lista completa de métodos, consulte la [documentación de JpaRepository] (https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/JpaRepository.html) .

## Conclusión

En esta publicación, hemos visto cómo trabajar con Spring Boot y Spring Data JPA. Hemos visto cómo configurar Spring Boot para usar JPA y hemos escrito algunos programas de ejemplo simples para mostrar cómo usar JPA en una aplicación Spring Boot.