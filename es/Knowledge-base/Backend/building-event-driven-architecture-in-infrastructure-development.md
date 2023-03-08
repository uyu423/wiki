---
title: Construcción de arquitectura impulsada por eventos en el desarrollo de infraestructura
description: 
published: true
date: 2023-02-04T15:55:25.738Z
tags: 
editor: markdown
dateCreated: 2023-02-04T15:55:24.187Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building Event-Driven Architecture in Infrastructure Development***English** document is available*](/en/Knowledge-base/Backend/building-event-driven-architecture-in-infrastructure-development)
{.links-list}


# Construcción de arquitectura impulsada por eventos en el desarrollo de infraestructura

## Introducción

Los desarrolladores están adoptando cada vez más la arquitectura basada en eventos (EDA) para crear aplicaciones escalables y resistentes. Esto se debe a que EDA permite el desacoplamiento de componentes, lo que hace que las aplicaciones sean más escalables y fáciles de mantener. Además, EDA puede hacer que las aplicaciones respondan mejor al permitir que los componentes reaccionen a los eventos a medida que ocurren, en lugar de buscar datos.

Hay muchos beneficios al usar EDA en el desarrollo de infraestructura. Por ejemplo, EDA puede ayudar a reducir la complejidad al permitir que los desarrolladores creen aplicaciones como un conjunto de componentes pequeños e independientes que se comunican entre sí a través de eventos. Esto puede hacer que las aplicaciones sean más escalables y fáciles de mantener. Además, EDA puede hacer que las aplicaciones respondan mejor al permitir que los componentes reaccionen a los eventos a medida que ocurren, en lugar de buscar datos.

Hay algunos desafíos que deben tenerse en cuenta al utilizar EDA en el desarrollo de infraestructura. En primer lugar, los desarrolladores deben elegir una plataforma de procesamiento de eventos adecuada. En segundo lugar, los desarrolladores deben diseñar los componentes de procesamiento de eventos de forma escalable y resistente. Finalmente, los desarrolladores deben considerar cómo manejar los eventos que ocurren en diferentes partes del mundo en diferentes momentos.

## Elegir una plataforma de procesamiento de eventos

Hay varias plataformas de procesamiento de eventos disponibles, cada una con sus propias ventajas y desventajas. Los desarrolladores deben elegir una plataforma que sea apropiada para su aplicación.

Una plataforma popular de procesamiento de eventos es Apache Kafka. Kafka es una plataforma de transmisión distribuida que es muy adecuada para crear aplicaciones escalables y resistentes. Kafka tiene una serie de características que lo hacen ideal para la arquitectura basada en eventos, incluida la compatibilidad con múltiples consumidores y productores, creación de particiones y replicación.

Otra plataforma popular de procesamiento de eventos es Apache Flume. Flume es un servicio distribuido, confiable y disponible para recopilar, agregar y mover de manera eficiente grandes cantidades de datos de transmisión. Flume tiene una serie de características que lo hacen ideal para la arquitectura basada en eventos, incluido un modelo de programación simple, soporte para múltiples fuentes de datos y equilibrio de carga integrado.

## Diseño de componentes de procesamiento de eventos

Al usar EDA en el desarrollo de infraestructura, los desarrolladores deben diseñar los componentes de procesamiento de eventos de una manera que sea escalable y resistente.

Una forma de hacerlo es utilizar una plataforma de middleware orientada a mensajes como Apache Camel. Camel es un marco de integración liviano que se puede usar para enrutar y procesar eventos de múltiples fuentes. Camel es altamente escalable y se puede implementar de forma distribuida.

Otra forma de diseñar componentes de procesamiento de eventos es usar una plataforma de procesamiento de flujo distribuido como Apache Storm. Storm es un sistema de computación distribuido, tolerante a fallas y en tiempo real. Storm es muy adecuado para la arquitectura basada en eventos porque puede procesar datos de múltiples fuentes en paralelo y puede manejar fallas con gracia.

## Manejo de eventos que ocurren en diferentes partes del mundo

Al usar EDA en el desarrollo de infraestructura, los desarrolladores deben considerar cómo manejar los eventos que ocurren en diferentes partes del mundo en diferentes momentos.

Una forma de hacer esto es usar una plataforma de procesamiento de transmisión distribuida como Apache Flink. Flink es una plataforma de procesamiento de flujo distribuido que puede manejar datos desordenados y que llegan tarde. Flink es muy adecuado para la arquitectura basada en eventos porque puede procesar datos de múltiples fuentes en paralelo y puede manejar fallas con gracia.

Otra forma de manejar eventos que ocurren en diferentes partes del mundo es usar una plataforma global de procesamiento de eventos como Apache Samza. Samza es una plataforma de procesamiento de flujo distribuido que puede procesar datos de múltiples fuentes en múltiples zonas horarias. Samza es muy adecuado para la arquitectura basada en eventos porque puede procesar datos de múltiples fuentes en paralelo y puede manejar fallas con gracia.

## Conclusión

La arquitectura basada en eventos es una herramienta poderosa para crear aplicaciones escalables y resistentes. Sin embargo, existen algunos desafíos que deben tenerse en cuenta al utilizar EDA en el desarrollo de infraestructura. Los desarrolladores deben elegir una plataforma de procesamiento de eventos adecuada y diseñar los componentes de procesamiento de eventos de manera escalable y resistente. Además, los desarrolladores deben considerar cómo manejar los eventos que ocurren en diferentes partes del mundo en diferentes momentos.