---
title: Memoria virtual e intercambio de Linux
description: 
published: true
date: 2023-02-11T15:33:01.732Z
tags: 
editor: markdown
dateCreated: 2023-02-11T15:32:54.637Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Virtual Memory and Swapping***English** document is available*](/en/Knowledge-base/Linux/linux-virtual-memory-and-swapping)
{.links-list}


# Memoria virtual e intercambio de Linux

La memoria virtual es una técnica que permite que un sistema utilice más memoria de la que está físicamente disponible en forma de RAM mediante el uso del disco duro como almacenamiento temporal. Esto permite ejecutar más programas al mismo tiempo y puede mejorar el rendimiento.

El intercambio es el proceso de mover datos de la RAM al disco duro y viceversa según sea necesario. Cuando un sistema tiene poca RAM, el núcleo comenzará a intercambiar datos en el disco duro para liberar memoria. Esto puede hacer que el sistema se ralentice ya que el disco duro es mucho más lento que la RAM.

## ¿Qué es la memoria virtual?

La memoria virtual es una técnica que permite que un sistema utilice más memoria de la que está físicamente disponible en forma de RAM mediante el uso del disco duro como almacenamiento temporal. Esto permite ejecutar más programas al mismo tiempo y puede mejorar el rendimiento.

Cuando se inicia un programa, el sistema operativo asigna una cierta cantidad de memoria para su uso. Esta memoria se utiliza para el código y los datos del programa. Si el programa intenta utilizar más memoria de la asignada, se producirá un error.

La memoria virtual permite que el sistema operativo asigne más memoria a un programa de la que está físicamente disponible. Cuando el programa intente acceder a esta memoria adicional, el sistema operativo copiará de forma transparente los datos necesarios del disco duro a la RAM. Este proceso se conoce como intercambio.

El intercambio es el proceso de mover datos de la RAM al disco duro y viceversa según sea necesario. Cuando un sistema tiene poca RAM, el núcleo comenzará a intercambiar datos en el disco duro para liberar memoria. Esto puede hacer que el sistema se ralentice ya que el disco duro es mucho más lento que la RAM.

Linux usa una técnica llamada demanda de paginación para la memoria virtual. Esto significa que los datos solo se copian del disco duro a la RAM cuando se necesitan. Esto contrasta con técnicas como la paginación previa, en la que los datos se copian del disco duro a la RAM, incluso si no son necesarios.

La paginación por demanda es más eficiente ya que solo copia los datos que realmente se necesitan. Sin embargo, puede hacer que el sistema se ralentice si se necesitan muchos datos y aún no están en la RAM.

## Ventajas de la memoria virtual

La memoria virtual tiene varias ventajas sobre la memoria física:

* Se pueden ejecutar más programas al mismo tiempo ya que cada programa usa menos memoria.

* El sistema operativo puede usar el espacio en disco de manera más eficiente ya que no necesita asignar un bloque de memoria contiguo para cada programa.

* El sistema operativo puede evitar copiar datos hacia y desde el disco duro con tanta frecuencia como lo haría si los datos no estuvieran en la memoria virtual.

* La memoria virtual permite que el sistema operativo proteja el espacio de direcciones de cada programa de otros programas. Esto se conoce como protección de direcciones de memoria.

## Desventajas de la memoria virtual

La memoria virtual también tiene algunas desventajas:

* El sistema se ralentizará a medida que los datos se copien hacia y desde el disco duro.

* El disco duro es mucho más lento que la RAM, por lo que el sistema no podrá ejecutarse tan rápido como si todos los datos estuvieran en la RAM.

* El disco duro puede llenarse rápidamente si el sistema usa mucha memoria virtual.

## Configuración de la memoria virtual

Linux usa un programa llamado `swap` para administrar la memoria virtual. El programa `swap` es responsable de asignar espacio en el disco duro para la memoria virtual y de copiar datos hacia y desde el disco duro según sea necesario.

El programa `swap` se configura utilizando el archivo `/etc/fstab`. Este archivo contiene una lista de todas las particiones del disco duro y otra información sobre ellas. El programa `swap` buscará una línea en este archivo que comience con `/swap` y usará la partición listada allí para la memoria virtual.

Aquí hay un archivo `/etc/fstab` de ejemplo:

    /dev/sda1 /boot ext4 por defecto 0 2
    /dev/sda2 / ext4 por defecto 0 1
    /dev/sda3 intercambiar valores predeterminados de intercambio 0 0

En este ejemplo, la partición `/dev/sda3` se usa para la memoria virtual.

El archivo `/etc/fstab` también se puede usar para configurar otras opciones para el programa `swap`. Por ejemplo, la opción `swappiness` se puede utilizar para controlar la frecuencia con la que el programa `swap` copiará datos hacia y desde el disco duro.

La opción `swappiness` es un número entre 0 y 100 que controla la frecuencia con la que el programa `swap` copiará datos hacia y desde el disco duro. Un valor de 0 significa que el programa `swap` solo copiará datos al disco duro cuando el sistema tenga poca memoria. Un valor de 100 significa que el programa `swap` copiará datos al disco duro incluso si el sistema no tiene poca memoria.

El valor predeterminado para `swappiness` es 60. Esto significa que el programa `swap` comenzará a copiar datos en el disco duro cuando el sistema tenga libre el 60% de su RAM.

## Conclusión

La memoria virtual es una técnica que permite que un sistema utilice más memoria de la que está físicamente disponible en forma de RAM mediante el uso del disco duro como almacenamiento temporal. Esto permite ejecutar más programas al mismo tiempo y puede mejorar el rendimiento.

El intercambio es el proceso de mover datos de la RAM al disco duro y viceversa según sea necesario. Cuando un sistema tiene poca RAM, el kernel comenzará a intercambiar datos en el disco duro para liberar memoria. Esto puede hacer que el sistema se ralentice ya que el disco duro es mucho más lento que la RAM.

 Linux usa una técnica llamada demanda de paginación para la memoria virtual. Esto significa que los datos solo se copian del disco duro a la RAM cuando se necesitan. Esto contrasta con técnicas como la paginación previa, en la que los datos se copian del disco duro a la RAM, incluso si no son necesarios.

La paginación por demanda es más eficiente ya que solo copia los datos que realmente se necesitan. Sin embargo, puede hacer que el sistema se ralentice si se necesitan muchos datos y aún no están en la RAM.

El programa `swap` es responsable de asignar espacio en el disco duro para la memoria virtual y de copiar datos hacia y desde el disco duro según sea necesario. El programa `swap` se configura utilizando el archivo `/etc/fstab`. Este archivo contiene una lista de todas las particiones del disco duro y otra información sobre ellas. El programa `swap` buscará una línea en este archivo que comience con `/swap` y usará la partición listada allí para la memoria virtual.

La opción `swappiness` es un número entre 0 y 100 que controla la frecuencia con la que el programa `swap` copiará datos hacia y desde el disco duro. Un valor de 0 significa que el programa `swap` solo copiará datos al disco duro cuando el sistema tenga poca memoria. Un valor de 100 significa que el programa `swap` copiará datos al disco duro incluso si el sistema no tiene poca memoria.

## Referencias

* [https://www.geeksforgeeks.org/virtual-memory-in-operating-system/](https://www.geeksforgeeks.org/virtual-memory-in-operating-system/)

* [https://www.geeksforgeeks.org/paginación-en-sistemas-operativos/](https://www.geeksforgeeks.org/paginación-en-sistemas-operativos/)

* [https://www.redhat.com/sysadmin/linux-swap-space](https://www.redhat.com/sysadmin/linux-swap-space)

* [https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-18-04](https://www.digitalocean.com/community/tutorials/how -para-agregar-intercambiar-espacio-en-ubuntu-18-04)