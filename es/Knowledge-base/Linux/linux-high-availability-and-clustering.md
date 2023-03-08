---
title: Alta disponibilidad y agrupamiento de Linux
description: 
published: true
date: 2023-02-10T05:17:26.009Z
tags: 
editor: markdown
dateCreated: 2023-02-10T05:17:24.394Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux High Availability and Clustering***English** document is available*](/en/Knowledge-base/Linux/linux-high-availability-and-clustering)
{.links-list}


# Alta disponibilidad y agrupamiento de Linux

La alta disponibilidad (HA) y la agrupación en clústeres son temas importantes para cualquiera que trabaje con servidores Linux. En este artículo, cubriremos qué son HA y clústeres, cómo funcionan y algunos casos de uso comunes.

## ¿Qué es la alta disponibilidad?

La alta disponibilidad es una característica de un sistema o componente que describe la capacidad del sistema para proporcionar un servicio ininterrumpido durante un cierto período de tiempo. Un sistema con alta disponibilidad es aquel que está diseñado para minimizar el tiempo de inactividad y las interrupciones.

Hay muchos factores que contribuyen a la disponibilidad general de un sistema, entre ellos:

- Hardware: La calidad de los componentes de hardware utilizados en el sistema.
- Software: La calidad de los componentes de software utilizados en el sistema.
- Redes: La calidad de las redes que conectan los componentes del sistema.
- Procedimientos: Los procedimientos y procesos utilizados para mantener y operar el sistema.

## ¿Qué es la agrupación en clústeres?

La agrupación en clústeres es un tipo de solución de alta disponibilidad que involucra múltiples sistemas (llamados nodos) que trabajan juntos para brindar un servicio ininterrumpido. Los clústeres a menudo se utilizan para proporcionar capacidades de conmutación por error, de modo que si un nodo del clúster falla, los otros nodos pueden tomar el control y mantener el sistema en funcionamiento.

Los clústeres se pueden usar para una variedad de propósitos, incluido el equilibrio de carga, el almacenamiento y el nivel de aplicación HA.

## ¿Cómo funcionan juntos la alta disponibilidad y el agrupamiento?

Una de las formas más comunes de lograr una alta disponibilidad es mediante el uso de clústeres. Los clústeres pueden proporcionar varios niveles de disponibilidad, según la configuración. Por ejemplo, un clúster de dos nodos puede proporcionar funciones básicas de conmutación por error, mientras que un clúster más complejo puede proporcionar equilibrio de carga y otras funciones avanzadas.

Hay algunos tipos diferentes de clústeres, que incluyen:

- Activo/pasivo: en un clúster activo/pasivo, un nodo está activo y los otros nodos están en espera. El nodo activo maneja todo el tráfico y los nodos en espera solo se usan si el nodo activo deja de funcionar.

- Activo/activo: en un clúster activo/activo, todos los nodos están activos y manejan el tráfico. Este tipo de configuración se usa a menudo para equilibrar la carga.

- N+1: en un clúster N+1, hay N nodos activos y un nodo en espera. El nodo en espera se utiliza si uno de los nodos activos deja de funcionar.

## Casos de uso para alta disponibilidad y agrupamiento

Hay muchos casos de uso potenciales para la alta disponibilidad y el agrupamiento. Algunos ejemplos comunes incluyen:

- Servidores web: los clústeres se utilizan a menudo para proporcionar alta disponibilidad a los servidores web. Por ejemplo, se puede usar un grupo de servidores web para proporcionar capacidades de conmutación por error en caso de que uno de los servidores se caiga.

- Bases de datos: los clústeres también se pueden utilizar para proporcionar alta disponibilidad para las bases de datos. Por ejemplo, se puede usar un grupo de servidores de bases de datos para proporcionar capacidades de conmutación por error en caso de que uno de los servidores se caiga.

- Equilibrio de carga: los clústeres se pueden utilizar para equilibrar la carga del tráfico entre varios servidores. Esto puede ayudar a mejorar el rendimiento y evitar que un servidor se sobrecargue.

## Conclusión

La alta disponibilidad y la agrupación en clústeres son temas importantes para cualquiera que trabaje con servidores Linux. En este artículo, hemos cubierto qué son HA y agrupación en clústeres, cómo funcionan y algunos casos de uso comunes.