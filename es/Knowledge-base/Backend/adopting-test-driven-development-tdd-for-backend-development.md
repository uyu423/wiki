---
title: Adopción del desarrollo basado en pruebas (TDD) para el desarrollo de back-end
description: 
published: true
date: 2023-02-16T11:17:29.027Z
tags: 
editor: markdown
dateCreated: 2023-02-16T11:17:27.329Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Adopting Test Driven Development (TDD) for Backend Development***English** document is available*](/en/Knowledge-base/Backend/adopting-test-driven-development-tdd-for-backend-development)
{.links-list}


# Adopción del desarrollo basado en pruebas (TDD) para el desarrollo de back-end

## ¿Qué es el desarrollo dirigido por pruebas?

El desarrollo basado en pruebas (TDD) es un proceso de desarrollo de software que se basa en la repetición de un ciclo de desarrollo muy corto: primero, el desarrollador escribe un caso de prueba automatizado (inicialmente fallido) que define una mejora deseada o una nueva función, luego produce la cantidad mínima de código para pasar esa prueba y finalmente refactoriza el nuevo código a estándares aceptables.

TDD se opone al modelo tradicional de desarrollo en cascada, en el que los requisitos se recopilan antes de que comience la codificación.

TDD se puede utilizar para mejorar la calidad de su código y hacerlo más robusto. También puede hacer que su proceso de desarrollo sea más eficiente al ayudarlo a evitar la repetición del trabajo.

## ¿Por qué usar TDD?

Hay muchas razones para adoptar TDD para su desarrollo de back-end. Estos son algunos de los beneficios más importantes:

### 1. TDD te ayuda a escribir mejor código

TDD lo obliga a pensar en la funcionalidad que está tratando de agregar o cambiar, y cómo debe usarse. Esto le ayuda a escribir código que es más comprensible, mantenible y comprobable.

### 2. TDD lo ayuda a detectar errores temprano

Si una prueba falla, eso significa que hay un error en su código. Al escribir pruebas antes de escribir el código, puede detectar errores temprano y evitar tener que corregirlos más tarde.

### 3. TDD te ayuda a escribir menos código

TDD puede ayudarlo a evitar escribir código innecesario. Si descubre que está escribiendo código que no está cubierto por una prueba, es probable que el código no sea necesario.

### 4. TDD lo ayuda a cumplir con los plazos

TDD puede ayudarlo a cumplir con los plazos al ayudarlo a evitar escribir código que no es necesario. Al centrarse en la funcionalidad que se requiere, puede evitar escribir código que no es necesario y ahorrar tiempo.

### 5. TDD te ayuda a evitar regresiones

Las regresiones son cambios que rompen la funcionalidad existente. Al escribir pruebas antes de escribir código, puede evitar la introducción de regresiones.

## Cómo usar TDD

TDD es un proceso que consta de tres pasos:

### 1. Escribe una prueba

El primer paso es escribir una prueba que defina la funcionalidad que desea agregar o cambiar. La prueba debe escribirse de manera que falle cuando se ejecute el código.

### 2. Escribe el código

El segundo paso es escribir el código que hará pasar la prueba. El código debe estar escrito de una manera que sea fácil de entender y mantener.

### 3. Refactorizar el Código

El tercer paso es refactorizar el código. Esto se hace para mejorar la calidad del código y hacerlo más mantenible.

## Ejemplo

Digamos que queremos agregar una nueva función a nuestro backend que convierte Celsius a Fahrenheit. Comenzaríamos escribiendo una prueba para la nueva función:

```
def test_celsius_to_fahrenheit(self):
    celsius = 100
    fahrenheit = 212
    self.assertEqual(celsius_to_fahrenheit(celsius), fahrenheit)
```

Esta prueba define la funcionalidad de la nueva función. Luego escribiríamos el código para hacer que la prueba pase:

```
def celsius_to_fahrenheit(celsius):
    fahrenheit = celsius * 9 / 5 + 32
    return fahrenheit
```

Finalmente, refactorizaríamos el código para mejorar la calidad:

```
def celsius_to_fahrenheit(celsius):
    """Converts Celsius to Fahrenheit."""
    fahrenheit = celsius * 9 / 5 + 32
    return fahrenheit
```

## Conclusión

TDD es un proceso de desarrollo de software que puede ayudarlo a escribir mejor código, detectar errores temprano y evitar regresiones. Es un proceso que consta de tres pasos: escribir una prueba, escribir el código y refactorizar el código.