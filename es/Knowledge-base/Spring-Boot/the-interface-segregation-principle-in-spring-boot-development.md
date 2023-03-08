---
title: El principio de segregación de la interfaz en el desarrollo de Spring Boot
description: 
published: true
date: 2023-02-04T02:17:22.380Z
tags: 
editor: markdown
dateCreated: 2023-02-04T02:17:20.763Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [The Interface Segregation Principle in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-interface-segregation-principle-in-spring-boot-development)
{.links-list}


# El principio de segregación de la interfaz en el desarrollo de Spring Boot

El Principio de segregación de la interfaz (ISP) es un principio de diseño de software que establece que ningún cliente debe verse obligado a depender de métodos que no utiliza.

En otras palabras, es mejor mantener las interfaces pequeñas y enfocadas para que puedan ser implementadas por las clases que las necesitan, sin depender de métodos no utilizados.

El principio fue definido por primera vez por Robert C. Martin en su libro "Desarrollo de software ágil, principios, patrones y prácticas".

## Aplicación del principio de segregación de interfaces

Al diseñar software, es importante tener en cuenta el ISP para que las interfaces no sean demasiado grandes o demasiado generales.

Por ejemplo, considere una interfaz para un servicio de usuario que incluya métodos para crear, actualizar y eliminar usuarios.

```java
public interface UserService {
    
    public void createUser(User user);
    
    public void updateUser(User user);
    
    public void deleteUser(User user);
    
}
```

Una clase que implemente esta interfaz necesitaría proporcionar implementaciones para los tres métodos, incluso si solo necesita admitir la creación de usuarios.

Un mejor diseño sería tener interfaces separadas para cada tipo de operación.

```java
public interface UserService {
    
    public void createUser(User user);
    
}

public interface UserUpdateService {
    
    public void updateUser(User user);
    
}

public interface UserDeleteService {
    
    public void deleteUser(User user);
    
}
```

Este diseño está más en línea con el ISP porque cada interfaz está enfocada a una tarea específica.

Una clase que solo necesita admitir la creación de usuarios puede implementar la interfaz ```UserService``` sin depender de las otras interfaces.

## Spring Boot y el principio de segregación de la interfaz

Spring Boot es un marco popular para desarrollar aplicaciones Java.

Se basa en el principio de la convención sobre la configuración, lo que significa que favorece la convención sobre la configuración explícita.

Este principio se puede aplicar al diseño de interfaces.

Por ejemplo, considere una aplicación Spring Boot que tiene una interfaz ```UserService```.

```java
@Service
public interface UserService {
    
    public void createUser(User user);
    
}
```

La anotación ```@Service``` se usa para indicar que esta interfaz es un servicio Spring.

Spring creará automáticamente un bean para esta interfaz y lo inyectará en cualquier componente que lo necesite.

Este diseño está en línea con el ISP porque la interfaz está enfocada a una tarea específica (creación de usuarios) y no es necesario que los componentes dependan de métodos no utilizados.