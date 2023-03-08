---
title: Cómo construir un chatbot con Microsoft Bot Framework
description: 
published: true
date: 2023-02-12T09:17:32.171Z
tags: 
editor: markdown
dateCreated: 2023-02-12T09:17:30.476Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [How to Build a Chatbot with Microsoft Bot Framework***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-chatbot-with-microsoft-bot-framework)
{.links-list}


# Cómo construir un chatbot con Microsoft Bot Framework

Desarrollar un chatbot puede parecer una tarea desalentadora, pero con Microsoft Bot Framework puede ser fácil y divertido. En este artículo, repasaremos todo lo que necesita saber para comenzar a crear su propio chatbot.

## ¿Qué es un chatbot?

Un chatbot es un programa informático que simula una conversación humana. Los chatbots se utilizan en una variedad de industrias, incluido el servicio al cliente, el marketing e incluso la atención médica.

## ¿Por qué construir un chatbot?

Los chatbots pueden ser una excelente manera de mejorar el servicio al cliente o ayudar a las personas a encontrar información. ¡También se pueden usar para marketing o incluso solo para divertirse!

## ¿Qué necesito para construir un chatbot?

Para construir un chatbot, necesitará una computadora con conexión a Internet y un editor de texto. También necesitará una cuenta de Microsoft. Si no tienes uno, puedes crear uno gratis.

## ¿Cómo construyo un chatbot?

Hay dos formas principales de crear un chatbot: usar las herramientas de Bot Framework o usar Azure Bot Service.

### Uso de las herramientas de Bot Framework

Las herramientas de Bot Framework son una excelente manera de comenzar a construir su chatbot. Incluyen todo lo que necesita para comenzar, incluido un SDK de Bot Builder y una CLI.

Para comenzar, primero cree una nueva carpeta para su proyecto de chatbot. Luego, abra la carpeta en su editor de texto y cree un archivo llamado `app.js`.

A continuación, deberá instalar el SDK de Bot Builder. Puedes hacer esto usando npm:

```
npm install botbuilder
```

Una vez que el SDK está instalado, puede importarlo a su archivo `app.js`:

```js
const builder = require('botbuilder');
```

¡Ahora estás listo para comenzar a codificar!

Primero, deberá crear un adaptador de bot. Esto se usará para conectar su chatbot a Microsoft Bot Framework. Puedes hacer esto con el siguiente código:

```js
const adapter = new builder.BotFrameworkAdapter();
```

A continuación, deberá crear un controlador de bot. Esto se usará para manejar los mensajes entrantes del usuario. Puedes hacer esto con el siguiente código:

```js
const bot = new builder.UniversalBot(adapter);
```

¡Ahora está listo para comenzar a agregar código a su controlador de bot!

Lo primero que deberá hacer es definir un cuadro de diálogo "Mensaje de bienvenida". Este cuadro de diálogo se utilizará para saludar al usuario y comenzar. Puedes hacer esto con el siguiente código:

```js
bot.dialog('WelcomeMessage', [
    (session) => {
        session.send("Hello! I'm a chatbot.");
        session.beginDialog('GetName');
    },
]);
```

Como puede ver, este cuadro de diálogo enviará un mensaje al usuario y luego iniciará el cuadro de diálogo `GetName`.

El cuadro de diálogo `GetName` se utilizará para obtener el nombre del usuario. Puedes hacer esto con el siguiente código:

```js
bot.dialog('GetName', [
    (session) => {
        builder.Prompts.text(session, "What's your name?");
    },
    (session, results) => {
        session.endDialog(`Hello, ${results.response}!`);
    },
]);
```

Como puede ver, este cuadro de diálogo solicitará al usuario su nombre y luego almacenará la respuesta en una variable llamada `resultados.respuesta`. Luego finalizará el diálogo y enviará un mensaje al usuario con su nombre.

¡Ahora estás listo para probar tu chatbot! Para hacer esto, deberá ejecutar el siguiente comando:

```
node app.js
```

¡Esto iniciará su chatbot y ahora puede hablar con él! Intenta decir "Hola" o "¿Cómo te llamas?" y ver lo que hace.

### Uso del servicio de bots de Azure

Azure Bot Service es una excelente manera de crear e implementar su chatbot. Incluye todo lo que necesita para comenzar, incluido un SDK de Bot Builder y una CLI.

Para comenzar, primero cree una nueva carpeta para su proyecto de chatbot. Luego, abra la carpeta en su editor de texto y cree un archivo llamado `app.js`.

A continuación, deberá instalar el SDK de Bot Builder. Puedes hacer esto usando npm:

```
npm install botbuilder
```

Una vez que el SDK está instalado, puede importarlo a su archivo `app.js`:

```js
const builder = require('botbuilder');
```

¡Ahora estás listo para comenzar a codificar!

Primero, deberá crear un adaptador de bot. Esto se usará para conectar su chatbot a Microsoft Bot Framework. Puedes hacer esto con el siguiente código:

```js
const adapter = new builder.BotFrameworkAdapter();
```

A continuación, deberá crear un controlador de bot. Esto se usará para manejar los mensajes entrantes del usuario. Puedes hacer esto con el siguiente código:

```js
const bot = new builder.UniversalBot(adapter);
```

¡Ahora está listo para comenzar a agregar código a su controlador de bot!

Lo primero que deberá hacer es definir un cuadro de diálogo "Mensaje de bienvenida". Este cuadro de diálogo se utilizará para saludar al usuario y comenzar. Puedes hacer esto con el siguiente código:

```js
bot.dialog('WelcomeMessage', [
    (session) => {
        session.send("Hello! I'm a chatbot.");
        session.beginDialog('GetName');
    },
]);
```

Como puede ver, este cuadro de diálogo enviará un mensaje al usuario y luego iniciará el cuadro de diálogo `GetName`.

El cuadro de diálogo `GetName` se utilizará para obtener el nombre del usuario. Puedes hacer esto con el siguiente código:

```js
bot.dialog('GetName', [
    (session) => {
        builder.Prompts.text(session, "What's your name?");
    },
    (session, results) => {
        session.endDialog(`Hello, ${results.response}!`);
    },
]);
```

Como puede ver, este cuadro de diálogo solicitará al usuario su nombre y luego almacenará la respuesta en una variable llamada `resultados.respuesta`. Luego finalizará el diálogo y enviará un mensaje al usuario con su nombre.

¡Ahora estás listo para probar tu chatbot! Para hacer esto, deberá ejecutar el siguiente comando:

```
node app.js
```

¡Esto iniciará su chatbot y ahora puede hablar con él! Intenta decir "Hola" o "¿Cómo te llamas?" y ver lo que hace.

## Recursos

- [Microsoft Bot Framework] (https://dev.botframework.com/)
- [Servicio de bots de Azure](https://azure.microsoft.com/en-us/services/bot-service/)
- [SDK de Bot Builder](https://docs.microsoft.com/en-us/javascript/api/botbuilder-core/botbuilder-core-sdk?view=botbuilder-js-stable)