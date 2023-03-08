---
title: 016: Depuración de aplicaciones Nest.js
description: 
published: true
date: 2023-02-15T01:32:20.206Z
tags: 
editor: markdown
dateCreated: 2023-02-15T01:32:18.366Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [016: Debugging Nest.js applications***English** document is available*](/en/Knowledge-base/Nest-js/Learning/016-debugging-nest-js-applications)
{.links-list}


# Depuración de aplicaciones Nest.js

Nest.js es un marco de Node.js para crear aplicaciones del lado del servidor. Utiliza TypeScript y está basado en Express.

La depuración de las aplicaciones de Nest.js puede ser un desafío, ya que existen varias formas de depurar las aplicaciones de Node.js en general, y Nest.js agrega sus propias complejidades además de eso. En esta publicación, repasaremos algunos de los aspectos básicos de la depuración de aplicaciones Nest.js.

## Depuración de aplicaciones Node.js

Las aplicaciones de Node.js se pueden depurar de varias maneras. La forma más común es usar el depurador Node.js, que se puede invocar con el comando `debug`.

```
$ node debug <script.js>
```

Esto iniciará el depurador de Node.js y proporcionará un aviso donde puede ingresar comandos. Para obtener una lista completa de comandos, escriba `ayuda` en el indicador.

Otra forma de depurar aplicaciones de Node.js es usar un depurador gráfico, como el que proporciona Visual Studio Code. Para usar esto, deberá instalar la extensión Node.js para Visual Studio Code.

Una vez instalada la extensión, puede abrir su proyecto Nest.js en Visual Studio Code y establecer puntos de interrupción en su código. Para iniciar el depurador, presione F5 o haga clic en el ícono Depurar en la Barra de actividad.

## Depuración de aplicaciones Nest.js

Nest.js agrega su propia capa encima de Node.js, por lo que los métodos para depurar aplicaciones de Nest.js son similares a los de depurar aplicaciones de Node.js.

La forma más común de depurar aplicaciones Nest.js es usar el comando `nest`, que proporciona la CLI de Nest.js.

```
$ nest debug <script.ts>
```

Esto iniciará el depurador de Nest.js y proporcionará un aviso donde puede ingresar comandos. Para obtener una lista completa de comandos, escriba `ayuda` en el indicador.

Otra forma de depurar aplicaciones Nest.js es usar un depurador gráfico, como el que proporciona Visual Studio Code. Para usar esto, deberá instalar la extensión Nest.js para Visual Studio Code.

Una vez instalada la extensión, puede abrir su proyecto Nest.js en Visual Studio Code y establecer puntos de interrupción en su código. Para iniciar el depurador, presione F5 o haga clic en el ícono Depurar en la Barra de actividad.

## Información adicional

- [Depuración de aplicaciones Node.js](https://nodejs.org/en/docs/guides/debugging-getting-started/)
- [Depuración de aplicaciones Nest.js](https://docs.nestjs.com/cli/debug)
- [Extensión de Visual Studio Code para Nest.js](https://marketplace.visualstudio.com/items?itemName=nestjs.nest-cli)