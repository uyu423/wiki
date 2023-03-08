---
title: Supervisión y registro del sistema Linux
description: 
published: true
date: 2023-02-12T10:32:20.537Z
tags: 
editor: markdown
dateCreated: 2023-02-12T10:32:13.961Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux System Monitoring and Logging***English** document is available*](/en/Knowledge-base/Linux/linux-system-monitoring-and-logging)
{.links-list}


# Supervisión y registro del sistema Linux

El sistema operativo Linux tiene muchas herramientas para monitorear el rendimiento y la actividad del sistema. Las herramientas son útiles para comprobar el estado del sistema y para diagnosticar y solucionar problemas.

El rendimiento del sistema se puede monitorear mediante herramientas que miden el uso de la CPU y la memoria, el tráfico de la red, la actividad del disco y la información del proceso. La actividad del sistema se puede monitorear usando herramientas que rastrean los archivos de registro del sistema, la actividad del usuario y la información del proceso.

## Uso de CPU y memoria

El comando superior es un monitor de actividad del sistema de propósito general. Se puede usar para ver información sobre los procesos que se están ejecutando actualmente, incluida la identificación del proceso, la identificación del usuario, el uso de la CPU y el uso de la memoria. El comando htop es una alternativa más fácil de usar que top.

El comando vmstat se puede usar para ver información sobre la memoria virtual, incluido el uso de la memoria, la actividad del disco y la información del proceso. El comando iostat se puede usar para ver información sobre la actividad del disco.

El comando free se puede utilizar para ver información sobre la cantidad de memoria libre y utilizada en el sistema. La opción -m muestra la salida en megabytes.

## Tráfico de red

El comando iftop se puede usar para ver información sobre el tráfico de la red. El comando tcpdump se puede usar para capturar y ver el tráfico de la red.

## Actividad del disco

El comando iotop se puede usar para ver información sobre la actividad del disco. La opción -d muestra la salida en megabytes por segundo.

## Procesar informacion

El comando ps se puede usar para ver información sobre los procesos. La opción -e muestra todos los procesos. La opción -f muestra la línea de comando completa para cada proceso.

El comando pstree se puede usar para ver un árbol de procesos. La opción -p muestra el ID de proceso para cada proceso.

El comando lsof se puede usar para ver información sobre archivos abiertos. La opción -n muestra los archivos de red.

El comando kill se puede usar para matar un proceso. La opción -9 envía una señal SIGKILL al proceso.

## Archivos de registro del sistema

El archivo /var/log/messages contiene mensajes del sistema. El archivo /var/log/secure contiene mensajes de seguridad. El archivo /var/log/apache2/access.log contiene registros de acceso de Apache.

## Actividad del usuario

El comando w se puede usar para ver información sobre la actividad del usuario. La opción -u muestra información para un usuario específico.

El último comando se puede usar para ver información sobre los últimos usuarios que iniciaron sesión. La opción -x muestra información sobre los reinicios del sistema.

El comando who se puede utilizar para ver información sobre los usuarios que han iniciado sesión actualmente.

## Conclusión

Linux proporciona muchas herramientas para monitorear el rendimiento y la actividad del sistema. Las herramientas son útiles para comprobar el estado del sistema y para diagnosticar y solucionar problemas.