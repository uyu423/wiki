---
title: Programación de E/S de Linux y administración de discos
description: 
published: true
date: 2023-02-11T17:32:34.306Z
tags: 
editor: markdown
dateCreated: 2023-02-11T17:32:32.649Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux I/O Scheduling and Disk Management***English** document is available*](/en/Knowledge-base/Linux/linux-io-scheduling-and-disk-management)
{.links-list}


# Programación de E/S de Linux y administración de discos

El planificador de E/S del kernel de Linux es responsable de optimizar el orden en que se envían las solicitudes de E/S de bloque desde la capa de bloque del kernel a los dispositivos de almacenamiento. Este proceso, conocido como programación de E/S, puede tener un impacto significativo en el rendimiento del sistema.

Hay tres objetivos principales de la programación de E/S:

- Mejore el rendimiento reordenando las solicitudes para minimizar las búsquedas
- Mejorar el rendimiento mediante la fusión de solicitudes
- Reduzca la latencia dando prioridad a las solicitudes de procesos con menor prioridad de E/S

El programador de E/S en el kernel de Linux está diseñado para equilibrar estos tres objetivos.

## Algoritmos de programación de E/S

Hay tres algoritmos de programación de E/S disponibles en el kernel de Linux:

- Programador de E/S de fecha límite
- Programador de E/S Noop
- Programador de E/S CFQ

El programador de E/S de fecha límite es el programador de E/S predeterminado en el kernel de Linux. Está diseñado para minimizar la latencia al dar prioridad a las solicitudes de procesos con menor prioridad de E/S.

El programador de E/S de Noop es un programador de E/S muy simple que no reordena las solicitudes. Por lo general, se usa para dispositivos con latencia de E/S muy baja, como unidades de estado sólido.

El programador de E/S CFQ es el programador de E/S predeterminado en la mayoría de las distribuciones de Linux. Está diseñado para equilibrar los tres objetivos de la programación de E/S: minimizar el tiempo de búsqueda, fusionar solicitudes y reducir la latencia.

## Cambio del programador de E/S

El planificador de E/S se puede cambiar por dispositivo usando la opción `-s` del comando `blockdev`. Por ejemplo, para cambiar el programador de E/S de `/dev/sda` al programador de E/S de fecha límite, usaría el siguiente comando:

```
blockdev -s /dev/sda deadline
```

El planificador de E/S también se puede cambiar según el sistema de archivos. Para cambiar el programador de E/S del sistema de archivos `/` al programador de E/S de CFQ, usaría el siguiente comando:

```
mount -o remount,ioscheduler=cfq /
```

## Programación de E/S y administración de discos

El programador de E/S puede tener un impacto significativo en el rendimiento del disco. Por ejemplo, el programador de E/S de fecha límite está diseñado para minimizar la latencia al dar prioridad a las solicitudes de procesos con menor prioridad de E/S. Esto puede dar como resultado un mayor rendimiento para los procesos con alta prioridad de E/S, como los servidores de bases de datos.

El programador de E/S de CFQ está diseñado para equilibrar los tres objetivos de la programación de E/S: minimizar el tiempo de búsqueda, fusionar solicitudes y reducir la latencia. Esto puede resultar en un mayor rendimiento para la mayoría de las cargas de trabajo.

## Conclusión

El planificador de E/S en el kernel de Linux es responsable de optimizar el orden en el que se envían las solicitudes de E/S de bloque desde la capa de bloque del kernel a los dispositivos de almacenamiento. Hay tres objetivos principales de la programación de E/S: mejorar el rendimiento reordenando las solicitudes para minimizar las búsquedas, mejorar el rendimiento fusionando solicitudes y reducir la latencia dando prioridad a las solicitudes de procesos con menor prioridad de E/S.

El programador de E/S puede tener un impacto significativo en el rendimiento del disco. El planificador de E/S de fecha límite está diseñado para minimizar la latencia al dar prioridad a las solicitudes de procesos con menor prioridad de E/S. El programador de E/S de CFQ está diseñado para equilibrar los tres objetivos de la programación de E/S: minimizar el tiempo de búsqueda, fusionar solicitudes y reducir la latencia.

## Recursos

- [Programación de E/S de Linux](https://www.kernel.org/doc/Documentation/block/ioprio.txt)
- [Programador de E/S](https://en.wikipedia.org/wiki/I/O_scheduler)
- [Programador de E/S de Noop](https://www.kernel.org/doc/Documentation/block/noop-iosched.txt)
- [Programador de E/S de CFQ](https://www.kernel.org/doc/Documentation/block/cfq-iosched.txt)
- [programador de E/S de fecha límite] (https://www.kernel.org/doc/Documentation/block/deadline-iosched.txt)