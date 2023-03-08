---
title: Gestión de clústeres para alta disponibilidad
description: 
published: true
date: 2023-02-12T20:55:24.538Z
tags: 
editor: markdown
dateCreated: 2023-02-12T20:55:22.950Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Managing Clusters for High Availability***English** document is available*](/en/Knowledge-base/Backend/managing-clusters-for-high-availability)
{.links-list}


# Gestión de clústeres para alta disponibilidad

 La alta disponibilidad es una característica de un sistema, cuyo objetivo es garantizar un nivel acordado de rendimiento operativo, generalmente tiempo de actividad, durante un período superior al normal. Lograr una alta disponibilidad a menudo implica implementar redundancias en todo el sistema. Por ejemplo, si falla un componente, el sistema puede cambiar a un componente redundante, sin ninguna interrupción en el servicio.

Los sistemas de TI son cada vez más críticos y se espera que estén disponibles las 24 horas del día, los 7 días de la semana. Sin embargo, no importa qué tan bien esté diseñado y construido un sistema, los componentes inevitablemente fallarán en algún momento. La clave para lograr una alta disponibilidad es diseñar el sistema de modo que pueda tolerar las fallas de los componentes sin interrumpir el servicio.

Hay muchos factores a considerar cuando se diseña para alta disponibilidad, incluyendo:

- Hardware: servidores, almacenamiento, redes, etc.
- Software: sistema operativo, aplicaciones, bases de datos, etc.
- Procesos: monitorización, backup y recovery, etc.

## Herrajes

Los componentes de hardware redundantes son una parte clave para lograr una alta disponibilidad. Por ejemplo, si falla un servidor, el sistema puede cambiar a un servidor redundante.

Los componentes de hardware redundantes comunes incluyen:

- Servidores: se pueden utilizar varios servidores, y cada servidor ejecuta un componente diferente del sistema. Por ejemplo, un servidor podría ejecutar la aplicación, mientras que otro servidor ejecuta la base de datos.
- Almacenamiento: el almacenamiento se puede replicar en varios servidores. Por ejemplo, la aplicación y la base de datos podrían almacenarse en dos servidores diferentes.
- Red: se pueden usar varias conexiones de red, y cada conexión se ejecuta en un conmutador diferente.

## Software

Los componentes de software de un sistema también deben diseñarse para una alta disponibilidad. Por ejemplo, la aplicación debe estar diseñada para manejar correctamente las fallas del servidor.

Las técnicas de software comunes para lograr una alta disponibilidad incluyen:

- Equilibrio de carga: se pueden utilizar varios servidores, y cada servidor ejecuta un componente diferente del sistema. Por ejemplo, un servidor podría ejecutar la aplicación, mientras que otro servidor ejecuta la base de datos.
- Replicación: los datos se pueden replicar en varios servidores. Por ejemplo, la aplicación y la base de datos podrían almacenarse en dos servidores diferentes.
- Agrupación: se pueden agrupar varios servidores, de modo que si un servidor falla, los demás pueden hacerse cargo.

## Procesos

Además de los componentes de hardware y software, los procesos de un sistema también deben diseñarse para una alta disponibilidad. Por ejemplo, el sistema debe monitorearse para que las fallas de los componentes puedan detectarse y remediarse rápidamente.

Los procesos comunes para lograr una alta disponibilidad incluyen:

- Monitoreo: el sistema debe ser monitoreado para que cualquier falla en los componentes pueda ser detectada rápidamente.
- Copia de seguridad y recuperación: se debe hacer una copia de seguridad del sistema con regularidad, de modo que si un componente falla, el sistema se pueda restaurar rápidamente.

## Conclusión

Lograr una alta disponibilidad es un objetivo clave de los sistemas de TI. Hay muchos factores a considerar cuando se diseña para alta disponibilidad, incluidos hardware, software y procesos.