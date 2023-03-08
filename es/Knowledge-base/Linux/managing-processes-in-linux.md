---
title: Gestión de procesos en Linux
description: 
published: true
date: 2023-02-11T07:32:34.383Z
tags: 
editor: markdown
dateCreated: 2023-02-11T07:32:27.726Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Managing Processes in Linux***English** document is available*](/en/Knowledge-base/Linux/managing-processes-in-linux)
{.links-list}


# Gestión de procesos en Linux

En este artículo, echaremos un vistazo a la gestión de procesos en Linux. Cubriremos algunos de los conceptos básicos de qué son los procesos y cómo funcionan, y luego veremos algunas de las herramientas y técnicas que puede usar para administrarlos.

## ¿Qué es un proceso?

Un proceso es una instancia de un programa que se está ejecutando. Cuando ejecuta un programa, crea un proceso. Un proceso tiene una serie de estructuras de datos asociadas, incluida una lista de archivos abiertos, una lista de subprocesos en ejecución y varias opciones específicas del proceso.

A cada proceso se le asigna una ID de proceso (PID) única, que el sistema operativo utiliza para realizar un seguimiento del proceso. Los procesos se pueden crear y destruir, y pueden estar en uno de tres estados:

- **En ejecución:** El proceso se está ejecutando actualmente.
- **Durmiente:** el proceso no se está ejecutando actualmente, pero está esperando que ocurra un evento (como una operación de E/S para completar).
- **Zombie:** El proceso terminó de ejecutarse, pero su proceso principal aún no ha recopilado su estado de salida.

## Gestión de Procesos

Hay una serie de herramientas y técnicas que puede usar para administrar procesos en Linux. Cubriremos algunos de los más comunes aquí.

### El comando ps

El comando **ps** se usa para enumerar los procesos que se están ejecutando actualmente. De forma predeterminada, solo mostrará los procesos iniciados por el usuario actual. Para ver todos los procesos, use la opción **-A**:

```
ps -A
```

Para ver más información sobre cada proceso, utilice la opción **-o**. Por ejemplo, para ver el PID, el comando y el usuario de cada proceso, use este comando:

```
ps -o pid,command,user
```

Hay una serie de otras opciones que puede usar con **ps**. Para obtener una lista completa, consulte la página man de **ps**.

### El comando superior

El comando **top** es similar a **ps**, pero proporciona una lista de procesos continuamente actualizada. También muestra información adicional, como el uso de CPU y memoria de cada proceso.

Para salir de **arriba**, presione **q**. Para ordenar la lista de procesos, presione **o** y luego ingrese los criterios de ordenación. Por ejemplo, para ordenar por PID, use este comando:

```
top -o pid
```

Para ver una pantalla de ayuda, presione **h**.

### El comando de matar

El comando **kill** se usa para enviar una señal a un proceso. Por defecto, envía la señal **SIGTERM**, que solicita que finalice el proceso. Si el proceso no responde a esa señal, puede usar la opción **-9** para enviar la señal **SIGKILL**, que fuerza la finalización del proceso.

Por ejemplo, para terminar el proceso con PID 1234, use este comando:

```
kill 1234
```

Para matar todos los procesos en el grupo de procesos con ID 5678, use este comando:

```
kill -9 -5678
```

Hay una serie de otras señales que puedes enviar con **matar**. Consulte la página man de **kill** para obtener una lista completa.

### El comando pkill

El comando **pkill** es similar a **kill**, pero le permite matar procesos por nombre en lugar de por PID. Por ejemplo, para eliminar todos los procesos con el nombre **firefox**, use este comando:

```
pkill firefox
```

Para eliminar todos los procesos que pertenecen al usuario **jane**, use este comando:

```
pkill -u jane
```

Para obtener una lista completa de opciones, consulte la página de manual de **pkill**.

### El Comando Killall

El comando **killall** es similar a **pkill**, pero elimina todos los procesos que coinciden con el nombre especificado, en lugar de solo el primero que encuentra. Por ejemplo, para eliminar todos los procesos con el nombre **firefox**, use este comando:

```
killall firefox
```

Para eliminar todos los procesos que pertenecen al usuario **jane**, use este comando:

```
killall -u jane
```

Para obtener una lista completa de opciones, consulte la página de manual de **killall**.

## Terminando

En este artículo, hemos cubierto algunos de los conceptos básicos de la gestión de procesos en Linux. Hemos visto cómo usar los comandos **ps**, **top**, **kill**, **pkill** y **killall** para administrar procesos.