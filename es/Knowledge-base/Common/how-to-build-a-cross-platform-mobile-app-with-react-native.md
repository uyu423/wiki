---
title: Cómo crear una aplicación móvil multiplataforma con React Native
description: 
published: true
date: 2023-02-07T23:17:33.623Z
tags: 
editor: markdown
dateCreated: 2023-02-07T23:17:27.859Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [How to Build a Cross-Platform Mobile App with React Native***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-cross-platform-mobile-app-with-react-native)
{.links-list}


# Cómo crear una aplicación móvil multiplataforma con React Native

El desarrollo de aplicaciones móviles es un tema candente en estos días. La demanda de aplicaciones móviles es más alta que nunca y el mercado está saturado con diferentes herramientas de desarrollo de aplicaciones. React Native es una herramienta popular para crear aplicaciones móviles multiplataforma.

Si es un desarrollador web que quiere ingresar al desarrollo de aplicaciones móviles, React Native es una excelente opción. En este artículo, le mostraremos cómo crear una aplicación React Native simple y cómo compilarla tanto para iOS como para Android.

## ¿Qué es React Native?

React Native es una herramienta de desarrollo de aplicaciones móviles multiplataforma desarrollada por Facebook. Le permite crear aplicaciones móviles de apariencia nativa usando JavaScript y React.

Las aplicaciones React Native no son aplicaciones web. Son aplicaciones nativas reales que están diseñadas para funcionar en una plataforma específica (iOS o Android).

## Configuración de su entorno de desarrollo

Antes de que podamos comenzar a desarrollar nuestra aplicación, debemos configurar nuestro entorno de desarrollo.

Si tiene una Mac, puede usar Xcode para el desarrollo de iOS y Android Studio para el desarrollo de Android.

Si está en Windows, puede usar Visual Studio para el desarrollo de iOS y Android.

Una vez que haya configurado su entorno de desarrollo, debe instalar React Native CLI.

Para hacer esto, abra una terminal y ejecute el siguiente comando:

```
npm install -g react-native-cli
```

## Creando una nueva aplicación React Native

Ahora que tenemos instalada la CLI de React Native, podemos usarla para crear una nueva aplicación de React Native.

Para hacer esto, abra una terminal y ejecute el siguiente comando:

```
react-native init my-app
```

Esto creará un nuevo directorio llamado `my-app` en su directorio actual. Este directorio contendrá todos los archivos para su nueva aplicación React Native.

## Ejecutando tu aplicación

Ahora que hemos creado nuestra nueva aplicación, podemos ejecutarla en nuestro dispositivo.

Para hacer esto, abra una terminal y navegue hasta el directorio `my-app`. Luego, ejecuta el siguiente comando:

```
react-native run-ios
```

Esto creará y ejecutará su aplicación en un simulador de iOS. Si está en Windows, puede usar el comando `react-native run-android` para ejecutar su aplicación en un simulador de Android.

## Creando tu primer componente React Native

Ahora que tenemos nuestra aplicación ejecutándose, creemos nuestro primer componente React Native.

Abra `index.ios.js` (o `index.android.js` si está en Windows) en su editor de texto y reemplace el contenido del archivo con lo siguiente:

```javascript
import React, { Component } from 'react';
import {
  AppRegistry,
  Text,
  View
} from 'react-native';

export default class my-app extends Component {
  render() {
    return (
      <View>
        <Text>Hello, world!</Text>
      </View>
    );
  }
}

AppRegistry.registerComponent('my-app', () => my-app);
```

Este es un componente React simple que representa un elemento `<Text>`.

## Terminando

En este artículo, le mostramos cómo crear una aplicación React Native simple y cómo compilarla tanto para iOS como para Android.

React Native es una gran herramienta para crear aplicaciones móviles multiplataforma. Si es un desarrollador web que quiere ingresar al desarrollo de aplicaciones móviles, React Native es una excelente opción.