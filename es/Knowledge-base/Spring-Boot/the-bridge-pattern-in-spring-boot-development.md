---
title: El patrón de puente en el desarrollo de Spring Boot
description: 
published: true
date: 2023-02-06T09:17:15.836Z
tags: 
editor: markdown
dateCreated: 2023-02-06T09:17:14.247Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [The Bridge Pattern in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-bridge-pattern-in-spring-boot-development)
{.links-list}


# El patrón de puente en el desarrollo de Spring Boot

Uno de los patrones de diseño más útiles es el patrón de puente. Este patrón es útil para desacoplar una abstracción de su implementación para que las dos puedan variar de forma independiente. El patrón de puente se usa a menudo junto con el patrón de adaptador.

En Spring Boot, el patrón de puente se usa para desacoplar la aplicación de la base de datos subyacente. Esto se hace usando las anotaciones Repository y @Transactional.

La anotación Repository se utiliza para marcar una clase como repositorio. Un repositorio es una clase que proporciona operaciones CRUD para una entidad. La anotación @Transactional se usa para marcar un método como parte de una transacción.


Aquí hay un ejemplo de un repositorio:

```java
@Repository
public class PersonRepository {
 
    @Transactional
    public void save(Person person) {
        // save person
    }
 
    @Transactional
    public Person findById(Long id) {
        // find person by id
    }
 
    @Transactional
    public void delete(Person person) {
        // delete person
    }
}
```

En el ejemplo anterior, la clase PersonRepository está marcada como repositorio. Los métodos save, findById y delete se marcan como parte de una transacción.

El patrón de puente es un patrón útil para desacoplar una abstracción de su implementación. En Spring Boot, las anotaciones Repository y @Transactional se utilizan para desacoplar la aplicación de la base de datos subyacente.