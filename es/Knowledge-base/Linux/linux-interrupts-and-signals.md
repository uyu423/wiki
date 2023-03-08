---
title: Interrupciones y señales de Linux
description: 
published: true
date: 2023-02-11T14:32:22.759Z
tags: 
editor: markdown
dateCreated: 2023-02-11T14:32:21.103Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Interrupts and Signals***English** document is available*](/en/Knowledge-base/Linux/linux-interrupts-and-signals)
{.links-list}


# Interrupciones y señales de Linux

Una interrupción es un evento que requiere la atención del núcleo del sistema operativo. Cuando ocurre una interrupción, el núcleo puede suspender el proceso actual y ejecutar un controlador de interrupción especial para tratar el evento.

Una señal es una interrupción de software que el kernel u otro proceso envía a un proceso. El usuario puede generar una señal, como con el comando de eliminación, o el sistema operativo en respuesta a un evento, como una falla de segmentación.

Las interrupciones y las señales son similares, pero tienen algunas diferencias importantes.

## Interrupciones

El hardware genera una interrupción y hace que el kernel suspenda el proceso actual y ejecute un controlador de interrupción especial.

Las interrupciones pueden ser generadas por el usuario, como con el comando kill, o por el sistema operativo en respuesta a un evento, como una falla de segmentación.

## Señales

Una señal es una interrupción de software que se envía a un proceso. El usuario puede generar una señal, como con el comando de eliminación, o el sistema operativo en respuesta a un evento, como una falla de segmentación.

Las señales son generadas por el núcleo o por otro proceso. Cuando se genera una señal, el kernel puede suspender el proceso actual y ejecutar un controlador de señal especial para tratar el evento.

## Diferencias

Las interrupciones y las señales son similares, pero tienen algunas diferencias importantes:

- Las interrupciones son generadas por hardware, mientras que las señales son generadas por el kernel u otro proceso.
- Las interrupciones hacen que el núcleo suspenda el proceso actual y ejecute un controlador de interrupción especial. Las señales pueden hacer que el kernel suspenda el proceso actual y ejecute un controlador de señal especial.
- El usuario puede generar interrupciones, mientras que las señales solo pueden ser generadas por el kernel u otro proceso.

## Recursos externos

- [Wikipedia: Interrupción](https://en.wikipedia.org/wiki/Interrupción)
- [Wikipedia: Signal (informática)](https://en.wikipedia.org/wiki/Signal_(informática))
- [Documentación del kernel de Linux: interrupciones] (https://www.kernel.org/doc/Documentation/virtual/kvm/async_pf.txt)
- [Documentación del Kernel de Linux: Señales](https://www.kernel.org/doc/Documentation/signals.txt)