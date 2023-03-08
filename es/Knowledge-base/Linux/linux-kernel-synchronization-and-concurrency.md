---
title: Sincronización y concurrencia del kernel de Linux
description: 
published: true
date: 2023-02-11T18:32:25.707Z
tags: 
editor: markdown
dateCreated: 2023-02-11T18:32:18.908Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Kernel Synchronization and Concurrency***English** document is available*](/en/Knowledge-base/Linux/linux-kernel-synchronization-and-concurrency)
{.links-list}


# Sincronización y concurrencia del kernel de Linux

La concurrencia en el kernel de Linux se logra al permitir que múltiples procesos se ejecuten simultáneamente. Para hacer esto, el núcleo debe proporcionar un mecanismo para sincronizar el acceso a las estructuras de datos compartidas.

Hay dos formas principales en que el kernel puede lograr la concurrencia:

- Multitarea preventiva: el kernel puede permitir que varios procesos compartan la CPU programándolos de forma preventiva.
- Multitarea cooperativa: el kernel puede permitir que múltiples procesos compartan la CPU al ceder voluntariamente el control de la CPU.

El kernel de Linux utiliza una combinación de multitarea preventiva y cooperativa.

La multitarea preventiva se utiliza para tareas críticas que no pueden interrumpirse, como el manejo de interrupciones de hardware. La multitarea cooperativa se utiliza para tareas que pueden interrumpirse, como los procesos en el espacio del usuario.

El kernel de Linux utiliza varios mecanismos de sincronización diferentes para lograr la concurrencia, que incluyen:

- Operaciones atómicas: Son operaciones que no se pueden interrumpir. Por lo general, se usan para secciones críticas de código que no pueden permitirse ser interrumpidas.
- Spinlocks: estos son bloqueos que hacen que un proceso esté ocupado: espere hasta que se libere el bloqueo. Por lo general, se usan para secciones críticas cortas de código.
- Mutexes: estos son bloqueos que hacen que un proceso entre en suspensión hasta que se libera el bloqueo. Por lo general, se usan para secciones de código críticas más largas.
- Semáforos: Son un tipo de bloqueo que permiten que un proceso duerma hasta que se cumpla una determinada condición. Por lo general, se utilizan para la sincronización entre procesos.

El kernel de Linux también proporciona una serie de mecanismos para gestionar la programación de procesos, la gestión de la memoria y otros aspectos de la concurrencia.

## Programación de procesos

El kernel de Linux proporciona una serie de mecanismos para administrar la programación de procesos.

El programador del kernel es responsable de programar los procesos para que se ejecuten en la CPU. Utiliza una serie de algoritmos de programación para decidir qué proceso debe ejecutarse a continuación.

El algoritmo de programación más común es el programador de turnos. Este programador programa los procesos en orden Primero en entrar, primero en salir (FIFO).

Otros algoritmos de programación incluyen el programador de prioridad, que programa procesos en función de su prioridad, y el programador de fecha límite, que programa procesos en función de su fecha límite.

El núcleo también proporciona un mecanismo para procesos en tiempo real. Los procesos en tiempo real tienen una prioridad más alta que otros procesos y se garantiza que se programarán de manera oportuna.

## Gestión de la memoria

El kernel de Linux proporciona una serie de mecanismos para administrar la memoria.

El núcleo utiliza una serie de estrategias de gestión de memoria, incluidas la paginación y el intercambio.

La paginación es una técnica que permite que el kernel mapee la memoria del proceso en la memoria física. Esto permite que el kernel use la memoria física de manera más eficiente.

El intercambio es una técnica que permite que el núcleo escriba memoria de proceso en el disco. Esto permite que el kernel libere memoria física para otros procesos.

El núcleo también proporciona un mecanismo para la memoria compartida. La memoria compartida permite que los procesos compartan memoria entre ellos.

## Comunicación entre procesos

El kernel de Linux proporciona una serie de mecanismos para la comunicación entre procesos (IPC).

IPC permite que los procesos se comuniquen entre sí. La forma más común de IPC es el paso de mensajes.

El paso de mensajes permite que los procesos se envíen mensajes entre sí. El kernel proporciona una serie de mecanismos de paso de mensajes, incluidos conductos, FIFO y sockets.

Las tuberías y los FIFO permiten que los procesos se comuniquen entre sí mediante un flujo de datos unidireccional. Los sockets permiten que los procesos se comuniquen entre sí mediante un flujo de datos bidireccional.

El núcleo también proporciona un mecanismo para la memoria compartida. La memoria compartida permite que los procesos compartan memoria entre ellos.

## Conclusión

El kernel de Linux proporciona una serie de mecanismos para lograr la concurrencia. Estos mecanismos incluyen multitarea preventiva, multitarea cooperativa, spinlocks, mutexes, semáforos y una variedad de otras estrategias de programación de procesos y gestión de memoria.