---
title: Inicio e inicialización del sistema Linux
description: 
published: true
date: 2023-02-11T04:55:12.946Z
tags: 
editor: markdown
dateCreated: 2023-02-11T04:55:11.371Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux System Startup and Initialization***English** document is available*](/en/Knowledge-base/Linux/linux-system-startup-and-initialization)
{.links-list}


# Arranque e inicialización del sistema Linux

Cada vez que se inicia un sistema Linux, se inician una serie de procesos para inicializar el sistema. Este proceso se conoce como inicio o inicialización del sistema y, por lo general, ocurre en el siguiente orden:

1. ** BIOS **
2. ** Registro de arranque maestro (MBR)**
3. ** Cargador de arranque **
4. ** Núcleo **
5. ** Proceso de inicio **
6. ** Espacio de usuario **

## BIOS

El Sistema básico de entrada/salida (BIOS) es lo primero que se ejecuta cuando se enciende una computadora. Es responsable de iniciar la computadora leyendo el sector de inicio del disco duro, que contiene el cargador de inicio.

## Registro de arranque maestro (MBR)

El MBR es un pequeño fragmento de código que se encarga de cargar el gestor de arranque. Por lo general, se encuentra en el primer sector del disco duro.

## Cargador de arranque

El cargador de arranque es un programa que se encarga de cargar el kernel del sistema operativo. El cargador de arranque más común que se usa en los sistemas Linux es GRUB (Grand Unified Bootloader).

## Núcleo

El kernel es el núcleo del sistema operativo y es responsable de administrar los recursos del sistema, como la memoria, los dispositivos y los procesos.

## Proceso de inicio

El proceso init es el primer proceso que inicia el kernel. Es responsable de iniciar todos los demás procesos en el sistema.

## Espacio de usuario

Después de que el proceso de inicio haya iniciado todos los demás procesos necesarios, se dice que el sistema está en el espacio del usuario. Aquí es donde los usuarios normales pueden iniciar sesión y ejecutar programas.