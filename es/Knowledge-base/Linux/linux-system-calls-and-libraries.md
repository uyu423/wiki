---
title: Llamadas y bibliotecas del sistema Linux
description: 
published: true
date: 2023-02-09T11:17:34.581Z
tags: 
editor: markdown
dateCreated: 2023-02-09T11:17:32.957Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux System Calls and Libraries***English** document is available*](/en/Knowledge-base/Linux/linux-system-calls-and-libraries)
{.links-list}


# Llamadas y bibliotecas del sistema Linux

Las llamadas al sistema son cómo un programa solicita servicios de un sistema operativo. Las bibliotecas son cómo un programa solicita servicios de un lenguaje de programación.

En este artículo, veremos cómo funcionan las llamadas al sistema y las bibliotecas en Linux. Comenzaremos con una breve descripción general de cada uno y luego veremos algunos ejemplos específicos.

## Llamadas al sistema

Las llamadas al sistema son la interfaz entre el espacio del usuario y el espacio del núcleo. Son cómo un programa solicita servicios a un sistema operativo.

Las llamadas al sistema se realizan llamando a una función que tiene un nombre especial. Por ejemplo, en Linux, la llamada al sistema para leer un archivo se llama `read()`.

Las llamadas al sistema se realizan pasando argumentos a la función. El primer argumento es siempre un número que identifica la llamada al sistema. El resto de los argumentos dependen de la llamada al sistema que se realice.

Cuando se realiza una llamada al sistema, el núcleo comprueba si el programa que llama tiene permiso para realizar la llamada. Si se permite la llamada, el kernel ejecuta el código para la llamada al sistema.

El código para una llamada al sistema generalmente se escribe en lenguaje ensamblador. Esto dificulta que los programadores lo entiendan y lo depuren.

Las llamadas al sistema son lentas porque involucran un cambio de contexto entre el espacio del usuario y el espacio del kernel. Un cambio de contexto es cuando la CPU guarda el estado de un proceso y carga el estado de otro proceso.

Las llamadas al sistema también son un riesgo para la seguridad. Una llamada al sistema con errores puede bloquear el kernel o permitir que un usuario malintencionado obtenga acceso a información privilegiada.

## Bibliotecas

Las bibliotecas son una forma para que los programas soliciten servicios de un lenguaje de programación.

Las bibliotecas se componen de una colección de funciones. Cada función realiza una tarea específica.

Por ejemplo, la biblioteca estándar de C proporciona funciones para leer y escribir en archivos, manipular cadenas y realizar operaciones matemáticas.

Las bibliotecas suelen estar escritas en el mismo idioma que los programas que las utilizan. Esto hace que sea más fácil de entender y depurar para los programadores.

Las bibliotecas son más rápidas que las llamadas al sistema porque no implican un cambio de contexto.

Las bibliotecas también son más seguras que las llamadas al sistema porque es menos probable que contengan código defectuoso.

## Ejemplos

Ahora que hemos visto una breve descripción general de las llamadas al sistema y las bibliotecas, veamos algunos ejemplos específicos.

### Lectura de un archivo

Aquí hay un ejemplo de cómo leer de un archivo usando una llamada al sistema:

```c
#include <unistd.h>

int main() {
  char buf[1024];
  int n;

  n = read(0, buf, sizeof(buf));
  if (n < 0) {
    perror("read");
    return 1;
  }

  write(1, buf, n);

  return 0;
}
```

La llamada al sistema `read()` lee datos de un archivo. El primer argumento es el descriptor de archivo. El segundo argumento es un búfer donde se almacenarán los datos. El tercer argumento es el tamaño del búfer.

La llamada al sistema `write()` escribe datos en un archivo. El primer argumento es el descriptor de archivo. El segundo argumento es el búfer que contiene los datos. El tercer argumento es el número de bytes a escribir.

### Escribir en un archivo

Aquí hay un ejemplo de cómo escribir en un archivo usando una biblioteca:

```c
#include <stdio.h>

int main() {
  FILE *fp;
  char buf[1024];
  int n;

  fp = fopen("test.txt", "w");
  if (fp == NULL) {
    perror("fopen");
    return 1;
  }

  n = fwrite(buf, 1, sizeof(buf), fp);
  if (n < 0) {
    perror("fwrite");
    return 1;
  }

  fclose(fp);

  return 0;
}
```

La función `fopen()` abre un archivo. El primer argumento es la ruta del archivo. El segundo argumento es la moda. El modo puede ser `"r"` para leer, `"w"` para escribir o `"a"` para agregar.

La función `fwrite()` escribe datos en un archivo. El primer argumento es el búfer que contiene los datos. El segundo argumento es el tamaño de cada elemento. El tercer argumento es el número de elementos a escribir. El cuarto argumento es el puntero del archivo.

La función `fclose()` cierra un archivo. El argumento es el puntero del archivo.

## Conclusión

En este artículo, hemos visto una breve descripción de las llamadas al sistema y las bibliotecas. También hemos visto algunos ejemplos específicos de cómo usarlos.