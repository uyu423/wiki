---
title: 064: Chatbots en tiempo real con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T22:04:38.124Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:04:36.504Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [064: Real-Time Chatbots with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/064-real-time-chatbots-with-tensorflow-js-and-node-js)
{.links-list}


# Chatbots en tiempo real con TensorFlow.js y Node.js

En esta publicación, veremos cómo crear chatbots en tiempo real usando TensorFlow.js y Node.js. Usaremos un modelo previamente entrenado para construir nuestro chatbot y lo implementaremos en una plataforma sin servidor para que pueda manejar múltiples usuarios simultáneos.

## ¿Qué es un chatbot?

Un chatbot es un programa informático que simula una conversación humana. Los chatbots se utilizan en una variedad de contextos, incluidos el servicio al cliente, el marketing y el entretenimiento.

## ¿Por qué usar TensorFlow.js?

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. Es de código abierto y multiplataforma, y se puede usar en un navegador o en un entorno Node.js.

## ¿Qué es Node.js?

Node.js es un entorno de tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript fuera de un navegador. Node.js se utiliza para desarrollar aplicaciones del lado del servidor.

## Requisitos previos

Esta publicación asume que tiene una comprensión básica de JavaScript y Node.js. Si es nuevo en estas tecnologías, puede consultar los siguientes recursos:

- [Tutorial de JavaScript](https://www.w3schools.com/js/)
- [Tutorial de Node.js](https://nodejs.org/en/docs/guides/guía-de-primeros-inicios/)

## Empezando

### 1. Crear un nuevo proyecto Node.js

Comencemos por crear un nuevo proyecto de Node.js. Usaremos el marco web [Express](https://expressjs.com/), así que asegúrese de instalarlo también:

```
npm init
npm install express --save
```

### 2. Entrena a tu modelo

A continuación, necesitamos entrenar un modelo de aprendizaje automático que pueda ser utilizado por nuestro chatbot. Para esta publicación, usaremos un modelo previamente entrenado del [Zoológico de modelos de TensorFlow.js](https://js.tensorflow.org/tutorials/training-chatbot.html).

Puede entrenar su propio modelo o usar uno previamente entrenado. Si desea entrenar su propio modelo, deberá proporcionar un conjunto de datos de conversación. El Model Zoo de TensorFlow.js proporciona algunos conjuntos de datos diferentes que puede usar.

Una vez que haya seleccionado un conjunto de datos, puede usar [TensorFlow.js Model Maker](https://js.tensorflow.org/tutorials/model-maker.html) para entrenar su modelo.

### 3. Implementa tu modelo

Ahora que tenemos un modelo entrenado, debemos implementarlo para que nuestro chatbot pueda usarlo. Usaremos el [TensorFlow.js Model Server](https://js.tensorflow.org/tutorials/serving-models.html) para esto.

TensorFlow.js Model Server es una aplicación de Node.js que se puede implementar en cualquier plataforma. Le permite servir modelos TensorFlow.js y proporciona una API REST para la inferencia.

### 4. Implementa tu chatbot

Ahora que nuestro modelo está implementado, podemos comenzar a implementar nuestro chatbot. Usaremos la biblioteca [Botkit](https://botkit.ai/) para hacer esto.

Botkit es una biblioteca de Node.js que facilita la creación de bots para Slack, Facebook Messenger y otras plataformas de chat.

Primero, necesitamos instalar Botkit:

```
npm install botkit --save
```

Luego, podemos crear un archivo llamado `chatbot.js` y agregar el siguiente código:

```javascript
const Botkit = require('botkit');

const controller = Botkit.slackbot({
  debug: false,
});

controller.spawn({
  token: process.env.SLACK_BOT_TOKEN,
}).startRTM();

controller.hears('hello', ['direct_message', 'direct_mention', 'mention'], (bot, message) => {
  bot.reply(message, 'Hi there!');
});
```

Este código crea un bot de Slack que responde al comando `hola`.

### 5. Implementa tu chatbot

Ahora que nuestro chatbot está implementado, debemos implementarlo. Usaremos [Ahora] (https://zeit.co/now) para esto.

Now es una plataforma sin servidor que facilita la implementación de aplicaciones Node.js. Se ocupa de la infraestructura, para que pueda concentrarse en su código.

Primero, necesitamos crear una cuenta Now e instalar Now CLI:

```
npm install -g now
```

Luego, podemos implementar nuestro chatbot usando el siguiente comando:

```
now --env SLACK_BOT_TOKEN=your-bot-token
```

Esto desplegará nuestro chatbot y nos proporcionará una URL que podemos usar para acceder a él.

## Conclusión

En esta publicación, hemos visto cómo crear chatbots en tiempo real usando TensorFlow.js y Node.js. Hemos entrenado un modelo de aprendizaje automático y lo hemos implementado en una plataforma sin servidor. También implementamos un chatbot usando la biblioteca Botkit.