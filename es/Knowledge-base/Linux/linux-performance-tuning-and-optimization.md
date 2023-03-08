---
title: Ajuste y optimización del rendimiento de Linux
description: 
published: true
date: 2023-02-12T01:32:48.905Z
tags: 
editor: markdown
dateCreated: 2023-02-12T01:32:47.266Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Performance Tuning and Optimization***English** document is available*](/en/Knowledge-base/Linux/linux-performance-tuning-and-optimization)
{.links-list}


# Ajuste y optimización del rendimiento de Linux

Una guía del administrador del sistema para mejorar el rendimiento de Linux.

Linux es un sistema operativo versátil y potente que se puede modificar para satisfacer las necesidades específicas de una carga de trabajo determinada. Al optimizar el rendimiento del sistema operativo, un administrador del sistema puede exprimir hasta la última gota de rendimiento de un servidor Linux.

En esta guía, cubriremos algunas de las técnicas de optimización de rendimiento más comunes para Linux. Comenzaremos con una breve descripción general del kernel de Linux y su arquitectura, luego pasaremos a los parámetros del kernel relacionados con el rendimiento. Después de eso, analizaremos algunas estrategias comunes de optimización del rendimiento, incluidas las de CPU, memoria, E/S y redes.

## Descripción general del núcleo de Linux

El kernel de Linux es el corazón del sistema operativo Linux. Es responsable de administrar todos los recursos del sistema, incluida la CPU, la memoria, las E/S y las redes.

El núcleo es una pieza de software compleja y puede ser difícil entender cómo funciona. Sin embargo, es necesaria una comprensión básica de la arquitectura del kernel para ajustar el rendimiento.

El kernel de Linux se divide en varias capas diferentes. La capa más baja es el hardware, que consta de la CPU, la memoria, los dispositivos de E/S, etc. Por encima de eso está el propio kernel, que se encarga de gestionar todos los recursos del sistema.

El núcleo se divide en varios subsistemas diferentes, cada uno de los cuales es responsable de administrar un tipo específico de recurso. Por ejemplo, el subsistema de administración de memoria es responsable de administrar la memoria, el subsistema de redes es responsable de administrar las redes, etc.

 Cada subsistema tiene su propio conjunto de parámetros del núcleo que se pueden ajustar para mejorar el rendimiento. En la siguiente sección, discutiremos algunos de los parámetros del núcleo más importantes para el ajuste del rendimiento.

## Parámetros del núcleo

Hay muchos parámetros del núcleo que se pueden ajustar para mejorar el rendimiento. En esta sección, discutiremos algunos de los más importantes.

### intercambio

El parámetro swappiness controla la agresividad con la que el kernel intercambia páginas de memoria. Un valor más alto significa que el kernel será más agresivo con el intercambio de páginas de memoria, lo que puede mejorar el rendimiento en algunas cargas de trabajo. Sin embargo, también puede causar problemas de rendimiento en otras cargas de trabajo.

El valor predeterminado es 60, que es un buen punto de partida. Sin embargo, vale la pena experimentar con diferentes valores para ver qué funciona mejor para su carga de trabajo.

### página_enorme_transparente

El parámetro transparent_hugepage controla si el kernel usa o no páginas grandes transparentes. Las páginas grandes transparentes pueden mejorar el rendimiento en algunas cargas de trabajo, pero también pueden causar problemas de rendimiento en otras cargas de trabajo.

El valor predeterminado es siempre, lo que significa que el kernel usará páginas grandes transparentes si están disponibles. Sin embargo, vale la pena experimentar con diferentes valores para ver qué funciona mejor para su carga de trabajo.

### vm.proporción_sucia

El parámetro vm.dirty_ratio controla el porcentaje máximo de memoria que puede estar sucia antes de que el núcleo comience a escribirla en el disco. Un valor más alto significa que puede haber más memoria sucia antes de que el kernel comience a escribirla en el disco, lo que puede mejorar el rendimiento en algunas cargas de trabajo. Sin embargo, también puede causar problemas de rendimiento en otras cargas de trabajo.

El valor predeterminado es 20, que es un buen punto de partida. Sin embargo, vale la pena experimentar con diferentes valores para ver qué funciona mejor para su carga de trabajo.

### vm.dirty_background_ratio

El parámetro vm.dirty_background_ratio controla el porcentaje máximo de memoria que puede estar sucia antes de que el núcleo comience a escribirla en el disco en segundo plano. Un valor más alto significa que más memoria puede estar sucia antes de que el kernel comience a escribirla en el disco en segundo plano, lo que puede mejorar el rendimiento en algunas cargas de trabajo. Sin embargo, también puede causar problemas de rendimiento en otras cargas de trabajo.

El valor predeterminado es 10, que es un buen punto de partida. Sin embargo, vale la pena experimentar con diferentes valores para ver qué funciona mejor para su carga de trabajo.

### vm.dirty_expire_centisecs

El parámetro vm.dirty_expire_centisecs controla la cantidad de tiempo (en centésimas de segundo) que una página puede estar sucia antes de que el kernel comience a escribirla en el disco. Un valor más alto significa que una página puede estar sucia durante más tiempo antes de que el kernel comience a escribirla en el disco, lo que puede mejorar el rendimiento en algunas cargas de trabajo. Sin embargo, también puede causar problemas de rendimiento en otras cargas de trabajo.

El valor predeterminado es 300, que es un buen punto de partida. Sin embargo, vale la pena experimentar con diferentes valores para ver qué funciona mejor para su carga de trabajo.

### vm.dirty_writeback_centisecs

El parámetro vm.dirty_writeback_centisecs controla la cantidad de tiempo (en centésimas de segundo) entre reescrituras de páginas sucias en el disco. Un valor más alto significa que habrá más tiempo entre reescrituras de páginas sucias en el disco, lo que puede mejorar el rendimiento en algunas cargas de trabajo. Sin embargo, también puede causar problemas de rendimiento en otras cargas de trabajo.

El valor predeterminado es 500, que es un buen punto de partida. Sin embargo, vale la pena experimentar con diferentes valores para ver qué funciona mejor para su carga de trabajo.

## Estrategias de optimización del rendimiento

### UPC

Hay muchas técnicas diferentes que se pueden utilizar para optimizar el rendimiento de la CPU.

Una técnica común es usar una herramienta de creación de perfiles de CPU para identificar puntos calientes en el código. Un punto caliente es una sección de código que se ejecuta con más frecuencia que otras secciones de código. Al identificar y optimizar los puntos calientes, se puede lograr una mejora significativa del rendimiento.

Otra técnica común es usar un programador de tareas para distribuir la carga de trabajo de manera uniforme entre todas las CPU disponibles. Esto puede mejorar el rendimiento al reducir la contención por los recursos.

### Memoria

Hay muchas técnicas diferentes que se pueden utilizar para optimizar el rendimiento de la memoria.

Una técnica común es usar un generador de perfiles de memoria para identificar áreas de memoria que se usan en exceso. Al identificar y optimizar estas áreas, se puede lograr una mejora significativa del rendimiento.

Otra técnica común es utilizar un asignador de memoria diseñado específicamente para el rendimiento. El asignador glibc malloc es una buena opción para la mayoría de las cargas de trabajo.

### E/S

Hay muchas técnicas diferentes que se pueden utilizar para optimizar el rendimiento de E/S.

Una técnica común es usar un programador de E/S para programar operaciones de E/S de una manera que maximice el rendimiento. El programador de E/S de fecha límite es una buena opción para la mayoría de las cargas de trabajo.

Otra técnica común es usar un mecanismo de lectura anticipada para obtener datos en la memoria antes de que se necesiten. Esto puede mejorar el rendimiento al reducir la latencia.

### Redes

Hay muchas técnicas diferentes que se pueden utilizar para optimizar el rendimiento de la red.

Una técnica común es usar un programador de red para programar el tráfico de red de una manera que maximice el rendimiento. El programador de red pfifo_fast es una buena opción para la mayoría de las cargas de trabajo.

Otra técnica común es usar un acelerador de red para descargar el trabajo de la CPU a un dispositivo de hardware dedicado. Esto puede mejorar el rendimiento al reducir la utilización de la CPU.

## Conclusión

En esta guía, hemos cubierto algunas de las técnicas de optimización de rendimiento más comunes para Linux. Al ajustar el rendimiento del sistema operativo, un administrador del sistema puede exprimir hasta la última gota de rendimiento de un servidor Linux.

## Recursos externos

https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/performance_tuning_guide/index
https://www.kernel.org/doc/Documentation/sysctl/vm.txt
https://www.kernel.org/doc/Documentation/filesystems/proc.txt
https://www.kernel.org/doc/Documentation/block/deadline-iosched.txt
https://www.kernel.org/doc/Documentation/block/cfq-iosched.txt