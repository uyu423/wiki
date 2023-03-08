---
title: Recolectores de basura de baja pausa de Java: comprensión de G1GC
description: 
published: true
date: 2023-02-13T07:17:26.605Z
tags: 
editor: markdown
dateCreated: 2023-02-13T07:17:25.027Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Java's Low-Pause Garbage Collectors: Understanding G1GC***English** document is available*](/en/Knowledge-base/Java/java-s-low-pause-garbage-collectors-understanding-g1gc)
{.links-list}


# Recolectores de basura de baja pausa de Java: comprensión de G1GC

El recolector de elementos no utilizados (GC) G1 de Java es un recolector de pausa baja que intenta minimizar los tiempos de pausa del GC. Lo hace dividiendo el montón en varias regiones más pequeñas y recopilándolas individualmente.

G1GC se introdujo por primera vez en Java 7 y es el GC predeterminado en Java 8. Se considera que es el sucesor del CMS GC.

## Cómo funciona G1GC

G1GC divide el montón en varias regiones. Cada región tiene un tamaño fijo y cada región puede contener uno o dos objetos.

Cuando una región está llena, se considera "basura" y se recolecta. Los objetos de la región no se mueven; simplemente son liberados.

G1GC utiliza una serie de técnicas para minimizar los tiempos de pausa del GC, que incluyen:

- **Paralelismo:** G1GC puede recopilar regiones en paralelo, utilizando varios subprocesos.

- **Marcado simultáneo:** G1GC puede marcar objetos mientras se ejecuta la aplicación, en lugar de esperar hasta un ciclo de GC para hacerlo.

- **Recopilación incremental:** G1GC puede recopilar regiones de forma incremental, recopilando solo unas pocas regiones a la vez.

G1GC es un recopilador de pausa baja, pero no es un recopilador de baja latencia. Los tiempos de pausa de G1GC aún pueden ser significativos, y las aplicaciones que requieren GC de baja latencia pueden adaptarse mejor a otro recopilador, como CMS GC.

## Rendimiento G1GC

G1GC está diseñado para minimizar los tiempos de pausa del GC, pero no siempre es el GC más rápido. En algunos casos, G1GC puede ser más lento que otros recopiladores.

G1GC es particularmente adecuado para aplicaciones con grandes montones y una gran cantidad de objetos. G1GC también puede ser una buena opción para aplicaciones con requisitos de alto rendimiento.

## Cuándo usar G1GC

G1GC es una buena opción para aplicaciones con grandes montones y una gran cantidad de objetos. G1GC también puede ser una buena opción para aplicaciones con requisitos de alto rendimiento.

## Cuándo no usar G1GC

G1GC no siempre es la mejor opción para las aplicaciones. En algunos casos, G1GC puede ser más lento que otros recopiladores.

G1GC es particularmente adecuado para aplicaciones con grandes montones y una gran cantidad de objetos. G1GC también puede ser una buena opción para aplicaciones con requisitos de alto rendimiento.

## Conclusión

G1GC es un recolector de basura de baja pausa que está diseñado para minimizar los tiempos de pausa del GC. G1GC es una buena opción para aplicaciones con grandes montones y una gran cantidad de objetos. G1GC también puede ser una buena opción para aplicaciones con requisitos de alto rendimiento.