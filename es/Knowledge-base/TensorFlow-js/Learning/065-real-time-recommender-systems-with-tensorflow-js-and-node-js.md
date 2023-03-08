---
title: 065: Sistemas de recomendación en tiempo real con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T22:17:29.699Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:17:28.098Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [065: Real-Time Recommender Systems with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/065-real-time-recommender-systems-with-tensorflow-js-and-node-js)
{.links-list}


# Sistemas de recomendación en tiempo real con TensorFlow.js y Node.js

En esta publicación, aprenderemos a crear un sistema de recomendación en tiempo real con TensorFlow.js y Node.js. Comenzaremos discutiendo los conceptos clave detrás de los sistemas de recomendación y cómo funcionan. Luego implementaremos un sistema de recomendación simple usando TensorFlow.js y Node.js.

## ¿Qué es un sistema de recomendación?

Un sistema de recomendación (también llamado sistema de recomendación) es un tipo de inteligencia artificial que se utiliza para predecir lo que un usuario podría querer comprar o mirar. Las principales empresas como Amazon, Netflix y Spotify utilizan los sistemas de recomendación para personalizar la experiencia del usuario y aumentar la participación del cliente.

Hay dos tipos principales de sistemas de recomendación: filtrado colaborativo y basado en contenido.

Los sistemas de recomendación basados en contenido recomiendan elementos a los usuarios en función de la similitud entre los elementos. Por ejemplo, un sistema de recomendación de películas basado en el contenido podría recomendar una película a un usuario en función de las calificaciones anteriores del usuario de películas similares.

Los sistemas de recomendación de filtrado colaborativo recomiendan elementos a los usuarios en función de las calificaciones de otros usuarios. Por ejemplo, un sistema de recomendación de filtrado colaborativo para películas podría recomendar una película a un usuario en función de las calificaciones de otros usuarios que calificaron películas similares.

## ¿Cómo funcionan los sistemas de recomendación?

Los sistemas de recomendación utilizan una variedad de técnicas para predecir lo que un usuario podría querer comprar o ver. Las técnicas más comunes son la factorización de matrices y el aprendizaje profundo.

La factorización de matrices es una técnica que se utiliza para descomponer una matriz en sus partes constituyentes. La factorización de matrices se utiliza en los sistemas de recomendación para descomponer la matriz de elementos de usuario en dos matrices más pequeñas: una que contiene los vectores de usuario y otra que contiene los vectores de elementos.

El aprendizaje profundo es un tipo de aprendizaje automático que se utiliza para aprender patrones complejos en los datos. El aprendizaje profundo se utiliza en los sistemas de recomendación para aprender los patrones complejos en la matriz de elementos de usuario.

## Implementación de un sistema de recomendación

En esta sección, implementaremos un sistema de recomendación simple basado en contenido usando TensorFlow.js y Node.js.

Comenzaremos creando una matriz de elementos de usuario. La matriz de elementos de usuario es una matriz que contiene las calificaciones de los usuarios para los elementos. En nuestro caso, los artículos serán películas y las calificaciones serán las calificaciones que los usuarios le han dado a esas películas.

Luego usaremos TensorFlow.js para factorizar la matriz de elementos de usuario. TensorFlow.js es una biblioteca de JavaScript para el aprendizaje automático.

Finalmente, usaremos Node.js para recomendar películas a los usuarios. Node.js es un tiempo de ejecución de JavaScript que se utiliza para la programación del lado del servidor.

## Creación de la matriz de elementos de usuario

El primer paso es crear la matriz usuario-elemento. Haremos esto creando un archivo JSON que contenga las calificaciones de los usuarios para las películas.

El archivo JSON tendrá el siguiente formato:

```json
{
 "user1": {
  "movie1": 4,
  "movie2": 5,
  "movie3": 3
 },
 "user2": {
  "movie1": 5,
  "movie2": 4,
  "movie3": 3
 },
 "user3": {
  "movie1": 3,
  "movie2": 3,
  "movie3": 5
}
}
```

## Factorización de la matriz de elementos de usuario

Ahora que tenemos la matriz de elementos de usuario, podemos factorizarla usando TensorFlow.js. La factorización de la matriz de elementos de usuario nos dará los vectores de usuario y los vectores de elementos.

Los vectores de usuario son vectores que representan a los usuarios en la matriz de elementos de usuario. Los vectores de elementos son vectores que representan los elementos en la matriz de elementos de usuario.

## Recomendación

Finalmente, podemos usar los vectores de usuario y los vectores de elementos para recomendar películas a los usuarios. Haremos esto encontrando la similitud entre los vectores de usuario y los vectores de elementos.

La similitud entre dos vectores es una medida de qué tan cerca están los vectores entre sí. Cuanto más cerca están los vectores entre sí, más similares son.

Podemos usar la similitud del coseno para medir la similitud entre dos vectores. La similitud del coseno es una medida del ángulo entre dos vectores. La similitud del coseno se define como:

![Similitud de coseno](https://wikimedia.org/api/rest_v1/media/math/render/svg/bc28c1e82ea0fd1caec6e9eaa86bbfff1a03b2b4)

donde A y B son los dos vectores y ||A|| y ||B|| son las normas euclidianas de los vectores.

Podemos usar la similitud del coseno para recomendar películas a los usuarios. Haremos esto encontrando la similitud del coseno entre los vectores de usuario y los vectores de elementos. La similitud del coseno nos dará una medida de qué tan similares son los vectores de usuario a los vectores de elementos.

Entonces podemos recomendar películas a los usuarios encontrando las películas con la mayor similitud de coseno con los vectores de usuario.

## Conclusión

En esta publicación, aprendimos cómo crear un sistema de recomendación en tiempo real con TensorFlow.js y Node.js. Comenzamos discutiendo los conceptos clave detrás de los sistemas de recomendación y cómo funcionan. Luego implementamos un sistema de recomendación simple usando TensorFlow.js y Node.js.