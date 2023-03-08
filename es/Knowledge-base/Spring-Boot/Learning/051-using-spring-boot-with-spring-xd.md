---
title: 051: Uso de Spring Boot con Spring XD
description: 
published: true
date: 2023-02-04T17:32:31.201Z
tags: 
editor: markdown
dateCreated: 2023-02-04T17:32:29.567Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [051: Using Spring Boot with Spring XD***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/051-using-spring-boot-with-spring-xd)
{.links-list}


# Uso de Spring Boot con Spring XD

Spring Boot es una excelente manera de comenzar a usar aplicaciones Spring rápidamente. Proporciona muchas funciones listas para usar, incluida la configuración automática, servidores integrados y dependencias de inicio.

Spring XD es una herramienta para construir canalizaciones de datos. Puede ingerir datos de muchas fuentes, procesarlos de varias maneras y enviarlos a muchos receptores.

En esta publicación, aprenderemos cómo usar Spring Boot con Spring XD. Comenzaremos con un ejemplo simple que ingiere datos de un archivo y los envía a una base de datos. Luego exploraremos algunas de las características más avanzadas de Spring XD.

## Requisitos previos

Antes de comenzar, necesitamos instalar algunas cosas:

* [Java 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [Maven 3] (https://maven.apache.org/download.cgi)
* [CLI de Spring Boot](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/# getting-started-installing-the-cli)
* [Primavera XD](https://spring.io/projects/spring-xd)

## Hola Mundo

Comencemos con un ejemplo simple. Crearemos un archivo llamado `data.txt` con los siguientes contenidos:

```
Hello, world!
```

A continuación, crearemos una transmisión Spring XD que ingiere datos de este archivo y los envía a la consola. Esto lo podemos hacer con el siguiente comando:

```
xd:>stream create --name hello --definition "file --dir=./ --pattern=data.txt | log" --deploy
```

Esta secuencia tiene dos componentes: un origen de archivo y un receptor de registro. La fuente del archivo está configurada para leer desde el directorio `./` (el directorio actual) y buscar archivos con el patrón `data.txt`. El receptor de registro simplemente envía los datos a la consola.

Podemos ver la secuencia ejecutándose con el siguiente comando:

```
xd:>stream list
```

Y podemos ver la salida de la transmisión con el siguiente comando:

```
xd:>log hello
```

## Salida de base de datos

En el ejemplo anterior, enviamos los datos a la consola. Pero en muchos casos, querremos enviar los datos a una base de datos. Spring XD lo hace fácil con el sumidero `jdbc`.

Primero, necesitamos crear una base de datos. Usaremos [H2](http://www.h2database.com/html/main.html), que es una base de datos liviana que puede ejecutarse en la memoria. Podemos crear una base de datos con el siguiente comando:

```
xd:>jdbc create --name mydb --url jdbc:h2:mem:mydb
```

Esto creará una base de datos llamada `mydb` en la memoria.

A continuación, necesitamos crear una tabla en esta base de datos. Usaremos el siguiente SQL:

```sql
CREATE TABLE messages (
  id IDENTITY,
  message VARCHAR(255)
);
```

Podemos ejecutar este SQL con el siguiente comando:

```
xd:>jdbc execute --name mydb --sql "CREATE TABLE messages (id IDENTITY, message VARCHAR(255))"
```

Ahora que tenemos una base de datos y una tabla, podemos crear una secuencia que envíe los datos a esta tabla. Esto lo podemos hacer con el siguiente comando:

```
xd:>stream create --name db --definition "file --dir=./ --pattern=data.txt | jdbc --name=mydb --tableName=messages --columns=message" --deploy
```

Esta secuencia es similar a la anterior, pero tiene un sumidero `jdbc` en lugar de un sumidero `log`. El sumidero `jdbc` está configurado para escribir en la tabla `messages` en la base de datos `mydb`. La propiedad `columns` especifica qué columnas de la tabla deben llenarse con datos de la secuencia.

Podemos verificar que los datos han sido insertados en la base de datos con el siguiente SQL:

```sql
SELECT * FROM messages;
```

## Procesador

En los ejemplos anteriores, hemos visto cómo ingerir datos de un archivo y enviarlos a la consola o a una base de datos. Pero en muchos casos, querremos procesar los datos de alguna manera antes de generarlos. Spring XD lo hace fácil con los procesadores.

Los procesadores pueden transformar los datos de la forma que queramos. En este ejemplo, crearemos un procesador que convierte los datos a mayúsculas. Esto lo podemos hacer con el siguiente comando:

```
xd:>processor create --name uppercase --definition "transform --expression=payload.toUpperCase()" --deploy
```

Este procesador tiene un único módulo de "transformación". El módulo `transform` toma una expresión que se evalúa para cada dato en el flujo. En este caso, la expresión es `payload.toUpperCase()`, que convierte los datos a mayúsculas.

Ahora podemos modificar nuestro flujo `db` para usar este procesador:

```
xd:>stream create --name db --definition "file --dir=./ --pattern=data.txt | uppercase | jdbc --name=mydb --tableName=messages --columns=message" --deploy
```

Podemos verificar que los datos han sido insertados en la base de datos con el siguiente SQL:

```sql
SELECT * FROM messages;
```

## Resumen

En esta publicación, hemos aprendido a usar Spring Boot con Spring XD. Hemos visto cómo crear una secuencia que ingiere datos de un archivo y los envía a la consola o a una base de datos. Y hemos visto cómo usar un procesador para transformar los datos antes de que se envíen.