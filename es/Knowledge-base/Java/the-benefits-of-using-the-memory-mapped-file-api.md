---
title: Los beneficios de usar la API de archivos asignados a la memoria
description: 
published: true
date: 2023-02-09T10:55:51.619Z
tags: 
editor: markdown
dateCreated: 2023-02-09T10:55:45.587Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [The Benefits of Using the Memory Mapped File API***English** document is available*](/en/Knowledge-base/Java/the-benefits-of-using-the-memory-mapped-file-api)
{.links-list}


# Introducción

Los archivos asignados a la memoria son una herramienta poderosa para optimizar el rendimiento de E/S de archivos en las aplicaciones. Se pueden utilizar para mejorar el rendimiento de las operaciones de lectura y escritura al eliminar la necesidad de costosas llamadas al sistema. Además, los archivos asignados a la memoria se pueden usar para compartir fácilmente datos entre procesos, lo que puede ser útil para crear aplicaciones distribuidas.

A pesar de los beneficios de usar archivos mapeados en memoria, hay algunos inconvenientes a tener en cuenta. Una posible desventaja es que los archivos asignados a la memoria pueden usar mucha memoria, por lo que es posible que no sean adecuados para aplicaciones con recursos limitados. Además, los archivos mapeados en memoria pueden ser complicados para trabajar y es posible que no funcionen bien en todas las plataformas.

En este artículo, veremos más de cerca las ventajas y desventajas de usar archivos mapeados en memoria. También proporcionaremos algunos consejos prácticos para trabajar con archivos mapeados en memoria en sus aplicaciones.

# ¿Qué son los archivos asignados a la memoria?

Un archivo asignado a la memoria es un archivo que está asignado a la memoria, lo que significa que la aplicación puede acceder directamente a él sin pasar por el sistema operativo. Esto permite una E/S de archivo muy rápida porque la aplicación puede evitar la sobrecarga de hacer llamadas al sistema.

Los archivos mapeados en memoria se pueden usar tanto para leer como para escribir datos. Al leer datos de un archivo asignado a la memoria, la aplicación simplemente lee los datos de la memoria. Esto es mucho más rápido que hacer una llamada al sistema para leer los datos del archivo.

Escribir datos en un archivo mapeado en memoria es un poco más complicado. La aplicación primero tiene que escribir los datos en un búfer temporal. Una vez que los datos están en el búfer, la aplicación puede copiarlos en el archivo asignado a la memoria. Esto puede parecer más lento que simplemente escribir los datos directamente en el archivo, pero en realidad puede ser más rápido porque el sistema operativo puede optimizar la operación de copia.

# Los beneficios de los archivos asignados a la memoria

Hay varios beneficios al usar archivos mapeados en memoria en sus aplicaciones.

## E/S de archivo más rápida

Uno de los mayores beneficios de usar archivos mapeados en memoria es que pueden mejorar drásticamente el rendimiento de las operaciones de E/S de archivos. Esto se debe a que la aplicación puede evitar realizar llamadas al sistema, lo que puede ser bastante costoso.

En muchos casos, la mejora del rendimiento puede ser tan significativa que vale la pena usar archivos mapeados en memoria, incluso si requieren un poco más de esfuerzo para configurarlos.

## Fácil de compartir datos entre procesos

Otro beneficio de los archivos mapeados en memoria es que se pueden usar para compartir fácilmente datos entre procesos. Esto se debe a que cualquier proceso que tenga el archivo asignado a la memoria puede acceder a los datos en un archivo asignado a la memoria.

Esto puede ser útil para crear aplicaciones distribuidas. Por ejemplo, podría usar un archivo asignado a la memoria para compartir datos entre un servidor web y un servidor de base de datos.

## Uso de memoria reducido

Los archivos asignados a la memoria también pueden ayudar a reducir el uso de la memoria en sus aplicaciones. Esto se debe a que el sistema operativo puede paginar partes del archivo que no se están utilizando.

La paginación es un proceso en el que el sistema operativo intercambia datos de la memoria al disco cuando no se está utilizando. Esto puede ayudar a liberar memoria para otras aplicaciones.

# Inconvenientes de los archivos asignados a la memoria

También existen algunos inconvenientes en el uso de archivos mapeados en memoria.

## Pueden usar mucha memoria

Una desventaja potencial de los archivos mapeados en memoria es que pueden usar mucha memoria. Esto se debe a que todo el archivo se asigna a la memoria, incluso si solo se utiliza una pequeña parte.

Por este motivo, es posible que los archivos asignados a la memoria no sean adecuados para aplicaciones con recursos limitados.

## Puede ser complicado trabajar con ellos

Otra desventaja potencial de los archivos mapeados en memoria es que puede ser complicado trabajar con ellos. Esto se debe a que la aplicación tiene que administrar la asignación de archivos por sí misma.

 Además, la aplicación debe tener cuidado de desasignar el archivo cuando termine de usarlo. De lo contrario, el archivo permanecerá asignado a la memoria y seguirá consumiendo recursos.

## Es posible que no funcionen bien en todas las plataformas

Finalmente, es importante tener en cuenta que es posible que los archivos asignados a la memoria no funcionen bien en todas las plataformas. Esto se debe a que el sistema operativo debe admitir la función de asignación de archivos.

Además, el sistema de archivos en el que se almacena el archivo también debe admitir archivos asignados a la memoria. No todos los sistemas de archivos lo hacen.

# Conclusión

Los archivos asignados a la memoria son una herramienta poderosa para optimizar el rendimiento de E/S de archivos en las aplicaciones. Se pueden utilizar para mejorar el rendimiento de las operaciones de lectura y escritura al eliminar la necesidad de costosas llamadas al sistema. Además, los archivos asignados a la memoria se pueden usar para compartir fácilmente datos entre procesos, lo que puede ser útil para crear aplicaciones distribuidas.

A pesar de los beneficios de usar archivos mapeados en memoria, hay algunos inconvenientes a tener en cuenta. Una posible desventaja es que los archivos asignados a la memoria pueden usar mucha memoria, por lo que es posible que no sean adecuados para aplicaciones con recursos limitados. Además, los archivos mapeados en memoria pueden ser complicados para trabajar y es posible que no funcionen bien en todas las plataformas.

# Otras lecturas

Si está interesado en obtener más información sobre los archivos asignados a la memoria, hemos compilado una lista de recursos que pueden resultarle útiles.

## Libros

* El manual de mapas de memoria: una guía esencial para dispositivos con mapas de memoria y cómo funcionan por Michael Barr

## Artículos

* [¿Qué son los archivos asignados a la memoria?](https://www.geeksforgeeks.org/memory-mapped-file-operations-c-unix/)
* [Una introducción a la E/S asignada a la memoria] (https://www.ibm.com/developerworks/library/l-memory/)
* [Archivos asignados a la memoria en Windows](https://docs.microsoft.com/en-us/windows/win32/memory/memory-mapped-files)
* [mmap() tiene implicaciones de seguridad](https://lwn.net/Articles/531114/)

## Ejemplos de código

* [Archivos mapeados en memoria en C](https://www.geeksforgeeks.org/memory-mapped-file-operations-c-unix/)
* [Archivos mapeados en memoria en Java](https://www.baeldung.com/java-memory-mapped-file)
* [Archivos mapeados en memoria en Python](https://pymotw.com/2/mmap/)