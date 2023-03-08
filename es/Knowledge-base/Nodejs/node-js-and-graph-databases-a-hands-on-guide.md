---
title: Node.js y bases de datos gráficas: una guía práctica
description: 
published: true
date: 2023-02-03T13:17:36.713Z
tags: 
editor: markdown
dateCreated: 2023-02-03T13:17:35.098Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Node.js and Graph Databases: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-graph-databases-a-hands-on-guide)
{.links-list}


# Node.js y bases de datos gráficas: una guía práctica

En los últimos años, el auge de los grandes datos y la necesidad de procesar grandes cantidades de datos rápidamente ha llevado al desarrollo de nuevas tecnologías de bases de datos, como las bases de datos de gráficos. Las bases de datos de gráficos son ideales para manejar datos que están altamente conectados, como las redes sociales, y para aplicaciones que requieren procesamiento de datos en tiempo real.

Node.js es un entorno de tiempo de ejecución de JavaScript muy adecuado para crear aplicaciones de red rápidas y escalables. En este artículo, exploraremos cómo usar Node.js con una base de datos de gráficos, Neo4j. Aprenderemos cómo instalar Neo4j, importar datos a una base de datos de gráficos y ejecutar consultas contra los datos.

## Instalación de Neo4j

Neo4j se puede instalar en Windows, Mac o Linux. Usaremos la aplicación de escritorio Neo4j, que se puede descargar desde el sitio web de Neo4j.

Una vez que Neo4j Desktop está instalado, podemos crear una nueva base de datos de gráficos. Nombraremos nuestra base de datos "tutorialdb".

## Importación de datos

Usaremos el conjunto de datos de películas del sitio web de Neo4j para este tutorial. El conjunto de datos de películas consta de nodos para películas, actores y directores, y las relaciones entre ellos.

Podemos importar el conjunto de datos de la película a nuestra base de datos Neo4j utilizando el navegador Neo4j. El navegador Neo4j es una interfaz basada en web para Neo4j que se puede utilizar para ejecutar consultas y visualizar datos.

Para importar el conjunto de datos de la película, primero debemos crear una nueva base de datos de gráficos en el navegador Neo4j. Nombraremos nuestra base de datos "tutorialdb".

Una vez que se crea la base de datos, podemos abrir el archivo del conjunto de datos de la película en el navegador Neo4j. El archivo del conjunto de datos de la película es un archivo CSV (valores separados por comas). Podemos abrir el archivo haciendo clic en el botón "Abrir" en el navegador Neo4j.

Una vez abierto el archivo, podemos seleccionar el botón "Importar" para importar los datos a nuestra base de datos Neo4j.

## Ejecutar consultas

Ahora que tenemos nuestros datos importados en Neo4j, podemos comenzar a ejecutar consultas contra los datos.

Podemos encontrar todas las películas en nuestra base de datos ejecutando la siguiente consulta:

PARTIDO (m:Película)
RETORNO m

Esta consulta hará coincidir todos los nodos con la etiqueta "Película" y los devolverá.

También podemos encontrar todos los actores en nuestra base de datos ejecutando la siguiente consulta:

PARTIDO (a: Actor)
DEVOLVER un

Podemos encontrar todos los directores en nuestra base de datos ejecutando la siguiente consulta:

PARTIDO (d:Director)
RETORNO

Podemos encontrar todas las películas en las que ha estado un actor específico ejecutando la siguiente consulta:

PARTIDO (a:Actor)-[:ACTED_IN]->(m:Película)
DONDE a.nombre = "Tom Hanks"
RETORNO m

Esta consulta hará coincidir todos los nodos con la etiqueta "Actor" que tengan una relación con la etiqueta "Película" y devolverá las películas en las que ha estado el actor. En este caso, buscamos todas las películas en las que ha estado Tom Hanks. .

Podemos encontrar todos los directores que tiene una película específica ejecutando la siguiente consulta:

PARTIDO (m:Película)<-[:DIRIGIDO]-(d:Director)
DONDE m.title = "La Matrix"
RETORNO

Esta consulta hará coincidir todos los nodos con la etiqueta "Película" que tengan una relación con la etiqueta "Director" y devolverá los directores de la película. En este caso, estamos buscando a los directores de "The Matrix".

Podemos encontrar todas las películas que ha dirigido un director concreto ejecutando la siguiente consulta:

PARTIDO (d:Director)-[:DIRIGIDO]->(m:Película)
DONDE d.name = "Los Wachowski"
RETORNO m

Esta consulta hará coincidir todos los nodos con la etiqueta "Director" que tengan una relación con la etiqueta "Película" y devolverá las películas que ha dirigido el director. En este caso, buscamos todas las películas que han dirigido las Wachowski.

También podemos encontrar todas las películas en las que ha estado un actor específico y ha dirigido un director específico ejecutando la siguiente consulta:

PARTIDO (a:Actor)-[:ACTUADO_EN]->(m:Película)<-[:DIRIGIDO]-(d:Director)
DONDE a.nombre = "Tom Hanks" Y d.nombre = "Los Wachowski"
RETORNO m

Esta consulta hará coincidir todos los nodos con la etiqueta "Actor" que tengan una relación con la etiqueta "Película" y devolverá las películas en las que el actor ha estado y el director ha dirigido. En este caso, estamos buscando todas las películas en las que ha estado Tom Hanks y que han dirigido los Wachowski.

## Conclusión

En este artículo, hemos aprendido a usar Node.js con una base de datos de gráficos, Neo4j. Hemos instalado Neo4j e importado datos a una base de datos de gráficos. También hemos aprendido cómo ejecutar consultas contra los datos.