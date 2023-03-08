---
title: El principio de sustitución de Liskov en el desarrollo de Spring Boot
description: 
published: true
date: 2023-02-08T10:32:30.592Z
tags: 
editor: markdown
dateCreated: 2023-02-08T10:32:28.991Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [The Liskov Substitution Principle in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-liskov-substitution-principle-in-spring-boot-development)
{.links-list}


## Introducción

El principio de sustitución de Liskov es un principio fundamental de la programación orientada a objetos que establece que las clases derivadas deben ser sustituibles por sus clases base. En otras palabras, cualquier método que utilice una referencia a una clase base debería funcionar igualmente bien con una referencia a cualquier clase derivada sin necesidad de que el programador realice ningún cambio.

El principio lleva el nombre de Barbara Liskov, quien lo formalizó por primera vez en un artículo de 1987 titulado "Abstracción de datos y jerarquía".

## ¿Qué es el principio de sustitución de Liskov?

En pocas palabras, el principio de sustitución de Liskov establece que las clases derivadas deben ser sustituibles por sus clases base. En otras palabras, cualquier método que utilice una referencia a una clase base debería funcionar igualmente bien con una referencia a cualquier clase derivada sin necesidad de que el programador realice ningún cambio.

El principio lleva el nombre de Barbara Liskov, quien lo formalizó por primera vez en un artículo de 1987 titulado "Abstracción de datos y jerarquía".

El artículo de Liskov se inspiró en un artículo escrito por David Parnas en 1972 titulado "Sobre los criterios que se utilizarán para descomponer sistemas en módulos". En ese documento, Parnas presenta el "principio de sustitución", que establece que "cualquier módulo M1 que use un módulo M2 puede reemplazarse con otro módulo M3 que use M2 siempre que M3 proporcione la misma interfaz abstracta que M1 a M2".

El artículo de Liskov generaliza este principio a la herencia, mostrando que se aplica no solo a los módulos sino a cualquier jerarquía. Ella formaliza el principio de la siguiente manera:

"Sea q(x) una propiedad demostrable sobre objetos x de tipo T. Entonces q(y) debería ser demostrable sobre objetos y de tipo S donde S es un subtipo de T".

En otras palabras, si una propiedad es verdadera para una clase base, también debería serlo para todas las clases derivadas.

## El principio de sustitución de Liskov en la práctica

El principio de sustitución de Liskov a menudo se viola en la práctica, especialmente en el código heredado. Una infracción común es el problema de la "clase base frágil", donde un cambio en una clase base rompe todas las clases derivadas.

Otra infracción común es el problema de la "jerarquía frágil", donde un cambio en una clase derivada rompe la clase base.

Para evitar estos problemas, es importante diseñar sus clases de tal manera que se adhieran al principio de sustitución de Liskov.

Una forma de hacer esto es usar clases o interfaces abstractas en lugar de clases concretas. Esto le permite cambiar la implementación de una clase sin romper ningún código que la use.

Otra forma de adherirse al principio de sustitución de Liskov es usar composición en lugar de herencia. Esto le permite cambiar la implementación de una clase sin romper ningún código que la use.

## El principio de sustitución de Liskov en el desarrollo de Spring Boot

Spring Boot es un marco Java popular que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

El principio de sustitución de Liskov es un principio importante de la programación orientada a objetos y Spring Boot se adhiere a este principio.

Por ejemplo, Spring Boot usa clases e interfaces abstractas en lugar de clases concretas. Esto le permite cambiar la implementación de una clase sin romper ningún código que la use.

Además, Spring Boot usa composición en lugar de herencia. Esto le permite cambiar la implementación de una clase sin romper ningún código que la use.

## Conclusión

El principio de sustitución de Liskov es un principio fundamental de la programación orientada a objetos que establece que las clases derivadas deben ser sustituibles por sus clases base. En otras palabras, cualquier método que utilice una referencia a una clase base debería funcionar igualmente bien con una referencia a cualquier clase derivada sin necesidad de que el programador realice ningún cambio.

El principio lleva el nombre de Barbara Liskov, quien lo formalizó por primera vez en un artículo de 1987 titulado "Abstracción de datos y jerarquía".

El principio de sustitución de Liskov a menudo se viola en la práctica, especialmente en el código heredado. Una infracción común es el problema de la "clase base frágil", donde un cambio en una clase base rompe todas las clases derivadas.

Otra infracción común es el problema de la "jerarquía frágil", donde un cambio en una clase derivada rompe la clase base.

Para evitar estos problemas, es importante diseñar sus clases de tal manera que se adhieran al principio de sustitución de Liskov.

Una forma de hacer esto es usar clases o interfaces abstractas en lugar de clases concretas. Esto le permite cambiar la implementación de una clase sin romper ningún código que la use.

Otra forma de adherirse al principio de sustitución de Liskov es usar composición en lugar de herencia. Esto le permite cambiar la implementación de una clase sin romper ningún código que la use.

Spring Boot es un marco Java popular que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

El principio de sustitución de Liskov es un principio importante de la programación orientada a objetos y Spring Boot se adhiere a este principio.

Por ejemplo, Spring Boot usa clases e interfaces abstractas en lugar de clases concretas. Esto le permite cambiar la implementación de una clase sin romper ningún código que la use.

Además, Spring Boot usa composición en lugar de herencia. Esto le permite cambiar la implementación de una clase sin romper ningún código que la use.