---
title: Web Assembly
description: 
published: true
date: 2023-02-12T04:56:23.632Z
tags: 
editor: markdown
dateCreated: 2023-02-12T04:56:15.922Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Web Assembly***English** document is available*](/en/Knowledge-base/Dictionary/web-assembly)
{.links-list}


# Descripción general

Web Assembly (WASM) es un nuevo formato de instrucción binaria para una máquina virtual basada en pila. Está diseñado para ser un objetivo de compilación portátil, de tamaño y tiempo de carga eficiente para lenguajes de programación, lo que permite la implementación en la web para aplicaciones de servidor y cliente.

# Descripción

Web Assembly (WASM) es un lenguaje similar a un ensamblador de bajo nivel que está diseñado para ser un objetivo de compilación para lenguajes de programación como C, C++, Rust y otros. Es un formato de instrucción binaria que está diseñado para ser eficiente en términos de tamaño, tiempo de carga y tiempo de ejecución. WASM está diseñado para ser un destino portátil para la compilación de lenguajes de alto nivel, lo que les permite implementarse en la web para aplicaciones tanto del lado del cliente como del lado del servidor.

WASM está diseñado para ser un entorno de ejecución seguro y aislado, lo que permite que el código se ejecute en la web sin comprometer la seguridad del usuario. También proporciona una forma de ejecutar código en la web que es más eficiente que JavaScript, lo que permite un mejor rendimiento y tiempos de carga más rápidos.

El código WASM se compila con anticipación (AOT) en un formato binario, que luego se carga y ejecuta en una máquina virtual. Esta máquina virtual se puede integrar en un navegador web o se puede implementar como una aplicación independiente.

# Historia

Web Assembly fue anunciado por primera vez en 2015 por el World Wide Web Consortium (W3C) como parte del esfuerzo por crear una nueva plataforma web. La versión inicial del lenguaje se lanzó en 2017 y desde entonces ha visto varias actualizaciones.

# Características

WASM proporciona una serie de funciones que lo convierten en un objetivo de compilación atractivo para aplicaciones web.

- Es un lenguaje ensamblador de bajo nivel que está diseñado para ser eficiente en términos de tamaño, tiempo de carga y tiempo de ejecución.
- Es un entorno de ejecución seguro y aislado que permite que el código se ejecute en la web sin comprometer la seguridad del usuario.
- Proporciona una forma de ejecutar código en la web que es más eficiente que JavaScript, lo que permite un mejor rendimiento y tiempos de carga más rápidos.
- Está diseñado para ser un objetivo portátil para la compilación de lenguajes de alto nivel, lo que les permite implementarse en la web para aplicaciones tanto del lado del cliente como del lado del servidor.

# Ejemplo

El siguiente es un ejemplo de un programa simple escrito en C y compilado en WASM:

```C
#include <stdio.h>

int main() {
  printf("Hello, World!\n");
  return 0;
}
```

Este programa se puede compilar a WASM utilizando una herramienta como Emscripten:

```
emcc hello.c -o hello.wasm
```

Esto producirá un binario WASM, que luego puede ser cargado y ejecutado por una máquina virtual WASM.

# Pros y contras

WASM tiene una serie de ventajas sobre otras tecnologías web:

- Es un entorno de ejecución seguro y aislado que permite que el código se ejecute en la web sin comprometer la seguridad del usuario.
- Proporciona una forma de ejecutar código en la web que es más eficiente que JavaScript, lo que permite un mejor rendimiento y tiempos de carga más rápidos.
- Está diseñado para ser un objetivo portátil para la compilación de lenguajes de alto nivel, lo que les permite implementarse en la web para aplicaciones tanto del lado del cliente como del lado del servidor.

Sin embargo, también hay algunas desventajas al usar WASM:

- Es una tecnología relativamente nueva y aún está en desarrollo, por lo que puede haber errores o problemas de compatibilidad.
- No es tan ampliamente compatible como otras tecnologías web, por lo que es posible que no todos los navegadores lo admitan.
- No es tan fácil de depurar como otras tecnologías web, por lo que puede ser difícil solucionar problemas.

# Tecnología relacionada

WASM está relacionado con otras tecnologías web como JavaScript y WebGL. JavaScript es un lenguaje de secuencias de comandos que se utiliza para crear páginas web dinámicas, mientras que WebGL es una API de gráficos que permite gráficos 3D acelerados por hardware en navegadores web.

# Digresión

WASM es una tecnología nueva y emocionante que tiene el potencial de revolucionar la forma en que se desarrollan las aplicaciones web. Proporciona una forma de ejecutar código en la web que es más eficiente que JavaScript, lo que permite un mejor rendimiento y tiempos de carga más rápidos. También está diseñado para ser un entorno de ejecución seguro y aislado, lo que permite que el código se ejecute en la web sin comprometer la seguridad del usuario.