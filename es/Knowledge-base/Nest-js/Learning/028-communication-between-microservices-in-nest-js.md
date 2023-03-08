---
title: 028: Comunicación entre microservicios en Nest.js
description: 
published: true
date: 2023-02-15T08:32:23.808Z
tags: 
editor: markdown
dateCreated: 2023-02-15T08:32:21.796Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [028: Communication between microservices in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/028-communication-between-microservices-in-nest-js)
{.links-list}


## Introducción

Los microservicios son un estilo arquitectónico popular para crear aplicaciones escalables tolerantes a fallas. Nest.js es un marco para crear aplicaciones de Node.js que utiliza esta arquitectura.

En una arquitectura de microservicios, cada servicio es responsable de una tarea específica. Los servicios se comunican entre sí para completar una solicitud. Esta comunicación puede ocurrir de diferentes maneras, dependiendo de las necesidades de la aplicación.

En esta publicación, veremos algunas de las formas en que los microservicios pueden comunicarse entre sí en una aplicación Nest.js. También veremos algunos de los beneficios y desventajas de cada enfoque.

## HTTP y RESTO

Una de las formas más comunes para que los microservicios se comuniquen es a través de HTTP y REST. En este enfoque, cada servicio expone una API REST. Luego, los servicios pueden realizar solicitudes HTTP entre sí para acceder a los datos o realizar acciones.

Una ventaja de este enfoque es que es independiente del idioma. Cualquier idioma que pueda realizar solicitudes HTTP puede comunicarse con una API REST. Esto facilita la integración de servicios escritos en diferentes idiomas.

Otro beneficio es que las API REST están bien definidas. Esto facilita la documentación y prueba de las API.

Un inconveniente de este enfoque es que puede introducir latencia en el sistema. Las solicitudes HTTP pueden tardar en completarse, especialmente si los servicios se encuentran en diferentes ubicaciones geográficas.

Otro inconveniente es que las API REST pueden ser complejas de implementar. Requieren una planificación cuidadosa para garantizar que sean fáciles de usar y mantener.

## Colas de mensajes

Otra forma común para que los microservicios se comuniquen es a través de colas de mensajes. En este enfoque, cada servicio tiene una cola de mensajes. Los servicios pueden enviarse mensajes entre sí a través de las colas.

Una ventaja de este enfoque es que se puede utilizar para desacoplar servicios. Los servicios pueden procesar mensajes de forma asíncrona, sin tener que esperar una respuesta del otro servicio. Esto puede mejorar el rendimiento del sistema.

Otro beneficio es que las colas de mensajes a menudo se usan para implementar un modelo de publicación/suscripción. Esto permite que los servicios se suscriban a los mensajes que les interesan. Esto se puede usar para implementar arquitecturas basadas en eventos.

Un inconveniente de este enfoque es que puede ser difícil de depurar. Los mensajes pueden enviarse a la cola incorrecta o procesarse desordenadamente. Esto puede dificultar la localización de problemas en el sistema.

Otro inconveniente es que las colas de mensajes pueden introducir una complejidad adicional en el sistema. Requieren infraestructura adicional para su instalación y mantenimiento.

## gRPC

gRPC es un marco RPC de alto rendimiento. Utiliza HTTP/2 y búferes de protocolo para proporcionar una forma eficiente de que los servicios se comuniquen.

Una ventaja de gRPC es que es muy rápido. Utiliza un protocolo binario y HTTP/2, lo que puede reducir la latencia.

Otro beneficio es que gRPC es independiente del idioma. Los servicios se pueden escribir en cualquier idioma y seguir comunicándose entre sí.

Una desventaja de gRPC es que puede ser complejo de configurar. Requiere infraestructura adicional, como un servidor gRPC.

Otro inconveniente es que gRPC no se adopta tan ampliamente como otros enfoques. Esto puede dificultar la búsqueda de recursos y apoyo.

## Conclusión

Hay muchas formas de que los microservicios se comuniquen entre sí. El mejor enfoque depende de las necesidades de la aplicación.

HTTP y REST son enfoques comunes que son independientes del idioma y están bien definidos. Pero pueden introducir latencia y complejidad.

Las colas de mensajes se pueden utilizar para desacoplar servicios y mejorar el rendimiento. Pero pueden ser difíciles de depurar y agregar complejidad adicional.

gRPC es un marco RPC de alto rendimiento que es independiente del idioma. Pero puede ser complejo de configurar y no se adopta tan ampliamente.