---
title: 056: Depuración de aplicaciones TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T20:04:29.641Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:04:27.952Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [056: Debugging TensorFlow.js and Node.js Applications***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/056-debugging-tensorflow-js-and-node-js-applications)
{.links-list}


Depuración de aplicaciones TensorFlow.js y Node.js

TensorFlow.js y Node.js son dos plataformas de JavaScript populares para el aprendizaje automático y el desarrollo web, respectivamente. En esta publicación, le mostraremos cómo depurar las aplicaciones TensorFlow.js y Node.js.

Comenzaremos con una descripción general de las herramientas de depuración para cada plataforma. Luego, veremos algunos escenarios comunes de depuración y cómo resolverlos.

## Herramientas de depuración

### TensorFlow.js

Las herramientas de depuración de TensorFlow.js se basan en Chrome DevTools. Para usarlos, deberá ejecutar su aplicación TensorFlow.js en un navegador que admita DevTools.

Una vez que tenga su aplicación ejecutándose en el navegador, abra DevTools y seleccione la pestaña "Fuentes". Desde aquí, puede establecer puntos de interrupción, inspeccionar variables y revisar su código.

Las herramientas de depuración de TensorFlow.js también incluyen un panel "Depurador para TensorFlow.js". Este panel proporciona una vista de nivel superior de su código TensorFlow.js y se puede usar para depurar las operaciones de TensorFlow.js.

### Nodo.js

Las herramientas de depuración de Node.js se basan en el protocolo de depuración V8. Para usarlos, deberá ejecutar su aplicación Node.js con el indicador --inspect.

Una vez que su aplicación se ejecuta con el indicador --inspect, puede adjuntarle un depurador. Recomendamos usar el depurador de Visual Studio Code, que admite el protocolo de depuración V8.

Una vez que haya conectado su depurador, puede establecer puntos de interrupción, inspeccionar variables y recorrer su código.

## Escenarios de depuración

### TensorFlow.js

#### Escenario: mi aplicación no se está ejecutando

Si su aplicación TensorFlow.js no se está ejecutando, lo primero que debe verificar es la consola del navegador en busca de errores. La consola del navegador se puede abrir con la pestaña "Consola" de DevTools.

Si no hay errores en la consola del navegador, lo siguiente que debe verificar es el panel de operaciones de TensorFlow.js. Este panel se puede abrir con la pestaña "Depurador para TensorFlow.js" de DevTools.

Si ve algún error en el panel de operaciones de TensorFlow.js, puede hacer clic en él para ver más detalles.

#### Escenario: mi aplicación se ejecuta lentamente

Si su aplicación TensorFlow.js se ejecuta lentamente, lo primero que debe verificar es la consola del navegador para ver si hay advertencias. La consola del navegador se puede abrir con la pestaña "Consola" de DevTools.

Si no hay advertencias en la consola del navegador, lo siguiente que debe verificar es el panel de operaciones de TensorFlow.js. Este panel se puede abrir con la pestaña "Depurador para TensorFlow.js" de DevTools.

Si ve alguna advertencia en el panel de operaciones de TensorFlow.js, puede hacer clic en ella para ver más detalles.

#### Escenario: mi aplicación no usa la GPU

Si su aplicación TensorFlow.js no usa la GPU, lo primero que debe verificar es la consola del navegador en busca de errores. La consola del navegador se puede abrir con la pestaña "Consola" de DevTools.

Si no hay errores en la consola del navegador, lo siguiente que debe verificar es el panel de operaciones de TensorFlow.js. Este panel se puede abrir con la pestaña "Depurador para TensorFlow.js" de DevTools.

Si ve algún error en el panel de operaciones de TensorFlow.js, puede hacer clic en él para ver más detalles.

### Nodo.js

#### Escenario: mi aplicación no se está ejecutando

Si su aplicación Node.js no se está ejecutando, lo primero que debe verificar es la consola del depurador en busca de errores. La consola del depurador se puede abrir con el panel "Depurar" de Visual Studio Code.

Si no hay errores en la consola del depurador, lo siguiente que debe verificar es el panel de operaciones de Node.js. Este panel se puede abrir con el panel "Node.js" de Visual Studio Code.

Si ve algún error en el panel de operaciones de Node.js, puede hacer clic en él para ver más detalles.

#### Escenario: mi aplicación se ejecuta lentamente

Si su aplicación Node.js se ejecuta lentamente, lo primero que debe verificar es la consola del depurador para ver si hay advertencias. La consola del depurador se puede abrir con el panel "Depurar" de Visual Studio Code.

Si no hay advertencias en la consola del depurador, lo siguiente que debe verificar es el panel de operaciones de Node.js. Este panel se puede abrir con el panel "Node.js" de Visual Studio Code.

Si ve alguna advertencia en el panel de operaciones de Node.js, puede hacer clic en ella para ver más detalles.

#### Escenario: mi aplicación no usa la CPU

Si su aplicación Node.js no está usando la CPU, lo primero que debe verificar es la consola del depurador en busca de errores. La consola del depurador se puede abrir con el panel "Depurar" de Visual Studio Code.

Si no hay errores en la consola del depurador, lo siguiente que debe verificar es el panel de operaciones de Node.js. Este panel se puede abrir con el panel "Node.js" de Visual Studio Code.

Si ve algún error en el panel de operaciones de Node.js, puede hacer clic en él para ver más detalles.

## Información Adicional

### TensorFlow.js

Para obtener más información sobre la depuración de aplicaciones de TensorFlow.js, consulte la documentación de depuración de TensorFlow.js.

### Nodo.js

Para obtener más información sobre la depuración de aplicaciones de Node.js, consulte la documentación de depuración de Node.js.