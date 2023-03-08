---
title: Comprender el sistema de archivos de Linux
description: 
published: true
date: 2023-02-11T05:32:25.166Z
tags: 
editor: markdown
dateCreated: 2023-02-11T05:32:23.626Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Understanding the Linux File System***English** document is available*](/en/Knowledge-base/Linux/understanding-the-linux-file-system)
{.links-list}


# Comprender el sistema de archivos de Linux

El sistema de archivos de Linux es un sistema de archivos jerárquico. Está organizado en una estructura similar a un árbol, con un directorio raíz (/) en la parte superior y subdirectorios debajo. Los subdirectorios se pueden dividir en subdirectorios, y así sucesivamente.

El sistema de archivos de Linux está diseñado para ser eficiente y fácil de usar. Está organizado para que las tareas comunes se puedan realizar con unos pocos comandos simples. Por ejemplo, el comando ls enumera el contenido de un directorio y el comando cd cambia el directorio actual.

El sistema de archivos también está diseñado para ser seguro. se pueden establecer permisos en archivos y directorios para que solo los usuarios autorizados puedan acceder a ellos.

El sistema de archivos de Linux se divide en varias partes:

- El **directorio raíz** (/), que es el directorio de nivel superior en el sistema de archivos.
- El **directorio de inicio** (~), que es el directorio donde cada usuario tiene sus propios archivos y configuraciones personales.
- El **directorio de inicio** (/boot), que contiene los archivos necesarios para iniciar el sistema.
- El directorio **etc** (/etc), que contiene archivos de configuración de todo el sistema.
- El directorio **var** (/var), que contiene archivos que cambian con frecuencia, como los archivos de registro.

Hay otros directorios importantes, pero estos son los más importantes para comprender el sistema de archivos.

## El directorio raíz

El directorio raíz es el directorio de nivel superior en el sistema de archivos. Se denota con una barra diagonal (/).

El directorio raíz contiene todos los demás directorios del sistema de archivos. Es el punto de partida para todas las rutas de archivos.

## El directorio de inicio

El directorio de inicio es el directorio donde cada usuario tiene sus propios archivos y configuraciones personales. Se denota con una tilde (~).

Por ejemplo, el directorio de inicio del usuario "jane" sería /home/jane.

El directorio de inicio generalmente se encuentra en la misma partición que el directorio raíz, pero no tiene por qué ser así.

## El directorio de inicio

El directorio de inicio contiene los archivos necesarios para iniciar el sistema. Se denota por /boot.

El directorio de inicio normalmente contiene el kernel (el núcleo del sistema operativo) y el disco RAM inicial.

## El Directorio Etc.

El directorio etc contiene archivos de configuración de todo el sistema. Se denota por /etc.

El directorio etc normalmente contiene archivos que son necesarios para que el sistema funcione, como el archivo de contraseña y el archivo de registro del sistema.

## El Directorio Var

El directorio var contiene archivos que cambian con frecuencia, como archivos de registro. Se denota por /var.

El directorio var generalmente se usa para archivos que se crean y eliminan con frecuencia, como los archivos de registro del servidor web.

## Conclusión

Este artículo ha proporcionado una introducción al sistema de archivos de Linux. Ha descrito el propósito del directorio raíz, el directorio de inicio, el directorio de inicio, el directorio etc y el directorio var.