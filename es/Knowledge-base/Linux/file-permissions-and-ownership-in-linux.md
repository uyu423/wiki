---
title: Permisos de archivo y propiedad en Linux
description: 
published: true
date: 2023-02-11T08:32:24.963Z
tags: 
editor: markdown
dateCreated: 2023-02-11T08:32:23.261Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [File Permissions and Ownership in Linux***English** document is available*](/en/Knowledge-base/Linux/file-permissions-and-ownership-in-linux)
{.links-list}


# Permisos de archivo y propiedad en Linux

En cualquier sistema Linux, los permisos y la propiedad de los archivos son muy importantes para garantizar que se acceda a los archivos y se utilicen de la manera que desee. En este artículo, veremos qué son los permisos y la propiedad de los archivos, cómo funcionan y algunos escenarios comunes en los que podría necesitar usarlos.

## ¿Qué son los permisos y la propiedad de los archivos?

Los permisos de archivo son configuraciones que determinan quién puede leer, escribir o ejecutar un archivo en particular. La propiedad del archivo determina quién tiene control sobre un archivo y puede cambiar sus permisos.

En Linux, cada archivo tiene dos conjuntos de permisos:
- Los permisos para el propietario del archivo.
- Los permisos para todos los demás.

Puede ver los permisos de un archivo usando el comando `ls -l`. Esto dará una salida que se parece a esto:

```
-rw-r--r-- 1 root root 696 Apr 3 12:34 somefile
```

La primera columna muestra los permisos del propietario, la segunda columna muestra los permisos de todos los demás y la tercera y cuarta columnas muestran el propietario del archivo y el grupo, respectivamente.

Los permisos están representados por una serie de letras: `r`, `w` y `x`.
- `r` significa leer y significa que el archivo se puede leer
- `w` significa escribir y significa que el archivo se puede escribir en
- `x` significa ejecutar y significa que el archivo se puede ejecutar como un programa

Si no se establece un permiso, se representa con un `-`. Por ejemplo, la salida `ls -l` anterior muestra que el propietario tiene permisos de lectura y escritura, pero no permisos de ejecución, mientras que todos los demás solo tienen permisos de lectura.

## ¿Cómo funcionan los permisos y la propiedad de los archivos?

El propietario del archivo es el usuario que creó el archivo. El grupo de archivos es una colección de usuarios que tienen acceso al archivo. De forma predeterminada, el grupo de archivos suele ser el mismo que el propietario del archivo, pero se puede cambiar.

Cada archivo también tiene un conjunto de permisos que determinan quién puede leerlo, escribirlo o ejecutarlo. Estos permisos pueden ser modificados por el propietario del archivo o por un usuario con privilegios de root.

Para cambiar el propietario del archivo, puede usar el comando `chown`. Por ejemplo, para cambiar el propietario de un archivo llamado `somefile` al usuario `jane`, usaría el comando `chown jane somefile`.

Para cambiar el grupo de archivos, puede usar el comando `chgrp`. Por ejemplo, para cambiar el grupo de un archivo llamado `algúnarchivo` al grupo `usuarios`, usaría el comando `chgrp usuarios algúnarchivo`.

Para cambiar los permisos del archivo, puede usar el comando `chmod`. Hay dos formas de usar este comando:
- Con números
- Con letras

Los números representan los permisos para el propietario, el grupo y todos los demás, respectivamente. Las letras representan lo mismo pero son más fáciles de usar.

Por ejemplo, para dar al propietario permisos de lectura, escritura y ejecución, al grupo permisos de lectura y ejecución, y a todos los demás permisos de lectura, usaría el comando `chmod 751 somefile`.

También puede usar letras para representar los permisos. Para dar al propietario permisos de lectura, escritura y ejecución, al grupo permisos de lectura y ejecución, y a todos los demás permisos de lectura, usaría el comando `chmod u=rwx,g=rx,o=r somefile`.

## Escenarios en los que podría necesitar usar permisos y propiedad de archivos

Hay algunos escenarios comunes en los que es posible que deba usar los permisos y la propiedad de los archivos:

### Cuando desee permitir que otros usuarios accedan a sus archivos

Si desea permitir que otros usuarios del mismo sistema accedan a sus archivos, deberá establecer los permisos adecuados. Por ejemplo, si desea permitir que otros usuarios lean y escriban en un archivo llamado `somefile`, usaría el comando `chmod 664 somefile`.

### Cuando desee evitar que otros usuarios accedan a sus archivos

Si desea evitar que otros usuarios del mismo sistema accedan a sus archivos, deberá establecer los permisos adecuados. Por ejemplo, si desea evitar que otros usuarios lean un archivo llamado `somefile`, usaría el comando `chmod 600 somefile`.

### Cuando desee permitir que los usuarios de otros sistemas accedan a sus archivos

Si desea permitir que los usuarios de otros sistemas accedan a sus archivos, deberá establecer los permisos adecuados. Por ejemplo, si desea permitir que los usuarios de otros sistemas lean y escriban en un archivo llamado `somefile`, usaría el comando `chmod 666 somefile`.

### Cuando desee evitar que los usuarios de otros sistemas accedan a sus archivos

Si desea evitar que los usuarios de otros sistemas accedan a sus archivos, deberá establecer los permisos adecuados. Por ejemplo, si desea evitar que los usuarios de otros sistemas lean un archivo llamado `somefile`, usaría el comando `chmod 400 somefile`.

## Conclusión

En este artículo, hemos analizado qué son los permisos y la propiedad de los archivos, cómo funcionan y algunos escenarios comunes en los que podría necesitar usarlos. Los permisos y la propiedad de los archivos son importantes en cualquier sistema Linux para garantizar que se acceda a los archivos y se utilicen de la manera que desee.