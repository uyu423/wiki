---
title: 054: Uso de Spring Boot con Apache Nifi
description: 
published: true
date: 2023-02-03T01:23:39.010Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:23:37.387Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [054: Using Spring Boot with Apache Nifi***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/054-using-spring-boot-with-apache-nifi)
{.links-list}


# Uso de Spring Boot con Apache Nifi

Spring Boot es un marco popular basado en Java que se utiliza para crear microservicios. Apache NiFi es una poderosa herramienta de flujo de datos que se puede usar para procesar y enrutar datos.

En esta publicación, mostraremos cómo usar Spring Boot con Apache NiFi. Cubriremos los siguientes temas:

* Configuración de un proyecto Spring Boot
* Configuración de Apache NiFi
* Creación de un servicio Spring Boot
* Probar el flujo de datos

## Configuración de un proyecto Spring Boot

Lo primero que debemos hacer es crear un nuevo proyecto Spring Boot. Podemos usar [Spring Initializr](https://start.spring.io/) para generar un proyecto con las dependencias necesarias.

Para este ejemplo, necesitaremos las siguientes dependencias:

* Web - para crear una aplicación web
* H2 - para la base de datos en memoria

Una vez que tenemos el proyecto configurado, podemos comenzar a configurar Apache NiFi.

## Configuración de Apache NiFi

Apache NiFi debe configurarse para usar el servicio Spring Boot que crearemos. Tendremos que agregar lo siguiente a la configuración de NiFi:

* Un procesador para invocar el servicio Spring Boot
* Un grupo de conexiones para el procesador
* Un servicio de controlador para el grupo de conexiones

Podemos usar la GUI de NiFi para configurar estos ajustes. Primero, agregaremos el Procesador:

![Agregar procesador](https://i.imgur.com/Lb6qyFW.png)

A continuación, agregaremos el grupo de conexiones:

![Agregar grupo de conexiones](https://i.imgur.com/vH8X3zJ.png)

Finalmente, agregaremos el Servicio de controlador:

![Agregar servicio de controlador](https://i.imgur.com/g4SVfyi.png)

## Creando un servicio Spring Boot

Ahora que tenemos configurado Apache NiFi, podemos crear el servicio Spring Boot. El servicio será una aplicación web simple que expone un punto final REST.

El punto final tomará una carga JSON y devolverá una respuesta. La respuesta será la misma carga útil JSON con un ID generado.

Aquí está el código para el servicio:

```java
@RestController
public class DataController {

    @PostMapping("/data")
    public ResponseEntity<String> data(@RequestBody String data) {
        // Generate ID
        String id = UUID.randomUUID().toString();
        // Return response
        return ResponseEntity.ok().body(id);
    }
}
```

## Probando el flujo de datos

Ahora que tenemos el servicio en funcionamiento, podemos probar el flujo de datos. Usaremos la GUI de NiFi para enviar una carga JSON al punto final.

Primero, crearemos un nuevo FlowFile:

![Crear archivo de flujo](https://i.imgur.com/TGiukC5.png)

A continuación, agregaremos la carga útil de JSON:

![Agregar carga útil JSON](https://i.imgur.com/l0v4tqO.png)

Finalmente, activaremos el Procesador y verificaremos la respuesta:

![Procesador de activación](https://i.imgur.com/JY4fZUO.png)

![Comprobar respuesta](https://i.imgur.com/5AFw8gG.png)

Como podemos ver, la respuesta contiene el ID generado.

## Conclusión

En esta publicación, mostramos cómo usar Spring Boot con Apache NiFi. Hemos configurado un flujo de datos simple que invoca un servicio Spring Boot y devuelve una respuesta.

Si está interesado en obtener más información sobre NiFi, asegúrese de consultar la [documentación oficial] (https://nifi.apache.org/docs.html).