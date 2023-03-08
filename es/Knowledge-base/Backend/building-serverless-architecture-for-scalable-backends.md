---
title: Creación de una arquitectura sin servidor para backends escalables
description: 
published: true
date: 2023-02-01T23:23:39.229Z
tags: 
editor: markdown
dateCreated: 2023-02-01T23:23:37.628Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building Serverless Architecture for Scalable Backends***English** document is available*](/en/Knowledge-base/Backend/building-serverless-architecture-for-scalable-backends)
{.links-list}


# Creación de una arquitectura sin servidor para backends escalables

A medida que las empresas avanzan hacia la digitalización, la necesidad de backends escalables y confiables se vuelve más importante que nunca. La forma tradicional de construir backends, que consiste en aprovisionar y administrar servidores, puede ser costosa y consumir mucho tiempo. La arquitectura sin servidor es una nueva forma de crear backends que se está volviendo más popular porque es más escalable, confiable y rentable.

En este artículo, analizaremos qué es la arquitectura sin servidor y cómo se puede usar para crear backends escalables. También proporcionaremos algunos consejos prácticos sobre cómo comenzar a crear backends sin servidor.

## ¿Qué es la arquitectura sin servidor?

La arquitectura sin servidor es una nueva forma de crear backends que no requiere el aprovisionamiento ni la administración de servidores. En su lugar, se basa en una combinación de servicios administrados y proveedores de funciones como servicio (FaaS).

Los servicios administrados son servicios en la nube que abstraen la necesidad de administrar la infraestructura. Los ejemplos de servicios administrados incluyen bases de datos administradas, almacenamiento administrado y mensajería administrada. Los proveedores de FaaS le permiten ejecutar código sin tener que aprovisionar o administrar servidores. Los ejemplos de proveedores de FaaS incluyen AWS Lambda, Google Cloud Functions y Azure Functions.

Con la arquitectura sin servidor, puede crear backends que sean más escalables y confiables, y que se puedan implementar más rápido y a un menor costo.

## Cómo construir backends escalables con arquitectura sin servidor

Hay muchas formas de crear backends escalables con arquitectura sin servidor. En esta sección, analizaremos dos patrones comunes: la arquitectura basada en eventos y la arquitectura de microservicios.

### Arquitectura impulsada por eventos

La arquitectura basada en eventos es un patrón común para crear backends escalables con arquitectura sin servidor. En este patrón, los eventos se utilizan para desencadenar la ejecución del código. Por ejemplo, se puede generar un evento cuando un usuario se registra en un servicio, cuando se carga un archivo en un depósito de almacenamiento o cuando se envía un mensaje a una cola de mensajes.

La arquitectura basada en eventos es una buena opción para crear backends escalables porque se puede ampliar o reducir fácilmente. Por ejemplo, si tiene muchos usuarios que se registran en su servicio, puede ampliar su backend agregando más controladores de eventos. O bien, si tiene muchos archivos que se están cargando en su depósito de almacenamiento, puede escalar su backend agregando más código para manejar las cargas de archivos.

### Arquitectura de microservicios

La arquitectura de microservicios es otro patrón común para crear backends escalables con arquitectura sin servidor. En este patrón, cada servicio de backend es un microservicio independiente. Por ejemplo, si tiene un servicio de registro de usuarios, un servicio de carga de archivos y un servicio de cola de mensajes, cada uno de ellos sería un microservicio independiente.

La arquitectura de microservicios es una buena opción para crear backends escalables porque le permite escalar cada servicio de forma independiente. Por ejemplo, si tiene muchos usuarios que se registran en su servicio, puede escalar el servicio de registro de usuarios sin afectar a los otros servicios. O bien, si tiene muchos archivos que se están cargando en su depósito de almacenamiento, puede escalar el servicio de carga de archivos sin afectar a los otros servicios.

## Sugerencias para comenzar con backends sin servidor

Si es nuevo en la arquitectura sin servidor, aquí hay algunos consejos para ayudarlo a comenzar:

- Use servicios administrados: los servicios administrados pueden ayudarlo a comenzar con la arquitectura sin servidor de manera rápida y sencilla. Abstraen la necesidad de aprovisionar y administrar la infraestructura, y brindan una solución lista para tareas comunes de back-end.

- Utilice proveedores de FaaS: los proveedores de FaaS le permiten ejecutar código sin tener que aprovisionar o administrar servidores. Proporcionan una solución lista para ejecutar código en respuesta a eventos.

- Comience poco a poco: cuando se inicia por primera vez con la arquitectura sin servidor, es mejor comenzar poco a poco. Cree un backend simple que use algunos servicios administrados y proveedores de FaaS. Una vez que tenga una comprensión básica de cómo funciona la arquitectura sin servidor, puede comenzar a agregar más funciones y servicios.

- Utilice una canalización de CI/CD: una canalización de CI/CD puede ayudarlo a automatizar el proceso de creación, prueba e implementación de su backend sin servidor. Esto puede ayudarlo a ahorrar tiempo y garantizar que su backend esté siempre actualizado.

## Conclusión

La arquitectura sin servidor es una nueva forma de crear backends que se está volviendo más popular porque es más escalable, confiable y rentable. En este artículo, hemos discutido qué es la arquitectura sin servidor y cómo se puede usar para construir backends escalables. También proporcionamos algunos consejos sobre cómo comenzar con la arquitectura sin servidor.