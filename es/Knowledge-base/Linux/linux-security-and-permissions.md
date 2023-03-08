---
title: Seguridad y permisos de Linux
description: 
published: true
date: 2023-02-11T20:32:36.500Z
tags: 
editor: markdown
dateCreated: 2023-02-11T20:32:29.519Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Security and Permissions***English** document is available*](/en/Knowledge-base/Linux/linux-security-and-permissions)
{.links-list}


# Seguridad y permisos de Linux

Una de las grandes ventajas de Linux es su seguridad. Linux es muy seguro por defecto, pero todavía hay formas de hacerlo más seguro. En este artículo, veremos algunas de las formas en que puede mejorar la seguridad de su sistema Linux.

## Permisos de archivo

Uno de los aspectos más importantes de la seguridad son los permisos de archivos. Los permisos de archivo determinan quién puede leer, escribir y ejecutar un archivo. De forma predeterminada, solo el propietario de un archivo puede leerlo, escribirlo y ejecutarlo. Otros solo pueden leerlo y ejecutarlo.

Para ver los permisos de un archivo, use el comando `ls` con la opción `-l`:

    $ ls-l
    -rw-r--r-- 1 john john 0 25 de abril 18:42 file1

La primera columna muestra los permisos del archivo. La siguiente columna muestra el propietario del archivo. La tercera columna muestra el grupo al que pertenece el archivo. La cuarta columna muestra el tamaño del archivo en bytes. La quinta columna muestra la fecha y la hora en que se modificó por última vez el archivo. La sexta columna muestra el nombre del archivo.

Los permisos se muestran como una serie de caracteres. El primer carácter es `-` para un archivo normal, `d` para un directorio o `l` para un enlace simbólico. Los nueve caracteres siguientes se dividen en tres grupos de tres. El primer grupo son los permisos del propietario, el segundo grupo son los permisos del grupo y el tercer grupo son los permisos de los demás.

Cada grupo de tres caracteres consta de una `r` para leer, `w` para escribir, `x` para ejecutar o `-` para no tener permiso. Por ejemplo, los permisos `rwxr-xr-x` significan que el propietario puede leer, escribir y ejecutar el archivo; el grupo puede leer y ejecutar el archivo; y otros pueden leer y ejecutar el archivo.

Para cambiar los permisos de un archivo, use el comando `chmod`. Por ejemplo, para otorgar al propietario permisos de lectura, escritura y ejecución, y otorgar al grupo y a otros permisos de lectura y ejecución, usaría el siguiente comando:

    $ chmod 755 archivo1

El comando `chmod` también se puede usar para cambiar el propietario y el grupo de un archivo. Por ejemplo, para cambiar el propietario de un archivo a `john` y el grupo a `users`, usaría el siguiente comando:

    $ chmod u+rwx,g+rwx,o+rwx archivo1

## Cuentas de usuario

Otro aspecto importante de la seguridad son las cuentas de usuario. De forma predeterminada, los sistemas Linux tienen un usuario raíz y algunos otros usuarios predeterminados. El usuario root tiene acceso completo al sistema y puede hacer cualquier cosa. Los otros usuarios tienen acceso limitado y solo pueden hacer ciertas cosas.

Es una buena idea crear una cuenta de usuario separada para cada persona que use el sistema. De esa manera, si la cuenta de una persona se ve comprometida, las otras cuentas seguirán estando seguras.

Para crear una cuenta de usuario, use el comando `adduser`. Por ejemplo, para crear una cuenta de usuario para `john`, usaría el siguiente comando:

    $ añadir usuario john

Para dar a un usuario acceso sudo, lo que le permite ejecutar comandos con privilegios de root, use el comando `usermod`. Por ejemplo, para dar acceso sudo a `john`, usaría el siguiente comando:

    $ modusuario -aG sudo john

## Cortafuegos

Otra forma de mejorar la seguridad de su sistema Linux es instalar un firewall. Un firewall es un programa que controla el tráfico entrante y saliente en una red.

Los sistemas Linux tienen un cortafuegos incorporado llamado `iptables`. Para instalar `iptables`, use el comando `apt-get`:

    $ sudo apt-get install iptables

Para configurar `iptables`, edite el archivo `/etc/iptables.conf`. Por ejemplo, para permitir el tráfico entrante en el puerto 80 (para HTTP), agregaría la siguiente línea al archivo `/etc/iptables.conf`:

    -A ENTRADA -p tcp --dport 80 -j ACEPTAR

Para guardar los cambios, use el comando `iptables-save`:

    $ sudo iptables-guardar

## Conclusión

En este artículo, hemos analizado algunas de las formas en que puede mejorar la seguridad de su sistema Linux. De forma predeterminada, Linux es muy seguro, pero todavía hay formas de hacerlo más seguro. Al usar las técnicas descritas en este artículo, puede hacer que su sistema Linux sea aún más seguro.