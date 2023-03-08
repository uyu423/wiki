---
title: 009: uso de Spring Boot con bases de datos NoSQL (MongoDB)
description: 
published: true
date: 2023-02-03T08:36:55.375Z
tags: 
editor: markdown
dateCreated: 2023-02-03T08:36:50.439Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [009: Using Spring Boot with NoSQL databases (MongoDB)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/009-using-spring-boot-with-nosql-databases-mongodb)
{.links-list}


# Uso de Spring Boot con bases de datos NoSQL (MongoDB)

En esta publicación, veremos el uso de Spring Boot con MongoDB, una base de datos NoSQL popular.

Cubriremos los siguientes temas:

* ¿Qué es MongoDB?
* ¿Por qué usar MongoDB con Spring Boot?
* Configuración de MongoDB
* Creación de una aplicación Spring Boot con MongoDB
* Conclusión

## ¿Qué es MongoDB?

MongoDB es una poderosa base de datos NoSQL orientada a documentos. Tiene una función de búsqueda basada en índices y un esquema flexible. MongoDB es fácil de escalar y es popular por su alto rendimiento y escalabilidad.

## ¿Por qué usar MongoDB con Spring Boot?

Spring Boot es un marco Java popular para crear aplicaciones web. Está construido sobre el marco Spring y facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

MongoDB es una buena opción para usar con Spring Boot porque es fácil de configurar y usar. MongoDB también es fácil de escalar, lo cual es importante para las aplicaciones que se espera que crezcan.

## Configurando MongoDB

Antes de que podamos usar MongoDB con Spring Boot, debemos configurarlo.

Hay dos formas de configurar MongoDB:

* Use un servicio alojado como MongoDB Atlas
* Instalar MongoDB localmente

Cubriremos ambas opciones a continuación.

### Utilice un servicio alojado como MongoDB Atlas

La forma más sencilla de configurar MongoDB es utilizar un servicio alojado como MongoDB Atlas. MongoDB Atlas es un servicio MongoDB alojado en la nube. Es fácil de configurar y usar.

Para usar MongoDB Atlas, deberá crear una cuenta y configurar un clúster. Un clúster es un grupo de servidores MongoDB que se utilizan para almacenar datos.

Una vez que haya creado una cuenta y configurado un clúster, deberá crear un usuario. La aplicación Spring Boot utilizará al usuario para conectarse a la base de datos MongoDB.

Una vez que haya creado un usuario, deberá obtener la cadena de conexión. La cadena de conexión se utiliza para conectar la aplicación Spring Boot a la base de datos MongoDB.

### Instalar MongoDB localmente

Si desea instalar MongoDB localmente, puede seguir las instrucciones en el sitio web de MongoDB.

Una vez que haya instalado MongoDB, deberá crear una base de datos. La base de datos será utilizada por la aplicación Spring Boot para almacenar datos.

Después de haber creado una base de datos, deberá crear un usuario. La aplicación Spring Boot utilizará al usuario para conectarse a la base de datos MongoDB.

Una vez que haya creado un usuario, deberá obtener la cadena de conexión. La cadena de conexión se utiliza para conectar la aplicación Spring Boot a la base de datos MongoDB.

## Creando una aplicación Spring Boot con MongoDB

Ahora que tenemos configurado MongoDB, podemos crear una aplicación Spring Boot que use MongoDB.

Comenzaremos creando una nueva aplicación Spring Boot. Lo llamaremos "spring-boot-mongodb".

A continuación, agregaremos las siguientes dependencias a nuestro proyecto:

* spring-boot-starter-data-mongodb: esta dependencia se usa para conectarse a una base de datos MongoDB.
* spring-boot-starter-web: Esta dependencia se utiliza para crear una aplicación web.

También necesitaremos agregar la siguiente propiedad a nuestro archivo application.properties:

spring.data.mongodb.uri=mongodb://localhost/spring-boot-mongodb

Esta propiedad se utiliza para configurar la conexión a nuestra base de datos MongoDB.

A continuación, crearemos una clase modelo. Esta clase se utilizará para representar nuestros datos. Lo llamaremos "Usuario".

La clase Usuario tendrá los siguientes campos:

* id: El id del usuario. Este campo será generado por MongoDB.
* nombre: El nombre del usuario.
* email: El email del usuario.

A continuación, crearemos una interfaz de repositorio. Esta interfaz se utilizará para acceder a nuestros datos. Lo llamaremos "UserRepository".

La interfaz de UserRepository ampliará la interfaz de MongoRepository. La interfaz MongoRepository proporciona métodos para operaciones CRUD.

A continuación, crearemos un controlador. Este controlador se utilizará para gestionar las solicitudes web. Lo llamaremos "UserController".

La clase UserController tendrá los siguientes métodos:

* getAllUsers: Este método se utilizará para obtener todos los usuarios.
* createUser: Este método se utilizará para crear un usuario.
* getUser: Este método se usará para obtener un usuario por id.
* updateUser: Este método se utilizará para actualizar un usuario.
* deleteUser: Este método se utilizará para eliminar un usuario.

Finalmente, crearemos una clase de servicio. Esta clase se utilizará para la lógica empresarial. Lo llamaremos "Servicio de usuario".

La clase UserService tendrá los siguientes métodos:

* getAllUsers: Este método se utilizará para obtener todos los usuarios.
* createUser: Este método se utilizará para crear un usuario.
* getUser: Este método se usará para obtener un usuario por id.
* updateUser: Este método se utilizará para actualizar un usuario.
* deleteUser: Este método se utilizará para eliminar un usuario.

## Conclusión

En esta publicación, analizamos el uso de Spring Boot con MongoDB. Hemos cubierto los siguientes temas:

* ¿Qué es MongoDB?
* ¿Por qué usar MongoDB con Spring Boot?
* Configuración de MongoDB
* Creación de una aplicación Spring Boot con MongoDB