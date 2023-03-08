---
title: Depuración de aplicaciones TypeScript y Nest.js con Visual Studio Code
description: 
published: true
date: 2023-02-01T15:23:48.063Z
tags: 
editor: markdown
dateCreated: 2023-02-01T15:23:46.442Z
---

> Este artículo se tradujo automáticamente con la **API de Google Cloud Translation**.
Algunas páginas pueden leerse mejor que el original.{.is-info}

- [Debugging TypeScript and Nest.js Applications with Visual Studio Code***Spanish** version of this document is available*](/es/Knowledge-base/TypeScript/debugging-typescript-and-nest-js-applications-with-visual-studio-code)
{.links-list}



# Depuración de aplicaciones TypeScript y Nest.js con Visual Studio Code

TypeScript es un lenguaje poderoso que proporciona verificación de tipo estático y refactorización de código. Nest.js es un marco para crear aplicaciones escalables del lado del servidor. Visual Studio Code es un editor de código popular que ofrece una excelente compatibilidad con TypeScript y Nest.js.

En este artículo, analizaremos cómo depurar aplicaciones TypeScript y Nest.js con Visual Studio Code. Veremos cómo configurar puntos de interrupción, inspeccionar variables y usar la consola. También aprenderemos sobre algunas de las funciones avanzadas del depurador, como la pila de llamadas y la consola del depurador.

## Configuración del depurador

Lo primero que tenemos que hacer es configurar el depurador. Para hacerlo, abra Visual Studio Code y presione `Ctrl+Shift+P` (Windows) o `Cmd+Shift+P` (macOS) para abrir la paleta de comandos. Escriba `debug` y seleccione el comando `Debug: Open launch.json`.

Esto abrirá el archivo `.vscode/launch.json`. Necesitamos agregar una configuración para nuestra aplicación TypeScript. La configuración debería ser algo como esto:

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "program": "${workspaceFolder}/dist/index.js",
            "outFiles": [
                "${workspaceFolder}/dist/**/*.js"
            ]
        }
    ]
}
```

Analicemos esta configuración. El atributo `type` especifica el tipo de depurador. Queremos usar el depurador `node` porque estamos depurando una aplicación Node.js. El atributo `request` especifica el tipo de lanzamiento. Queremos usar la solicitud `lanzamiento` para que el depurador inicie el programa.

El atributo `name` es el nombre de la configuración. Este es el nombre que se mostrará en la lista desplegable Depurar. El atributo `programa` es la ruta al programa que queremos depurar. En este caso, estamos depurando el archivo `index.js` en el directorio `dist`.

El atributo `outFiles` es una matriz de patrones globales que especifican los archivos que deben tenerse en cuenta para la depuración. En este caso, estamos incluyendo todos los archivos JavaScript en el directorio `dist`.

## Lanzamiento del depurador

Ahora que hemos creado una configuración de lanzamiento, podemos lanzar el depurador. Para hacer esto, presione 'F5' o seleccione el comando 'Depurar: Iniciar depuración' de la Paleta de comandos. Esto iniciará el depurador y lo adjuntará al programa.

## Interrupción de las excepciones

Una de las características más útiles del depurador es la capacidad de interrumpir las excepciones. Esto puede ser muy útil cuando se trata de rastrear un error. Para habilitar esta función, abra el archivo `.vscode/launch.json` y agregue el atributo `"stopOnEntry": true` a la configuración. Esto hará que el depurador se interrumpa en la primera línea del programa.

## Establecer puntos de interrupción

Otra característica útil del depurador es la capacidad de establecer puntos de interrupción. Un punto de interrupción es un punto en el código donde se detendrá la ejecución del programa para que pueda examinar el estado del programa. Para establecer un punto de interrupción, simplemente haga clic en la línea de código donde desea interrumpir. Aparecerá un punto rojo para indicar que se ha establecido un punto de interrupción.

## Inspección de variables

Cuando la ejecución del programa se detiene en un punto de interrupción, puede inspeccionar los valores de las variables. Para hacer esto, simplemente coloque el cursor sobre la variable. El valor de la variable se mostrará en una información sobre herramientas.

También puede usar la `Consola de depuración` para inspeccionar variables. Para abrir la `Consola de depuración`, presione `Ctrl+Shift+Y` (Windows) o `Cmd+Shift+Y` (macOS). La `Consola de depuración` se mostrará en el panel Salida.

## Uso de la pila de llamadas

El panel `Pila de llamadas` es una herramienta muy útil para la depuración. Muestra la secuencia de llamadas a funciones que condujeron al punto actual en la ejecución del programa. Para abrir el panel `Pila de llamadas`, presione `Ctrl+\` (Windows) o `Cmd+\` (macOS).

## Conclusión

En este artículo, hemos aprendido a depurar aplicaciones TypeScript y Nest.js con Visual Studio Code. Hemos visto cómo configurar puntos de interrupción, inspeccionar variables y usar la consola. También hemos aprendido acerca de algunas de las funciones avanzadas del depurador, como la pila de llamadas y la consola del depurador.