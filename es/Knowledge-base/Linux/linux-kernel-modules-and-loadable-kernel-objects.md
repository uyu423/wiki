---
title: Módulos del kernel de Linux y objetos del kernel cargables
description: 
published: true
date: 2023-02-11T16:32:20.323Z
tags: 
editor: markdown
dateCreated: 2023-02-11T16:32:18.724Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Kernel Modules and Loadable Kernel Objects***English** document is available*](/en/Knowledge-base/Linux/linux-kernel-modules-and-loadable-kernel-objects)
{.links-list}


# Módulos del kernel de Linux y objetos del kernel cargables

## Descripción general

Un módulo del kernel de Linux es una pieza de código objeto que se puede cargar en el kernel en tiempo de ejecución, sin volver a compilar el kernel.

Los módulos de kernel cargables proporcionan un mecanismo para ampliar la funcionalidad del kernel sin necesidad de volver a compilar el kernel o reiniciar el sistema.

 Los módulos del kernel se pueden usar para agregar controladores de dispositivos, sistemas de archivos y otras funciones al kernel.

## Tipos de módulos del núcleo

Hay dos tipos de módulos del núcleo:

1. **Módulos del kernel cargables**: estos son módulos que se pueden cargar y descargar del kernel según sea necesario.
2. **Módulos del núcleo compilados estáticamente**: estos son módulos que se compilan en el propio núcleo.

## Ventajas de los módulos del kernel cargables

Los módulos de kernel cargables tienen una serie de ventajas sobre los módulos de kernel compilados estáticamente:

1. Se pueden cargar y descargar del kernel según sea necesario, sin necesidad de reiniciar el sistema.
2. Se pueden usar para agregar o eliminar funciones del kernel sin necesidad de volver a compilar el kernel.
3. Proporcionan un mecanismo para ampliar la funcionalidad del kernel sin necesidad de volver a compilar el kernel o reiniciar el sistema.

## Desventajas de los módulos del kernel cargables

Los módulos de kernel cargables tienen una serie de desventajas sobre los módulos de kernel compilados estáticamente:

1. Pueden introducir vulnerabilidades de seguridad si no se diseñan e implementan correctamente.
2. Pueden ser difíciles de depurar y solucionar.
3. Pueden ser difíciles de mantener y actualizar.

## Carga y descarga del módulo del kernel

Un módulo del kernel se puede cargar en el kernel usando el comando `insmod` y descargarlo del kernel usando el comando `rmmod`.

El comando `insmod` toma el nombre del módulo del kernel como argumento y lo carga en el kernel. El comando `rmmod` toma el nombre del módulo del núcleo como argumento y lo elimina del núcleo.

## Creación de un módulo del núcleo

Un módulo del kernel es una pieza de código objeto que se puede cargar en el kernel en tiempo de ejecución, sin volver a compilar el kernel. Los módulos del kernel generalmente se escriben en el lenguaje de programación C.

Los módulos del núcleo deben compilarse con el indicador de compilación `-DMODULE`. Esta bandera le dice al compilador que el código se está compilando como un módulo del kernel.

Los módulos del núcleo también se deben compilar con el indicador de compilación `-fPIC`. Esta bandera le dice al compilador que genere código independiente de la posición. El código independiente de la posición puede cargarse en la memoria en cualquier dirección y ejecutarse.

Los indicadores del compilador `-DMODULE` y `-fPIC` se pueden pasar al compilador usando la variable de entorno `CFLAGS`.

```
$ export CFLAGS=-DMODULE -fPIC
```

Una vez que se ha configurado la variable de entorno `CFLAGS`, el módulo del kernel se puede compilar usando el comando `make`.

```
$ make
```

## Cargando un Módulo del Kernel

Un módulo del kernel se puede cargar en el kernel usando el comando `insmod`. El comando `insmod` toma el nombre del módulo del kernel como argumento y lo carga en el kernel.

```
$ insmod hello.ko
```

## Descarga de un módulo del núcleo

Un módulo del kernel se puede descargar del kernel usando el comando `rmmod`. El comando `rmmod` toma el nombre del módulo del núcleo como argumento y lo elimina del núcleo.

```
$ rmmod hello
```

## Referencias

https://www.kernel.org/doc/Documentation/kmod/modules.txt
https://www.ibm.com/support/knowledgecenter/ssw_aix_71/com.ibm.aix.kernel/loadable_kernel_modules.htm
https://www.ibm.com/support/knowledgecenter/ssw_aix_71/com.ibm.aix.kernel/creating_kernel_modules.htm
https://www.ibm.com/support/knowledgecenter/ssw_aix_71/com.ibm.aix.kernel/loading_unloading_kernel_modules.htm