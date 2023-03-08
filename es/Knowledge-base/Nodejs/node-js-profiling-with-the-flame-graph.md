---
title: Creación de perfiles de Node.js con el gráfico de llamas
description: 
published: true
date: 2023-02-06T08:17:21.166Z
tags: 
editor: markdown
dateCreated: 2023-02-06T08:17:19.471Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Node.js Profiling with the Flame Graph***English** document is available*](/en/Knowledge-base/Nodejs/node-js-profiling-with-the-flame-graph)
{.links-list}


# Perfilado de Node.js con el gráfico de llamas

Como desarrolladores de Node.js, siempre estamos buscando formas de hacer que nuestras aplicaciones se ejecuten de manera más rápida y eficiente. Para ayudar con esto, podemos usar una herramienta llamada gráfico de llama.

Un gráfico de llamas es un tipo de perfil de rendimiento que nos muestra dónde pasa más tiempo nuestra aplicación Node.js. Puede ser una forma útil de identificar cuellos de botella en nuestro código para que podamos optimizar el rendimiento de nuestra aplicación.

En este artículo, veremos cómo usar la herramienta de gráficos de llamas para crear un perfil de una aplicación Node.js. También aprenderemos sobre algunas de las otras herramientas que están disponibles para la creación de perfiles de rendimiento en Node.js.

## ¿Qué es un gráfico de llama?

Un gráfico de llamas es un tipo de perfil de rendimiento que muestra dónde pasa la mayor parte del tiempo nuestra aplicación Node.js. Puede ser una forma útil de identificar cuellos de botella en nuestro código para que podamos optimizar el rendimiento de nuestra aplicación.

Los gráficos de llamas fueron desarrollados originalmente por Brendan Gregg para visualizar el rendimiento de los sistemas informáticos. El nombre "gráfico de llamas" proviene de la forma en que se ven los gráficos cuando se visualizan, con las barras más altas que representan las áreas donde se pasa la mayor parte del tiempo.

 Gregg ha escrito mucho sobre los gráficos de llamas y su uso para la creación de perfiles de rendimiento. Puede encontrar más información sobre los gráficos de llama en su sitio web:

http://www.brendangregg.com/flamegraphs.html

## Cómo usar gráficos de llamas para la creación de perfiles de Node.js

Hay algunas formas diferentes de generar gráficos de llamas para aplicaciones Node.js. En esta sección, veremos dos de las herramientas más populares:

### Llama de nodo

Node Flame es una herramienta de creación de perfiles de rendimiento de Node.js que genera gráficos de llamas a partir de perfiles de rendimiento. Se puede usar para perfilar aplicaciones que se ejecutan en la plataforma Node.js.

Para usar Node Flame, primero debemos instalarlo usando el administrador de paquetes npm:

```
npm install -g node-flame
```

Una vez que Node Flame está instalado, podemos usarlo para perfilar una aplicación Node.js ejecutando el siguiente comando:

```
node-flame <path-to-application>
```

 Node Flame generará un gráfico de llamas que muestra dónde pasa más tiempo nuestra aplicación. Luego podemos usar esta información para optimizar nuestro código.

### 0x

0x es una herramienta de creación de perfiles de rendimiento de Node.js que se puede utilizar para generar gráficos de llamas. Es de código abierto y está disponible en GitHub:

https://github.com/davecheney/0x

Para usar 0x, primero debemos instalarlo usando el administrador de paquetes npm:

```
npm install -g 0x
```

Una vez que se instala 0x, podemos usarlo para perfilar una aplicación Node.js ejecutando el siguiente comando:

```
0x <path-to-application>
```

0x generará un gráfico de llamas que muestra dónde pasa más tiempo nuestra aplicación. Luego podemos usar esta información para optimizar nuestro código.

## Conclusión

En este artículo, aprendimos sobre los gráficos de llamas y cómo usarlos para perfilar una aplicación Node.js. También hemos visto dos herramientas diferentes que se pueden usar para generar gráficos de llamas: Node Flame y 0x.

La creación de perfiles de rendimiento es una parte importante de la optimización de una aplicación Node.js. Los gráficos de llamas pueden ser una herramienta útil para identificar cuellos de botella en nuestro código para que podamos mejorar el rendimiento de nuestra aplicación.