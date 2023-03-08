---
title: Programación de procesos de Linux
description: 
published: true
date: 2023-02-11T13:32:46.637Z
tags: 
editor: markdown
dateCreated: 2023-02-11T13:32:44.899Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Process Scheduling***English** document is available*](/en/Knowledge-base/Linux/linux-process-scheduling)
{.links-list}


# Programación de procesos de Linux

El planificador de procesos de Linux es un planificador preventivo basado en prioridades. El planificador selecciona el siguiente proceso para ejecutar en función de su prioridad y otros factores. El programador se implementa como una cola FIFO (primero en entrar, primero en salir).

## Algoritmos de programación de procesos

El programador de procesos de Linux admite varios algoritmos de programación:

* Primero en entrar, primero en salir (FIFO)
* Ronda Robin (RR)
* Programación preferencial de prioridad estática (SPP)
* Programación preventiva de prioridad dinámica (DPP)
* Programación de múltiples colas (MQS)
* Programación Completamente Justa (CFS)

El programador utiliza el siguiente algoritmo para seleccionar el siguiente proceso a ejecutar:

1. El programador selecciona el proceso con la prioridad más alta.
2. Si hay varios procesos con la misma prioridad, el programador selecciona el proceso que ha estado esperando más tiempo.
3. Si hay varios procesos con la misma prioridad y el mismo tiempo de espera, el programador selecciona el proceso con el pid más bajo.

## Proceso prioritario

A cada proceso se le asigna una prioridad. La prioridad es un valor entero entre -20 y 19. Cuanto menor sea el valor de prioridad, mayor será la prioridad del proceso. La prioridad por defecto de un proceso es 0.

Se puede asignar una prioridad más alta a un proceso usando el comando `nice`. Por ejemplo, para asignar una prioridad de 10 al proceso `Firefox`, usaría el siguiente comando:

```
$ nice -n 10 firefox
```

Se puede asignar una prioridad más baja a un proceso usando el comando `renice`. Por ejemplo, para asignar una prioridad de -10 al proceso `Firefox`, usaría el siguiente comando:

```
$ renice -n -10 firefox
```

## Clases de programación de procesos

Los procesos se clasifican en una de las siguientes clases de planificación:

* Tiempo real
* Mejor esfuerzo
* Inactivo

### Procesos en tiempo real

Los procesos en tiempo real tienen la máxima prioridad. Están garantizados para ser programados.

### Procesos de mejor esfuerzo

Los procesos de mejor esfuerzo tienen una prioridad entre 0 y 99. No se garantiza que se programen.

### Procesos inactivos

Los procesos inactivos tienen la prioridad más baja. Solo se programan cuando no hay otros procesos para ejecutar.

## Políticas de programación de procesos

Los procesos se pueden programar utilizando una de las siguientes políticas:

* FIFO
* RR
* SPP
* DPP
* MQS
* SFC

### FIFO

FIFO es la política de programación más simple. Programa los procesos en el orden en que se crean.

### RR

RR es una política de programación más avanzada. Programa los procesos de forma rotativa.

### SPP

SPP es una política de programación de prioridad estática. Programa los procesos en función de su prioridad estática.

### DPP

DPP es una política de programación de prioridad dinámica. Programa los procesos en función de su prioridad dinámica.

### MQS

MQS es una política de programación de varias colas. Programa los procesos en función de su cola.

### SFC

CFS es una política de programación completamente justa. Programa los procesos en función de su tiempo de espera.

## Parámetros de programación de procesos

El programador de procesos de Linux utiliza los siguientes parámetros para programar procesos:

* `nice`: La prioridad del proceso.
* `rt_priority`: La prioridad en tiempo real del proceso.
* `política`: La política de programación del proceso.
* `sched_latency`: El tiempo máximo que se puede retrasar un proceso antes de programarlo.
* `sched_min_granularity`: El tiempo mínimo entre programaciones del proceso.
* `sched_wakeup_granularity`: El tiempo entre programaciones del proceso cuando se despierta.

## Conclusión

El planificador de procesos de Linux es un planificador preventivo basado en prioridades. El planificador selecciona el siguiente proceso para ejecutar en función de su prioridad y otros factores. El programador se implementa como una cola FIFO (primero en entrar, primero en salir).

El programador utiliza el siguiente algoritmo para seleccionar el siguiente proceso a ejecutar:

1. El programador selecciona el proceso con la prioridad más alta.
2. Si hay varios procesos con la misma prioridad, el programador selecciona el proceso que ha estado esperando más tiempo.
3. Si hay varios procesos con la misma prioridad y el mismo tiempo de espera, el programador selecciona el proceso con el pid más bajo.

A cada proceso se le asigna una prioridad. La prioridad es un valor entero entre -20 y 19. Cuanto menor sea el valor de prioridad, mayor será la prioridad del proceso.

Los procesos se clasifican en una de las siguientes clases de planificación:

* Tiempo real
* Mejor esfuerzo
* Inactivo

Los procesos en tiempo real tienen la máxima prioridad. Están garantizados para ser programados.

Los procesos de mejor esfuerzo tienen una prioridad entre 0 y 99. No se garantiza que se programen.

Los procesos inactivos tienen la prioridad más baja. Solo se programan cuando no hay otros procesos para ejecutar.

Los procesos se pueden programar utilizando una de las siguientes políticas:

* FIFO
* RR
* SPP
* DPP
* MQS
* SFC

FIFO es la política de programación más simple. Programa los procesos en el orden en que se crean.

RR es una política de programación más avanzada. Programa los procesos de forma rotativa.

SPP es una política de programación de prioridad estática. Programa los procesos en función de su prioridad estática.

DPP es una política de programación de prioridad dinámica. Programa los procesos en función de su prioridad dinámica.

MQS es una política de programación de varias colas. Programa los procesos en función de su cola.

CFS es una política de programación completamente justa. Programa los procesos en función de su tiempo de espera.

El programador de procesos de Linux utiliza los siguientes parámetros para programar procesos:

* `nice`: La prioridad del proceso.
* `rt_priority`: La prioridad en tiempo real del proceso.
* `política`: La política de programación del proceso.
* `sched_latency`: El tiempo máximo que se puede retrasar un proceso antes de programarlo.
* `sched_min_granularity`: El tiempo mínimo entre programaciones del proceso.
* `sched_wakeup_granularity`: El tiempo entre programaciones del proceso cuando se despierta.