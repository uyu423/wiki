---
title: Gestión de memoria de Linux
description: 
published: true
date: 2023-02-10T04:55:19.175Z
tags: 
editor: markdown
dateCreated: 2023-02-10T04:55:17.611Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Memory Management***English** document is available*](/en/Knowledge-base/Linux/linux-memory-management)
{.links-list}


# Gestión de memoria de Linux

Los desarrolladores que trabajan en un entorno Linux deben saber cómo el kernel administra la memoria y la programación de procesos. Esta guía brinda una descripción general de la administración de memoria en Linux, con un enfoque en cómo se relaciona con el desarrollo de TI.

## Gestión de memoria en Linux

El kernel de Linux es responsable de administrar la memoria y la programación de procesos. Utiliza una variedad de técnicas para optimizar el uso y el rendimiento de la memoria.

Uno de los aspectos más importantes de la gestión de la memoria es la memoria caché de la página. La memoria caché de la página es un conjunto de memoria libre que se utiliza para almacenar datos en la memoria caché del disco. Cuando un proceso necesita leer datos del disco, el kernel primero verifica el caché de la página para ver si los datos ya están en la memoria. Si es así, los datos se leen de la memoria en lugar del disco, que es mucho más rápido.

La memoria caché de la página es importante para el rendimiento, pero también puede causar problemas. Si un proceso necesita leer una gran cantidad de datos del disco, la memoria caché de la página puede llenarse rápidamente. Esto puede causar que el sistema se quede sin memoria y comience a intercambiar, lo cual es muy lento.

Para evitar este problema, el kernel usa una técnica llamada "intercambio". Swappiness es un parámetro ajustable que controla la agresividad con la que el núcleo utilizará la memoria caché de la página. Un valor de 0 significa que el kernel nunca se intercambiará, incluso si eso significa que el sistema se quedará sin memoria. Un valor de 100 significa que el núcleo siempre se intercambiará, incluso si no es necesario.

El valor predeterminado para swappiness es 60. Esto significa que el kernel usará la caché de la página de manera agresiva, pero aún así comenzará a intercambiar cuando sea necesario.

## Programación de procesos

Además de administrar la memoria, el kernel de Linux también es responsable de la programación de procesos. Los procesos se programan utilizando una variedad de algoritmos, incluido el programador de fecha límite, el programador justo y el programador completamente justo.

El programador de fechas límite está diseñado para procesos en tiempo real que necesitan completar su trabajo dentro de un período de tiempo específico.

El programador justo está diseñado para procesos por lotes que pueden ejecutarse durante mucho tiempo sin interrupción.

El programador completamente justo es el programador predeterminado en la mayoría de las distribuciones de Linux. Está diseñado para proporcionar un acceso justo a la CPU para todos los procesos.

## Conclusión

La gestión de la memoria y la programación de procesos son aspectos importantes del desarrollo de Linux. Los desarrolladores deben ser conscientes de cómo el kernel administra la memoria y la programación de procesos para optimizar el rendimiento y evitar problemas.