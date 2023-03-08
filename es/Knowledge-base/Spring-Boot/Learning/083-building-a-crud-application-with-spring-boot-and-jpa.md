---
title: 083: Creación de una aplicación CRUD con Spring Boot y JPA
description: 
published: true
date: 2023-02-05T13:32:25.263Z
tags: 
editor: markdown
dateCreated: 2023-02-05T13:32:22.883Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [083: Building a CRUD Application with Spring Boot and JPA***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/083-building-a-crud-application-with-spring-boot-and-jpa)
{.links-list}


083: Creación de una aplicación CRUD con Spring Boot y JPA
================================================== ======

En este artículo, aprenderemos cómo crear una aplicación CRUD con Spring Boot y JPA.

Primero crearemos una clase de representación de recursos. Esta clase se utilizará para representar nuestros datos en la aplicación.

A continuación, crearemos una interfaz de repositorio. Esta interfaz se utilizará para acceder a nuestros datos.

Finalmente, crearemos un controlador. Este controlador se usará para manejar solicitudes y respuestas HTTP.

Creación de la clase de representación de recursos
---------------------------------------------------------

El primer paso es crear una clase de representación de recursos. Esta clase se utilizará para representar nuestros datos en la aplicación.

Comenzaremos creando una clase llamada `Usuario`. Esta clase tendrá tres campos: `id`, `name` y `email`.


    Usuario de clase pública {
    
        identificación larga privada;
        cadena privada nombre;
        correo electrónico privado de cadena;
    
        // Getters y setters
    
    }


Creación de la interfaz del repositorio
---------------------------------

A continuación, crearemos una interfaz de repositorio. Esta interfaz se utilizará para acceder a nuestros datos.

Comenzaremos creando una interfaz llamada `UserRepository`. Esta interfaz extenderá `JpaRepository`. `JpaRepository` es una interfaz Spring Data JPA que nos proporciona operaciones CRUD.


    interfaz pública UserRepository extiende JpaRepository<User, Long> {
    
    }


Crear el controlador
-----------------------

Finalmente, crearemos un controlador. Este controlador se usará para manejar solicitudes y respuestas HTTP.

Comenzaremos creando una clase llamada `UserController`. Esta clase tendrá dos métodos: `getAllUsers` y `createUser`.

El método `getAllUsers` se usará para manejar una solicitud GET a `/users`. Este método devolverá una lista de todos los usuarios en la base de datos.

El método `createUser` se usará para manejar una solicitud POST a `/users`. Este método creará un nuevo usuario en la base de datos.


    @RestController
    clase pública UserController {
    
        @autocableado
        UserRepository privado UserRepository;
    
        @GetMapping("/usuarios")
        public List<Usuario> getAllUsers() {
            volver userRepository.findAll();
        }
    
        @PostMapping("/usuarios")
        public User createUser(@RequestBody Usuario usuario) {
            volver userRepository.save(usuario);
        }
    
    }


Prueba de la aplicación
-----------------------

Ahora que hemos creado nuestra clase de representación de recursos, la interfaz del repositorio y el controlador, estamos listos para probar nuestra aplicación.

Comenzaremos creando un objeto `Usuario`.


    Usuario usuario = nuevo Usuario();
    usuario.setName("Juan Pérez");
    usuario.setEmail("john.doe@example.com");


A continuación, llamaremos al método `createUser`.


    usuario = controlador de usuario.createUser (usuario);


Finalmente, llamaremos al método `getAllUsers`.


    List<Usuario> usuarios = userController.getAllUsers();
    afirmar que (usuarios). contiene (usuario);


Si todo salió bien, debería ver el siguiente resultado:


    [
        {
            "identificación": 1,
            "nombre": "Juan Pérez",
            "correo electrónico": "john.doe@example.com"
        }
    ]


Puede encontrar el código fuente completo para este ejemplo en GitHub.