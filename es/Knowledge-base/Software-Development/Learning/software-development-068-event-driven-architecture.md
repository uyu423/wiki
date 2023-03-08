---
title: Desarrollo de software 068: Arquitectura impulsada por eventos
description: 
published: true
date: 2023-02-10T18:17:26.728Z
tags: 
editor: markdown
dateCreated: 2023-02-10T18:17:25.062Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Software Development 068: Event-Driven Architecture***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-068-event-driven-architecture)
{.links-list}


# Desarrollo de software 068: Arquitectura impulsada por eventos

En ingeniería de software, la arquitectura dirigida por eventos (EDA) es un patrón de arquitectura de software que promueve la producción, detección, consumo y reacción a eventos. Un evento se puede definir como "un cambio significativo en el estado".[1] Por ejemplo, cuando un usuario presiona un botón, se genera un evento. Este evento puede ser detectado por el software, que luego puede desencadenar una reacción, como cambiar la pantalla.

EDA se usa a menudo en el desarrollo de interfaces gráficas de usuario (GUI) y otras aplicaciones que están controladas por eventos. Sin embargo, EDA también se puede utilizar en otros tipos de software, como middleware y sistemas operativos.

## ¿Qué es un evento?

En ingeniería de software, un evento es un cambio significativo en el estado. Los eventos pueden ser generados por varias fuentes, como la entrada del usuario, sensores o mensajes del sistema. Una vez que se ha producido un evento, puede ser detectado por el software. Luego, el software puede desencadenar una reacción, como cambiar la pantalla o ejecutar una determinada tarea.

Los eventos se pueden clasificar en dos tipos:

- **Eventos sincrónicos** ocurren cuando el software está esperando que ocurra un evento antes de continuar. Por ejemplo, cuando un usuario hace clic en un botón, el software esperará a que ocurra el evento de clic antes de continuar.

- **Eventos asincrónicos** ocurren cuando el software no está esperando que ocurra un evento. Por ejemplo, cuando se recibe un mensaje de red, el software seguirá ejecutándose y el mensaje se procesará en segundo plano.

## ¿Qué es una arquitectura impulsada por eventos?

La arquitectura basada en eventos (EDA) es un patrón de arquitectura de software que promueve la producción, detección, consumo y reacción a eventos.

EDA se usa a menudo en el desarrollo de interfaces gráficas de usuario (GUI) y otras aplicaciones que están controladas por eventos. Sin embargo, EDA también se puede utilizar en otros tipos de software, como middleware y sistemas operativos.

EDA consta de tres componentes principales:

- **Productores de eventos** generan eventos.

- **Consumidores de eventos** consumen eventos.

- **Canales de eventos** ofrecen eventos de productores a consumidores.

## Ventajas de la arquitectura impulsada por eventos

EDA tiene varias ventajas sobre otras arquitecturas de software:

- **Acoplamiento débil**: las arquitecturas basadas en eventos están débilmente acopladas, lo que significa que los productores y consumidores de eventos no dependen directamente unos de otros. Esto facilita la adición o eliminación de productores y consumidores de eventos sin afectar a los demás componentes.

- **Escalabilidad**: las arquitecturas basadas en eventos son escalables, lo que significa que se pueden expandir fácilmente para admitir más productores y consumidores de eventos.

- **Flexibilidad**: las arquitecturas basadas en eventos son flexibles, lo que significa que se pueden adaptar fácilmente a los requisitos cambiantes.

## Desventajas de la arquitectura impulsada por eventos

EDA también tiene algunas desventajas:

- **Complejidad**: las arquitecturas basadas en eventos pueden ser complejas, lo que las hace difíciles de entender y depurar.

- **Rendimiento**: las arquitecturas basadas en eventos pueden tener un rendimiento más bajo que otras arquitecturas, debido a la sobrecarga de la gestión de eventos.

## Conclusión

La arquitectura basada en eventos (EDA) es un patrón de arquitectura de software que promueve la producción, detección, consumo y reacción a eventos. EDA tiene varias ventajas, como el bajo acoplamiento, la escalabilidad y la flexibilidad. Sin embargo, EDA también puede ser complejo y tener un rendimiento más bajo que otras arquitecturas.