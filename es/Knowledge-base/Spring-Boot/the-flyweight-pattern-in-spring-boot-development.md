---
title: El patrón Flyweight en el desarrollo de Spring Boot
description: 
published: true
date: 2023-02-03T21:17:36.181Z
tags: 
editor: markdown
dateCreated: 2023-02-03T21:17:34.499Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [The Flyweight Pattern in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-flyweight-pattern-in-spring-boot-development)
{.links-list}


# El patrón Flyweight en el desarrollo de Spring Boot

El patrón Flyweight es una herramienta útil para optimizar el código cuando se trabaja con una gran cantidad de objetos. La idea clave es reutilizar objetos existentes en lugar de crear otros nuevos, lo que puede ahorrar tiempo y memoria.

En el desarrollo de Spring Boot, el patrón Flyweight se puede usar para mejorar el rendimiento almacenando en caché objetos comunes y reutilizándolos en las solicitudes. Por ejemplo, si tiene un servicio que devuelve una lista de usuarios, puede almacenar la lista en caché y reutilizarla en lugar de obtenerla de la base de datos cada vez.

Para implementar el patrón Flyweight en Spring Boot, puede usar la abstracción Spring Cache. Esto le permite especificar de forma declarativa qué objetos deben almacenarse en caché y cómo deben invalidarse.

En este artículo, veremos cómo usar el patrón Flyweight en el desarrollo de Spring Boot. Comenzaremos observando el problema que el patrón puede resolver. Luego veremos cómo implementar el patrón utilizando la abstracción Spring Cache. Finalmente, veremos algunos temas más avanzados relacionados con el patrón Flyweight.

## El problema

Considere una aplicación Spring Boot simple que expone una API REST para administrar usuarios. La API tiene un punto final GET que devuelve una lista de usuarios. El punto final se ve así:

```
@GetMapping("/users")
public List<User> getUsers() {
    return userService.getUsers();
}
```

El método ```getUsers()``` devuelve una lista de usuarios de un ```UserService```. ```UserService``` es un servicio simple que obtiene usuarios de una base de datos:

```
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public List<User> getUsers() {
        return userRepository.findAll();
    }

}
```

El ```UserService``` usa un ```UserRepository``` para obtener usuarios de una base de datos. El ```UserRepository``` es un repositorio CRUD simple:

```
@Repository
public interface UserRepository extends CrudRepository<User, Long> {

}
```

Ahora, imagina que tenemos una gran cantidad de usuarios en nuestra base de datos. Cuando hacemos una solicitud al punto final ```/users```, lleva mucho tiempo obtener todos los usuarios de la base de datos. Esto puede hacer que nuestra aplicación se vuelva lenta y no responda.

Una forma de resolver este problema es almacenar en caché la lista de usuarios. De esa manera, cuando hacemos una solicitud al punto final ```/users```, podemos simplemente devolver la lista de usuarios almacenada en caché en lugar de obtenerla de la base de datos cada vez.

## Implementando el patrón Flyweight

Podemos implementar el patrón Flyweight en nuestra aplicación de ejemplo usando la abstracción Spring Cache. Primero, necesitamos agregar la dependencia ```spring-boot-starter-cache``` a nuestro ```pom.xml```:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
```

A continuación, debemos configurar ```UserService``` para usar el almacenamiento en caché. Podemos hacer esto anotando el método ```getUsers()``` con la anotación ```@Cacheable```:

```
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    @Cacheable(value = "users")
    public List<User> getUsers() {
        return userRepository.findAll();
    }

}
```

La anotación ```@Cacheable``` le dice a Spring que almacene en caché los resultados del método ```getUsers()```. El atributo ```value``` especifica el nombre del caché. En este caso, hemos llamado al caché ```users```.

Ahora, cuando hacemos una solicitud al extremo ```/users```, el método ```getUsers()``` devolverá la lista de usuarios en caché. La primera vez que se invoca el método, obtendrá los usuarios de la base de datos y los almacenará en caché. Las invocaciones posteriores simplemente devolverán la lista de usuarios en caché.

También podemos configurar la anotación ```@Cacheable``` para controlar cómo se invalidan los resultados almacenados en caché. Por ejemplo, podemos usar el atributo ```key``` para especificar la clave del objeto en caché:

```
@Cacheable(value = "users", key = "#id")
public User getUserById(Long id) {
    return userRepository.findById(id).orElse(null);
}
```

En este ejemplo, hemos especificado que los resultados almacenados en caché deben ser ingresados por el parámetro ```id```. Esto significa que los resultados almacenados en caché se invalidarán cada vez que cambie el ```id```.

También podemos usar la anotación ```@CacheEvict``` para desalojar explícitamente un objeto del caché:

```
@CacheEvict(value = "users", key = "#id")
public void deleteUserById(Long id) {
    userRepository.deleteById(id);
}
```

En este ejemplo, hemos anotado el método ```deleteUserById()``` con la anotación ```@CacheEvict```. Esto le dice a Spring que desaloje los resultados almacenados en caché del método ```getUserById()``` cuando se invoca el método ```deleteUserById()```.

## Temas avanzados

Hay algunos temas avanzados relacionados con el patrón Flyweight que vale la pena mencionar.

### Caducidad

De forma predeterminada, la abstracción de Spring Cache caducará los objetos almacenados en caché después de que haya transcurrido una cierta cantidad de tiempo. El tiempo de caducidad predeterminado es de dos horas.

Podemos controlar el tiempo de caducidad de los objetos almacenados en caché usando el atributo ```@Cacheable``` de la anotación ```expire```:

```
@Cacheable(value = "users", expire = 60)
public List<User> getUsers() {
    return userRepository.findAll();
}
```

En este ejemplo, especificamos que los resultados almacenados en caché deben caducar después de 60 segundos.

También podemos usar la anotación ```@CacheEvict``` para caducar explícitamente un objeto:

```
@CacheEvict(value = "users", allEntries = true)
public void deleteUserById(Long id) {
    userRepository.deleteById(id);
}
```

En este ejemplo, hemos anotado el método ```deleteUserById()``` con la anotación ```@CacheEvict```. El atributo ```allEntries``` le dice a Spring que caduque todos los objetos en el caché ```users```.

### Serialización

La abstracción Spring Cache se puede utilizar para almacenar en caché cualquier tipo de objeto. Sin embargo, es importante tener en cuenta el hecho de que CacheManager serializará y deserializará los objetos almacenados en caché.

Esto puede causar problemas si los objetos almacenados en caché no son serializables. Por ejemplo, considere la siguiente clase ```Usuario```:

```
public class User {

    private Long id;

    private String name;

    private Date birthDate;

    // Getters and setters...

}
```

La clase ```Usuario``` no es serializable porque contiene un campo ```Fecha```. Esto significa que no podemos almacenar en caché los objetos ```User```.

Una forma de evitar este problema es hacer serializable la clase ```Usuario```:

```
public class User implements Serializable {

    private static final long serialVersionUID = 1L;

    private Long id;

    private String name;

    private Date birthDate;

    // Getters and setters...

}
```

En este ejemplo, hemos hecho serializable la clase ```User``` agregando un campo ```serialVersionUID```. Este campo es requerido por la interfaz ```Serializable```.

Otra forma de solucionar este problema es usar una clase contenedora ```Serializable```:

```
public class SerializableUser implements Serializable {

    private static final long serialVersionUID = 1L;

    private User user;

    // Getters and setters...

}
```

En este ejemplo, hemos creado una clase ```SerializableUser``` que envuelve un objeto ```Usuario```. Esto nos permite almacenar en caché el objeto ```SerializableUser``` sin tener que hacer serializable la clase ```User```.

## Conclusión

En este artículo, hemos visto cómo usar el patrón Flyweight en el desarrollo de Spring Boot. Comenzamos observando el problema que el patrón puede resolver. Luego, analizamos cómo implementar el patrón utilizando la abstracción Spring Cache. Finalmente, hemos analizado algunos temas más avanzados relacionados con el patrón Flyweight.