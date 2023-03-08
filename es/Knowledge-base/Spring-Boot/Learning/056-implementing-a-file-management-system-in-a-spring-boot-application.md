---
title: 056: Implementación de un sistema de gestión de archivos en una aplicación Spring Boot
description: 
published: true
date: 2023-02-03T20:17:31.262Z
tags: 
editor: markdown
dateCreated: 2023-02-03T20:17:29.561Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [056: Implementing a file management system in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/056-implementing-a-file-management-system-in-a-spring-boot-application)
{.links-list}


# Implementando un sistema de gestión de archivos en una aplicación Spring Boot

Spring Boot es un marco basado en Java que le permite crear aplicaciones Spring independientes de nivel de producción. En esta publicación, le mostraremos cómo implementar un sistema de administración de archivos en una aplicación Spring Boot.

## Requisitos previos

- Algo de experiencia con el desarrollo de Java
- Algo de experiencia con el framework Spring

## Empezando

Primero, necesitaremos crear un nuevo proyecto Spring Boot. Podemos hacer esto usando [Spring Initializr](https://start.spring.io/).

![Inicializar resorte](https://i.imgur.com/hmvkF9r.png)

Complete los detalles del proyecto:

- Grupo: com.ejemplo
- Artefacto: sistema de gestión de archivos
- Nombre: Sistema de gestión de archivos
- Descripción: Un sistema de gestión de archivos implementado en Spring Boot
- Nombre del paquete: com.example.filemanagementsystem
- Tipo: Proyecto Maven
- Envase: Tarro
- Versión Java: 8
- Seleccione las siguientes dependencias:
  - Internet
  - Hoja de tomillo
  - Lombok

Haga clic en "Generar proyecto" para descargar el proyecto.

## Estructura del proyecto

Una vez generado el proyecto, deberíamos tener la siguiente estructura de proyecto:

```
.
├── pom.xml
└── src
    └── main
        ├── java
        │   └── com
        │       └── example
        │           └── filemanagementsystem
        │               ├── FileManagementSystemApplication.java
        │               ├── controller
        │               │   └── FileController.java
        │               └── model
        │                   └── File.java
        └── resources
            ├── application.properties
            └── templates
                └── index.html
```

## Implementando el sistema de gestión de archivos

Ahora que tenemos un proyecto básico configurado, podemos comenzar a implementar nuestro sistema de administración de archivos.

### Creando el modelo

Nuestro sistema de gestión de archivos necesitará almacenar información sobre los archivos que se están gestionando. Podemos hacer esto creando un modelo `File`:

```java
@Data
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class File {

    private String name;
    private String type;
    private long size;
}
```

La anotación `@Data` de la biblioteca [Lombok](https://projectlombok.org/) generará getters, setters y un método toString para nosotros. La anotación `@Builder` nos permitirá crear objetos `File` utilizando un patrón de construcción. Las anotaciones `@NoArgsConstructor` y `@AllArgsConstructor` generarán un constructor sin argumentos y un constructor que toma todos los campos como argumentos, respectivamente.

### Creando el controlador

A continuación, necesitaremos crear un controlador para manejar las solicitudes a nuestro sistema de gestión de archivos. Podemos hacer esto creando un `FileController`:

```java
@Slf4j
@Controller
@RequestMapping("/files")
public class FileController {

    @GetMapping
    public String listFiles(Model model) {
        // TODO: Implement this method
        return "index";
    }

    @PostMapping
    public String uploadFile(@RequestParam("file") MultipartFile file) {
        // TODO: Implement this method
        return "redirect:/files";
    }

    @GetMapping("/{id}")
    public ResponseEntity<Resource> downloadFile(@PathVariable String id) {
        // TODO: Implement this method
        return null;
    }
}
```

La anotación `@Slf4j` de la biblioteca de Lombok generará un registrador para nosotros. La anotación `@Controller` marcará esta clase como un controlador. La anotación `@RequestMapping` asignará todos los métodos del controlador a la ruta `/files`.

El método `listFiles` manejará las solicitudes GET a la ruta `/files`. Tomará un objeto 'Modelo' como parámetro y devolverá una Cadena que indica qué plantilla se debe representar.

El método `uploadFile` manejará las solicitudes POST a la ruta `/files`. Tomará un objeto `MultipartFile` como parámetro y devolverá una cadena que indica qué plantilla se debe representar.

El método `downloadFile` manejará las solicitudes GET a la ruta `/files/{id}`. Tomará una identificación de cadena como parámetro y devolverá un objeto `ResponseEntity` que contiene el archivo que se solicitó.

### Creando las plantillas

Tendremos que crear dos plantillas para nuestro sistema de administración de archivos: una para listar archivos y otra para cargar archivos. Podemos hacer esto creando un archivo `index.html` en el directorio `src/main/resources/templates`:

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>File Management System</title>
</head>
<body>
    <h1>File Management System</h1>

    <table>
        <thead>
            <tr>
                <th>Name</th>
                <th>Type</th>
                <th>Size</th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            <tr th:each="file : ${files}">
                <td th:text="${file.name}"></td>
                <td th:text="${file.type}"></td>
                <td th:text="${file.size}"></td>
                <td><a href="/files/[[${file.id}]]">Download</a></td>
            </tr>
        </tbody>
    </table>

    <form method="post" enctype="multipart/form-data">
        <div>
            <label>File:</label>
            <input type="file" name="file"/>
        </div>
        <div>
            <button type="submit">Upload</button>
        </div>
    </form>
</body>
</html>
```

Esta plantilla enumerará todos los archivos que se han cargado y proporcionará un formulario para cargar archivos nuevos.

### Configuración de Spring Boot

Tendremos que configurar algunas cosas en nuestro archivo `application.properties`:

```properties
spring.thymeleaf.mode=HTML5
spring.thymeleaf.encoding=UTF-8
spring.thymeleaf.content-type=text/html
server.port=8080
```

Las propiedades `spring.thymeleaf.mode`, `spring.thymeleaf.encoding` y `spring.thymeleaf.content-type` configurarán Thymeleaf para usar HTML5, codificación UTF-8 y tipo de contenido de texto/html, respectivamente. La propiedad `server.port` configurará el servidor para que se ejecute en el puerto 8080.

## Ejecutando la aplicación

Ahora podemos ejecutar nuestra aplicación y probarla.

Primero, necesitaremos construir nuestro proyecto. Esto lo podemos hacer ejecutando el siguiente comando:

```
$ ./mvnw clean package
```

A continuación, podemos ejecutar nuestra aplicación usando el siguiente comando:

```
$ java -jar target/file-management-system-0.0.1-SNAPSHOT.jar
```

Ahora podemos acceder a nuestro sistema de gestión de archivos en http://localhost:8080.

## Conclusión

En esta publicación, le mostramos cómo implementar un sistema de administración de archivos en una aplicación Spring Boot.