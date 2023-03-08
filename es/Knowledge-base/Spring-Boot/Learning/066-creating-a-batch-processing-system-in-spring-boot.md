---
title: 066: Creación de un sistema de procesamiento por lotes en Spring Boot
description: 
published: true
date: 2023-02-05T02:32:14.177Z
tags: 
editor: markdown
dateCreated: 2023-02-05T02:32:12.608Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [066: Creating a Batch Processing System in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/066-creating-a-batch-processing-system-in-spring-boot)
{.links-list}


# 066: Creando un Sistema de Procesamiento por Lotes en Spring Boot

En esta publicación, aprenderemos cómo crear un sistema de procesamiento por lotes en Spring Boot. Cubriremos los siguientes temas:

* ¿Qué es el procesamiento por lotes?
* ¿Por qué usar Spring Boot para el procesamiento por lotes?
* Configuración de un proyecto Spring Boot para el procesamiento por lotes
* Creación de un trabajo por lotes
* Ejecutar un trabajo por lotes

## ¿Qué es el procesamiento por lotes?

El procesamiento por lotes es la ejecución de una serie de trabajos en un orden secuencial predeterminado. Un trabajo por lotes es una unidad de trabajo que normalmente se ejecuta como un solo proceso. Los trabajos por lotes se utilizan normalmente para tareas de larga duración y uso intensivo de recursos que no son adecuadas para la ejecución en tiempo real, como ETL (extracción, transformación y carga) de datos, limpieza de datos o agregación de datos.

## ¿Por qué usar Spring Boot para el procesamiento por lotes?

Spring Boot es un marco popular para crear aplicaciones Java. Está diseñado para simplificar el desarrollo y la implementación de aplicaciones basadas en Spring. Spring Boot es una excelente opción para crear sistemas de procesamiento por lotes porque proporciona una forma sencilla y directa de configurar y ejecutar trabajos por lotes.

## Configuración de un proyecto Spring Boot para el procesamiento por lotes

Para configurar un proyecto Spring Boot para el procesamiento por lotes, debemos agregar las siguientes dependencias a nuestro proyecto:

* spring-boot-starter-batch: este es el módulo de inicio para los trabajos por lotes de Spring Boot.
* mysql-connector-java: este es el controlador MySQL JDBC. Usaremos MySQL como nuestra base de datos.

## Creando un trabajo por lotes

Crearemos un trabajo por lotes simple que lea datos de un archivo CSV y los escriba en una base de datos MySQL. El trabajo tendrá los siguientes pasos:

1. Leer datos de un archivo CSV
2. Transformar los datos
3. Escriba los datos en una base de datos MySQL

## Ejecutar un trabajo por lotes

Para ejecutar nuestro trabajo por lotes, usaremos la interfaz de línea de comandos (CLI) de Spring Boot. La CLI es una herramienta que nos permite ejecutar aplicaciones Spring Boot desde la línea de comandos.

## Conclusión

En esta publicación, hemos aprendido cómo crear un sistema de procesamiento por lotes en Spring Boot. Hemos cubierto los siguientes temas:

* ¿Qué es el procesamiento por lotes?
* ¿Por qué usar Spring Boot para el procesamiento por lotes?
* Configuración de un proyecto Spring Boot para el procesamiento por lotes
* Creación de un trabajo por lotes
* Ejecutar un trabajo por lotes