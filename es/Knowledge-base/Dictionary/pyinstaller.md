---
title: PyInstaller
description: 
published: true
date: 2023-02-07T04:19:01.736Z
tags: 
editor: markdown
dateCreated: 2023-02-07T04:18:59.650Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [PyInstaller***English** document is available*](/en/Knowledge-base/Dictionary/pyinstaller)
{.links-list}


# Descripción general
PyInstaller es un programa que empaqueta programas de Python en ejecutables independientes, en Windows, Mac y Linux. Está diseñado para ser utilizado por desarrolladores de Python que necesitan distribuir sus aplicaciones a usuarios que pueden o no tener Python instalado.

# Descripción
PyInstaller es una herramienta gratuita y de código abierto para convertir programas de Python en ejecutables independientes. Está diseñado para ser utilizado por desarrolladores de Python que necesitan distribuir sus aplicaciones a usuarios que pueden o no tener Python instalado. El programa funciona analizando el programa Python y recopilando los archivos y bibliotecas necesarios para ejecutarlo. Luego empaqueta estos archivos en un solo archivo ejecutable que se puede ejecutar en cualquier máquina, independientemente de si Python está instalado o no.

PyInstaller es compatible con Python 2.7, 3.4, 3.5, 3.6 y 3.7 y puede empaquetar aplicaciones para Windows, Mac y Linux. También puede empaquetar programas de Python como ejecutables de un solo archivo, lo que puede ser útil para distribuir aplicaciones sin revelar el código fuente.

# Historia
PyInstaller se lanzó por primera vez en 2005 y actualmente lo mantiene un equipo de voluntarios. Ha experimentado un crecimiento constante en popularidad desde su lanzamiento inicial, con más de 2 millones de descargas a partir de 2020.

# Características
PyInstaller tiene una serie de funciones que lo hacen útil para los desarrolladores de Python. Éstas incluyen:

- Soporte para múltiples plataformas: PyInstaller puede empaquetar aplicaciones para Windows, Mac y Linux.
- Ejecutables de un solo archivo: PyInstaller puede empaquetar programas de Python como ejecutables de un solo archivo, lo que puede ser útil para distribuir aplicaciones sin revelar el código fuente.
- Detección automática de dependencias: PyInstaller detecta y empaqueta automáticamente los archivos y bibliotecas necesarios para ejecutar un programa de Python.
- Intérprete de Python incluido: PyInstaller puede incluir un intérprete de Python con la aplicación, lo que le permite ejecutarse en máquinas sin Python instalado.

# Ejemplo
En este ejemplo, usaremos PyInstaller para empaquetar un programa Python simple en un ejecutable independiente. El programa imprime la cadena "¡Hola, mundo!" a la consola

Primero, creamos un archivo llamado "hello.py" con los siguientes contenidos:

```
print("Hello, world!")
```

A continuación, ejecutamos el siguiente comando para empaquetar el programa en un ejecutable independiente:

```
pyinstaller hello.py
```

PyInstaller creará una carpeta llamada "dist" que contiene el archivo ejecutable. Este archivo se puede ejecutar en cualquier máquina, independientemente de si Python está instalado o no.

# Pros y contras
ventajas

- Fácil de usar: PyInstaller es fácil de usar y requiere una configuración mínima.
- Multiplataforma: PyInstaller puede empaquetar aplicaciones para Windows, Mac y Linux.
- Ejecutables de un solo archivo: PyInstaller puede empaquetar programas de Python como ejecutables de un solo archivo, lo que puede ser útil para distribuir aplicaciones sin revelar el código fuente.

Contras

- Soporte limitado: PyInstaller solo es compatible con Python 2.7, 3.4, 3.5, 3.6 y 3.7.
- Sin GUI: PyInstaller no tiene una GUI, por lo que debe usarse desde la línea de comandos.

# Tecnología relacionada
PyOxidizer es otra herramienta para empaquetar programas de Python en ejecutables independientes. Está diseñado para ser más robusto y rico en funciones que PyInstaller, pero aún está en desarrollo temprano.