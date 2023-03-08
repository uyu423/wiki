---
title: Buffer Overflow
description: 
published: true
date: 2023-02-02T11:24:05.838Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:24:00.802Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Buffer Overflow***English** document is available*](/en/Knowledge-base/Dictionary/buffer-overflow)
{.links-list}


# Descripción general
El desbordamiento de búfer es un tipo de vulnerabilidad de software en el que un programa almacena más datos en un búfer de los que debe contener. Cuando esto ocurre, puede hacer que el programa se bloquee, se vuelva inestable o incluso permita que se ejecute un código malicioso.

# Descripción
Un búfer es una región de la memoria utilizada para almacenar datos temporalmente. Cuando los datos se escriben en un búfer, se almacenan en la memoria hasta que el programa termina con ellos. Si se escriben más datos en el búfer de los que está diseñado para contener, puede hacer que los datos almacenados en el búfer sobrescriban otras partes de la memoria, lo que podría provocar un bloqueo u otro comportamiento inesperado.

Los desbordamientos de búfer pueden ocurrir en cualquier lenguaje de programación, pero son especialmente comunes en C y C++. Esto se debe a que C y C++ no tienen una verificación de límites integrada, lo que significa que si un programador no verifica explícitamente los desbordamientos del búfer, el programa puede volverse vulnerable fácilmente.

Los desbordamientos de búfer pueden ser explotados por actores malintencionados para obtener acceso a un sistema. Esto se puede hacer escribiendo código malicioso en el búfer, que luego puede ser ejecutado por el programa. Esto puede permitir a los atacantes obtener acceso a información confidencial, ejecutar código arbitrario o incluso tomar el control del sistema.

# Historia
El concepto de desbordamiento de búfer existe desde al menos la década de 1970, cuando Bob Morris lo describió por primera vez en un artículo. En 1988, la primera instancia conocida de un desbordamiento de búfer ocurrió cuando un pirata informático obtuvo acceso a un sistema al explotar un desbordamiento de búfer en el daemon finger.

Desde entonces, los desbordamientos de búfer se han convertido en un importante problema de seguridad. En la década de 1990, se descubrieron varias vulnerabilidades de desbordamiento de búfer de alto perfil, incluido el infame gusano Morris. En los últimos años, se han descubierto desbordamientos de búfer en varios programas populares, incluidos Microsoft Office, Adobe Reader y el kernel de Linux.

# Características
Los desbordamientos de búfer se caracterizan por las siguientes características:

- Ocurren cuando se escriben más datos en un búfer de los que está diseñado para contener.
- Pueden provocar bloqueos, inestabilidad o ejecución de código malicioso.
- Son especialmente comunes en C y C++ debido a la falta de verificación de límites.
- Pueden ser explotados por actores maliciosos para obtener acceso a un sistema.

# Ejemplo
Un ejemplo común de un desbordamiento de búfer es un programa que lee la entrada del usuario desde la línea de comandos. Si el usuario ingresa más datos de los que el búfer está diseñado para contener, puede hacer que el programa se bloquee o permitir que se ejecute un código malicioso.

# Pros y contras
La principal ventaja de los desbordamientos de búfer es que se pueden utilizar para obtener acceso a un sistema. Sin embargo, esta también es la principal desventaja, ya que los desbordamientos de búfer pueden ser explotados por actores malintencionados para obtener acceso a información confidencial o tomar el control del sistema.

# Controversia
Los desbordamientos de búfer han sido una fuente de controversia en la comunidad de seguridad. Por un lado, los desbordamientos de búfer pueden ser explotados por actores maliciosos para obtener acceso a un sistema. Por otro lado, los desbordamientos de búfer se pueden utilizar para fines legítimos, como fuzzing o ingeniería inversa.

# Tecnología relacionada
Los desbordamientos de búfer están relacionados con otros tipos de vulnerabilidades de software, como desbordamientos de pila, desbordamientos de montón y vulnerabilidades de cadena de formato. También están relacionados con lenguajes de programación como C y C++, que carecen de verificación de límites integrada.

# Digresión
Los desbordamientos de búfer han sido una fuente importante de vulnerabilidades de seguridad durante décadas. Como resultado, se han desarrollado varias técnicas para detectar y prevenir desbordamientos de búfer, como canarios de pila, aleatorización del diseño del espacio de direcciones (ASLR) y prevención de ejecución de datos (DEP).

# Otros
Los desbordamientos de búfer pueden ser difíciles de detectar y prevenir. Como resultado, siguen siendo una importante preocupación de seguridad en la actualidad. Para reducir el riesgo de desbordamientos de búfer, es importante utilizar prácticas de programación seguras, como el uso de verificación de límites y evitar funciones no seguras.