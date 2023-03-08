---
title: Desarrollo de software 052: Sistemas de recomendación
description: 
published: true
date: 2023-02-02T19:57:45.713Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:57:41.096Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Software Development 052: Recommender Systems***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-052-recommender-systems)
{.links-list}


# Desarrollo de software 052: Sistemas de recomendación

En los últimos años, los sistemas de recomendación se han vuelto cada vez más populares. Un sistema de recomendación, también conocido como sistema de recomendación, es una subclase de sistema de filtrado de información que busca predecir la "calificación" o "preferencia" que un usuario le daría a un artículo.

Los sistemas de recomendación se utilizan en una variedad de áreas, con ejemplos comúnmente reconocidos que toman la forma de generadores de listas de reproducción para servicios de video y música, recomendadores de productos para tiendas en línea o recomendadores de contenido para plataformas de redes sociales y recomendadores de contenido web abierto. Estos sistemas pueden operar usando una sola entrada, como música, o múltiples entradas dentro y entre plataformas como noticias, libros y consultas de búsqueda.

Hay algunos tipos diferentes de sistemas de recomendación, y el que elija dependerá del tipo de datos que tenga y de lo que desee recomendar. Los tres tipos principales de sistemas de recomendación son los basados en contenido, el filtrado colaborativo y los híbridos.

## Basado en contenido

Los sistemas de recomendación basados en contenido se basan en la similitud entre los elementos. Este enfoque se usa cuando tiene un gran conjunto de datos de elementos con algún tipo de metadatos adjuntos. Por ejemplo, si estuviera creando un recomendador de películas, podría usar metadatos como género, director, actor y palabras clave para encontrar películas similares.

El primer paso para crear un recomendador basado en contenido es crear un perfil basado en contenido para cada artículo. Este perfil se utiliza luego para calcular la similitud entre los elementos. La similitud entre los elementos a menudo se calcula utilizando la similitud del coseno, que es una medida de qué tan cerca están alineados dos vectores.

Una vez que haya calculado la similitud entre los elementos, puede recomendar elementos a los usuarios en función de sus perfiles. Por ejemplo, si un usuario ha visto muchas películas de acción, podría recomendarle otras películas de acción similares a las que ya ha visto.

## Filtración colaborativa

El filtrado colaborativo es un método para hacer recomendaciones que se basan en la sabiduría colectiva de un grupo de personas. Este enfoque se usa cuando tiene un conjunto de datos de usuarios y sus calificaciones para los elementos.

Hay dos tipos principales de filtrado colaborativo: basado en usuarios y basado en elementos.

El filtrado colaborativo basado en el usuario es un método para hacer recomendaciones que se basan en la similitud entre los usuarios. Este enfoque se usa cuando tiene un conjunto de datos de usuarios y sus calificaciones para los elementos. Por ejemplo, si estuviera creando un recomendador de películas, podría usar las calificaciones de otros usuarios para encontrar usuarios similares. Una vez que haya encontrado usuarios similares, puede recomendar elementos al usuario actual que los usuarios similares hayan calificado altamente.

El filtrado colaborativo basado en elementos es un método para hacer recomendaciones que se basan en la similitud entre los elementos. Este enfoque se usa cuando tiene un conjunto de datos de usuarios y sus calificaciones para los elementos. Por ejemplo, si estuviera creando un recomendador de películas, podría usar las calificaciones de otros usuarios para encontrar películas similares. Una vez que haya encontrado películas similares, puede recomendar esas películas al usuario actual.

## Híbrido

Un sistema de recomendación híbrido es una combinación de filtrado colaborativo y basado en contenido. Este enfoque se usa cuando tiene un conjunto de datos de elementos con algún tipo de metadatos adjuntos y un conjunto de datos de usuarios y sus calificaciones para los elementos.

El primer paso para crear un recomendador híbrido es crear un perfil basado en contenido para cada artículo. Este perfil se utiliza luego para calcular la similitud entre los elementos. La similitud entre los elementos a menudo se calcula utilizando la similitud del coseno, que es una medida de qué tan cerca están alineados dos vectores.

Una vez que haya calculado la similitud entre los elementos, puede recomendar elementos a los usuarios en función de sus perfiles. Por ejemplo, si un usuario ha visto muchas películas de acción, podría recomendarle otras películas de acción similares a las que ya ha visto.

Además de las recomendaciones basadas en el contenido, también puede usar el filtrado colaborativo para hacer recomendaciones. Hay dos tipos principales de filtrado colaborativo: basado en usuarios y basado en elementos.

El filtrado colaborativo basado en el usuario es un método para hacer recomendaciones que se basan en la similitud entre los usuarios. Este enfoque se usa cuando tiene un conjunto de datos de usuarios y sus calificaciones para los elementos. Por ejemplo, si estuviera creando un recomendador de películas, podría usar las calificaciones de otros usuarios para encontrar usuarios similares. Una vez que haya encontrado usuarios similares, puede recomendar elementos al usuario actual que los usuarios similares hayan calificado altamente.

El filtrado colaborativo basado en elementos es un método para hacer recomendaciones que se basan en la similitud entre los elementos. Este enfoque se usa cuando tiene un conjunto de datos de usuarios y sus calificaciones para los elementos. Por ejemplo, si estuviera creando un recomendador de películas, podría usar las calificaciones de otros usuarios para encontrar películas similares. Una vez que haya encontrado películas similares, puede recomendar esas películas al usuario actual.

## Conclusión

Los sistemas de recomendación son una herramienta poderosa que se puede utilizar para personalizar la experiencia del usuario en su sitio web o aplicación. Al comprender los diferentes tipos de sistemas de recomendación y cómo funcionan, puede elegir el adecuado para sus necesidades.