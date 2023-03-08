---
title: Desarrollo de chatbots con Microsoft Bot Framework
description: 
published: true
date: 2023-02-12T19:18:22.632Z
tags: 
editor: markdown
dateCreated: 2023-02-12T19:18:20.750Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Developing Chatbots with Microsoft Bot Framework***English** document is available*](/en/Knowledge-base/Common/developing-chatbots-with-microsoft-bot-framework)
{.links-list}


# Desarrollo de chatbots con Microsoft Bot Framework

El desarrollo de chatbots se ha convertido en un tema candente en la industria de TI a medida que más empresas buscan formas de automatizar las interacciones con los clientes. Microsoft Bot Framework es una de las plataformas líderes para crear chatbots y ofrece un conjunto de herramientas y servicios fáciles de usar que permiten a los desarrolladores crear bots que pueden interactuar con los usuarios de forma natural.

En este artículo, veremos lo que se necesita para desarrollar chatbots usando Microsoft Bot Framework. Comenzaremos observando los diferentes componentes del marco y cómo funcionan juntos. Luego, analizaremos algunos ejemplos de código para mostrarle cómo comenzar a crear sus propios chatbots.

## ¿Qué es Microsoft Bot Framework?

Microsoft Bot Framework es un conjunto de herramientas y servicios que ayudan a los desarrolladores a crear chatbots para una variedad de plataformas, incluidas Facebook Messenger, Skype, Slack y más. El marco incluye un SDK de Bot Builder, que proporciona un conjunto de API para crear bots y un conjunto de herramientas y servicios para administrar conversaciones de bots.

El SDK de Bot Builder permite a los desarrolladores crear bots que puedan comprender el lenguaje natural. El SDK incluye un conjunto de herramientas para crear bots, incluido un sistema de diálogo, un conjunto de herramientas de procesamiento de lenguaje natural y un conjunto de herramientas para administrar conversaciones de bots.

El SDK también incluye un conjunto de API para integrar bots con una variedad de servicios, incluidos Facebook Messenger, Skype, Slack y más.

## Cómo funciona Microsoft Bot Framework

Microsoft Bot Framework funciona al permitir que los desarrolladores creen bots que puedan entender el lenguaje natural. El marco incluye un conjunto de herramientas para crear bots, incluido un sistema de diálogo, un conjunto de herramientas de procesamiento de lenguaje natural y un conjunto de herramientas para administrar conversaciones de bots.

El marco también incluye un conjunto de API para integrar bots con una variedad de servicios, incluidos Facebook Messenger, Skype, Slack y más.

## Primeros pasos con Microsoft Bot Framework

Ahora que hemos analizado qué es Microsoft Bot Framework y cómo funciona, comencemos con algunos ejemplos de código.

Lo primero que deberá hacer es crear un nuevo proyecto de Microsoft Bot Framework. Puede hacerlo con el generador Yeoman de Microsoft Bot Framework.

Para instalar el generador, deberá tener Node.js y Yeoman instalados en su máquina. Para instalar Node.js, diríjase al sitio web de Node.js y descargue el instalador para su sistema operativo.

Una vez que Node.js está instalado, puede instalar el generador Yeoman usando el siguiente comando:

```
npm install -g yo generator-botframework
```

Una vez que el generador está instalado, puede crear un nuevo proyecto usando el siguiente comando:

```
yo botframework
```

Se le pedirá que ingrese algunos detalles sobre su proyecto, incluidos el nombre, la descripción y la versión.

Una vez que se genera su proyecto, deberá instalar las dependencias. Para hacer esto, dirígete al directorio del proyecto y ejecuta el siguiente comando:

```
npm install
```

Una vez instaladas las dependencias, puede comenzar a desarrollar su chatbot.

## Desarrollando tu chatbot

Microsoft Bot Framework viene con un conjunto de herramientas y servicios que facilitan el desarrollo de chatbots. En esta sección, veremos cómo usar los diferentes componentes del marco para desarrollar su chatbot.

### El SDK del creador de bots

El SDK de Bot Builder es un conjunto de herramientas que le permiten crear bots que pueden comprender el lenguaje natural. El SDK incluye un sistema de diálogo, un conjunto de herramientas de procesamiento de lenguaje natural y un conjunto de herramientas para administrar conversaciones de bots.

Para comenzar con el SDK, deberá crear un nuevo archivo en el directorio raíz de su proyecto. El archivo debe llamarse `bot.js`.

En el archivo `bot.js`, deberá solicitar el módulo `botbuilder` y crear una nueva instancia de `BotBuilder`.

```javascript
var builder = require('botbuilder');

var bot = new builder.BotBuilder();
```

### El sistema de diálogo

El sistema de diálogo es el corazón del SDK de Bot Builder. Te permite definir el flujo de conversación entre el usuario y el chatbot.

El sistema de diálogo se basa en el concepto de diálogos. Un diálogo es una unidad de conversación entre el usuario y el chatbot. Los diálogos se pueden anidar, lo que significa que un diálogo puede contener otros diálogos.

Para crear un cuadro de diálogo, deberá crear un nuevo archivo en el directorio `/dialogs` de su proyecto. El archivo debe llamarse `{dialog_name}.js`.

En el archivo `{dialog_name}.js`, deberá solicitar el módulo `botbuilder` y crear una nueva instancia `Dialog`.

```javascript
var builder = require('botbuilder');

var dialog = new builder.Dialog();
```

Una vez que tenga una instancia de `Dialog`, puede definir el flujo de conversación agregando diálogos a la propiedad `stack`.

```javascript
dialog.stack(
    // First dialog in the stack
    function (session, args, next) {
        // Do something here
    },
    // Second dialog in the stack
    function (session, args, next) {
        // Do something here
    }
);
```

También puede agregar cuadros de diálogo a la propiedad `stack` usando el método `addDialog`.

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
});
```

El método `addDialog` acepta una función `onSelector`, que le permite especificar cuándo debe ejecutarse el diálogo. La función `onSelector` debería devolver `true` cuando el cuadro de diálogo debería ejecutarse y `false` cuando no debería.

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
}, function (session, args) {
    // Return true when the dialog should be executed
    return true;
});
```

El método `addDialog` también acepta una función `onReject`, que le permite especificar qué debería suceder si el diálogo no se ejecuta. La función `onReject` debe devolver una `Promesa` que se resuelve con el valor que debe pasarse al siguiente diálogo en la pila.

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
}, function (session, args) {
    // Return false when the dialog should not be executed
    return false;
}, function (session, args) {
    // Return a Promise that resolves with the value that should be passed to the next dialog
    return Promise.resolve('some-value');
});
```

El método `addDialog` también acepta una función `onPost`, que le permite especificar lo que debería suceder después de que se haya ejecutado el diálogo. La función `onPost` debe devolver una `Promesa` que se resuelve con el valor que se debe pasar al siguiente diálogo en la pila.

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
}, function (session, args) {
    // Return true when the dialog should be executed
    return true;
}, function (session, args) {
    // Return a Promise that resolves with the value that should be passed to the next dialog
    return Promise.resolve('some-value');
});
```

### Las herramientas de procesamiento del lenguaje natural

El SDK de Bot Builder incluye un conjunto de herramientas para procesar el lenguaje natural. Estas herramientas se pueden usar para comprender la intención del usuario, extraer entidades de la entrada del usuario y más.

Las herramientas de procesamiento de lenguaje natural se basan en las clases `LuisRecognizer` y `QnAMakerRecognizer`.

Para utilizar las herramientas de procesamiento de lenguaje natural, deberá crear un nuevo archivo en el directorio `/recognizers` de su proyecto. El archivo debe llamarse `{recognizer_name}.js`.

En el archivo `{recognizer_name}.js`, deberá solicitar el módulo `botbuilder` y crear una nueva instancia `LuisRecognizer` o `QnAMakerRecognizer`.

```javascript
var builder = require('botbuilder');

var recognizer = new builder.LuisRecognizer();
```

Una vez que tenga una instancia de `LuisRecognizer` o `QnAMakerRecognizer`, puede usar el método `recognize` para procesar la entrada del usuario.

```javascript
recognizer.recognize('What is your name?', function (err, result) {
    // Handle the result here
});
```

El método `recognize` acepta una función `callback`, que se llama con los resultados del reconocimiento. A la función `callback` se le pasan dos argumentos: `err` y `result`.

El argumento `err` es un objeto de error que se pasa si se produce un error durante el reconocimiento.

El argumento `resultado` es un objeto que contiene los resultados del reconocimiento. El objeto tiene las siguientes propiedades:

- `intento`: El nombre del intento que fue reconocido.
- `puntuación`: Una puntuación de confianza entre 0 y 1.
- `entidades`: un objeto que contiene las entidades que se extrajeron de la entrada del usuario.

### Las herramientas para administrar conversaciones de bots

El SDK de Bot Builder incluye un conjunto de herramientas para administrar conversaciones de bot. Estas herramientas se pueden usar para enviar mensajes al usuario, finalizar la conversación y más.

Para usar las herramientas para administrar conversaciones de bots, deberá solicitar el módulo `botbuilder` y crear una nueva instancia de `ConversationBot`.

```javascript
var builder = require('botbuilder');

var bot = new builder.ConversationBot();
```

Una vez que tenga una instancia de `ConversationBot`, puede usar el método `message` para enviar un mensaje al usuario.

```javascript
bot.message('Hello, world!');
```

El método `mensaje` acepta un argumento `texto`, que es el mensaje que debe enviarse al usuario, y una función `devolución de llamada`, que se llama cuando se ha enviado el mensaje.

También puede usar el método `endConversation` para finalizar la conversación.

```javascript
bot.endConversation();
```

El método `endConversation` no acepta ningún argumento.

## Implementación de su chatbot

Una vez que haya desarrollado su chatbot, deberá implementarlo en un servidor para que los usuarios puedan usarlo.

Microsoft Bot Framework viene con un conjunto de herramientas y servicios para implementar chatbots. El marco incluye un servicio Bot Connector, que le permite conectar su chatbot a una variedad de plataformas de chat, incluidas Facebook Messenger, Skype, Slack y más.

Para implementar su chatbot, primero deberá crear un nuevo archivo en el directorio raíz de su proyecto. El archivo debe llamarse `.env`.

En el archivo `.env`, deberá agregar las siguientes variables de entorno:

- `PORT`: El puerto en el que se ejecutará su chatbot.
- `MICROSOFT_APP_ID`: Su ID de aplicación de Microsoft.
- `MICROSOFT_APP_PASSWORD`: Su contraseña de aplicación de Microsoft.

Una vez que haya agregado las variables de entorno al archivo `.env`, puede iniciar el chatbot con el siguiente comando:

```
npm start
```

Su chatbot ahora se ejecutará en el puerto especificado en la variable de entorno `PORT`.

## Conclusión

En este artículo, analizamos lo que se necesita para desarrollar chatbots utilizando Microsoft Bot Framework. Hemos analizado los diferentes componentes del marco y cómo funcionan juntos. También hemos visto algunos ejemplos de código de cómo comenzar a crear sus propios chatbots.