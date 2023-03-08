---
title: 047: Implementando una carga de archivos en una aplicación Spring Boot
description: 
published: true
date: 2023-02-04T13:32:32.037Z
tags: 
editor: markdown
dateCreated: 2023-02-04T13:32:26.505Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [047: Implementing a file upload in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/047-implementing-a-file-upload-in-a-spring-boot-application)
{.links-list}


# Implementando una carga de archivos en una aplicación Spring Boot

En esta publicación, veremos cómo implementar una carga de archivos en una aplicación Spring Boot.

Comenzaremos observando la anotación @ConfigurationProperties y cómo se puede usar para configurar la carga de archivos en Spring Boot. Luego, crearemos un formulario HTML simple que permita a los usuarios seleccionar un archivo para cargar. Finalmente, implementaremos un controlador que maneje la carga de archivos y guarde el archivo en un directorio en el servidor.

## Configurar la carga de archivos en Spring Boot

Spring Boot proporciona una serie de propiedades que se pueden usar para configurar la carga de archivos en una aplicación Spring Boot. Estas propiedades tienen el prefijo ```spring.servlet.multipart.```.

La propiedad más importante es ```spring.servlet.multipart.enabled```. Esta propiedad debe establecerse en ```true``` para permitir la carga de archivos en Spring Boot.

La siguiente propiedad es ```spring.servlet.multipart.file-size-threshold```. Esta propiedad especifica el umbral de tamaño de los archivos que se almacenarán en la memoria. Los archivos que superen este umbral se escribirán en un archivo temporal en el disco.

La última propiedad que veremos es ```spring.servlet.multipart.location```. Esta propiedad especifica la ubicación en el servidor donde se almacenarán los archivos cargados. Esta ubicación debe ser un directorio en el que pueda escribir el usuario en el que se ejecuta la aplicación.

## Crear un formulario HTML para cargar archivos

Ahora que hemos configurado Spring Boot para cargar archivos, necesitamos crear un formulario HTML que permita a los usuarios seleccionar un archivo para cargar.

El formulario debe tener un campo de entrada ```archivo``` y un botón ```enviar```. El campo de entrada ```archivo``` debe tener el atributo ```múltiple``` establecido en ```verdadero```. Esto permitirá a los usuarios seleccionar varios archivos para cargar.

El atributo ```acción``` del elemento ```form``` debe establecerse en la URL del controlador que manejará la carga del archivo. El atributo ```método``` debe establecerse en ```POST```.

## Implementando el controlador de carga de archivos

Ahora que tenemos un formulario para cargar archivos, necesitamos implementar un controlador que maneje la carga de archivos.

El controlador debe tener una anotación ```@PostMapping``` con el valor ```/upload```. Esto asignará la URL ```/upload``` al método del controlador.

El método del controlador debe tener una anotación ```@RequestParam``` con el valor ```file```. Esto vinculará el campo de entrada ```file``` a un objeto ```MultipartFile```.

El método del controlador también debe tener una anotación ```@ResponseBody```. Esto hará que el método del controlador devuelva el contenido del archivo cargado como respuesta a la solicitud.

Finalmente, el método del controlador debe tener una anotación ```@RequestMapping``` con el valor ```/upload```. Esto asignará la URL ```/upload``` al método del controlador.

## Guardando el archivo subido

Una vez que se ha cargado el archivo, debemos guardarlo en el directorio que configuramos anteriormente. Podemos hacer esto llamando al método ```transferTo()``` en el objeto ```MultipartFile```.

El método ```transferTo()``` toma un objeto ```File``` como argumento. Podemos crear un objeto ```File``` concatenando la ubicación configurada con el nombre de archivo original del archivo cargado.

Una vez que el archivo ha sido transferido, podemos devolver un objeto ```ResponseEntity``` con un código de estado ```201``` para indicar que el archivo se subió correctamente.

## Conclusión

En esta publicación, hemos visto cómo implementar una carga de archivos en una aplicación Spring Boot. Comenzamos observando la anotación @ConfigurationProperties y cómo se puede usar para configurar la carga de archivos en Spring Boot. Luego creamos un formulario HTML simple que permite a los usuarios seleccionar un archivo para cargar. Finalmente, implementamos un controlador que maneja la carga de archivos y guarda el archivo en un directorio en el servidor.