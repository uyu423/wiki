---
title: Primeros pasos con el desarrollo web: HTML, CSS y JavaScript
description: 
published: true
date: 2023-02-15T19:56:07.821Z
tags: 
editor: markdown
dateCreated: 2023-02-15T19:55:59.773Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Getting Started with Web Development: HTML, CSS, and JavaScript***English** document is available*](/en/Knowledge-base/Common/getting-started-with-web-development-html-css-and-javascript)
{.links-list}


# Primeros pasos con el desarrollo web: HTML, CSS y JavaScript

Internet se ha convertido en una parte integral de nuestras vidas. Lo usamos para todo, desde mantenernos en contacto con amigos y familiares hasta pagar nuestras cuentas y comprar nuestros alimentos. La World Wide Web ha recorrido un largo camino desde que se inventó por primera vez en 1989, y ahora es posible hacer casi cualquier cosa en línea.

Si alguna vez ha querido crear su propio sitio web o aplicación web, está de suerte. Con solo un poco de conocimiento, puede estar listo y funcionando en muy poco tiempo. En este artículo, lo guiaremos a través de los conceptos básicos del desarrollo web, desde elegir un entorno de desarrollo hasta escribir su primera línea de código. Al final, tendrá toda la información que necesita para comenzar su propio proyecto.

## ¿Qué es el desarrollo web?

El desarrollo web es el proceso de creación y mantenimiento de sitios web. Abarca todo, desde crear un sitio web desde cero hasta agregar nuevas funciones a un sitio existente.

El desarrollo web es un término amplio que se puede utilizar para describir una variedad de roles diferentes, como el diseño web, la ingeniería web y la gestión de contenido web. En general, los desarrolladores web son responsables de la codificación, el diseño y el diseño de un sitio web. También pueden participar en el desarrollo de aplicaciones web, que son programas que se ejecutan en un servidor web y a los que acceden los usuarios a través de un navegador web.

## Elegir un entorno de desarrollo

El primer paso para comenzar con el desarrollo web es elegir un entorno de desarrollo. Este es el software que utilizará para escribir su código y administrar su proyecto.

Hay algunas opciones diferentes disponibles, pero recomendamos usar [Visual Studio Code] (https://code.visualstudio.com/). Es un editor de código gratuito y de código abierto de Microsoft que está disponible para Windows, macOS y Linux. Tiene un excelente soporte para una variedad de lenguajes de programación, incluidos HTML, CSS y JavaScript.

Una vez que haya descargado e instalado Visual Studio Code, estará listo para comenzar a codificar.

## Escribiendo tu primera línea de código

El siguiente paso es escribir su primera línea de código. Para ello, vamos a utilizar un editor de texto sencillo como el Bloc de notas o TextEdit.

Abre tu editor de texto y escribe lo siguiente:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My first web page</title>
</head>
<body>
    <h1>Hello, world!</h1>
</body>
</html>
```

Este código crea una página web básica con un título y un solo elemento de encabezado. La declaración `<!DOCTYPE html>` le dice al navegador web que se trata de un documento HTML. Los elementos `<html>`, `<head>` y `<body>` son los componentes básicos de una página HTML. El elemento `<head>` contiene información sobre la página, como el título, y el elemento `<body>` contiene el contenido de la página.

El elemento `<h1>` es un elemento de encabezado y se usa para crear un encabezado en la página. En este caso, lo hemos usado para crear un encabezado que diga "¡Hola, mundo!".

Para guardar el archivo, seleccione Archivo > Guardar como en el menú y elija HTML en el menú desplegable de tipo de archivo. Nombra el archivo `index.html` y guárdalo en tu computadora.

## Visualización de su página web

Ahora que ha escrito su primera línea de código, es hora de ver su página web en un navegador web.

Para hacer esto, abra el archivo index.html que acaba de crear en su navegador web. Si usa Chrome, puede hacerlo seleccionando Archivo > Abrir archivo en el menú.

Deberías ver una página que se parece a esto:

![](https://i.imgur.com/JD7iK7I.png)

¡Felicidades! Acabas de crear tu primera página web.

## Agregando estilo con CSS

Ahora que ha creado una página web básica, es hora de agregar algo de estilo. CSS (hojas de estilo en cascada) es un lenguaje que se utiliza para diseñar documentos HTML. Con CSS, puede controlar el color, la fuente y el diseño de su página web.

Comencemos agregando un poco de color a nuestra página. Podemos hacer esto agregando una regla CSS a nuestra página.

Agrega el siguiente código al elemento `<head>` de tu documento HTML:

```css
<style>
    body {
        background-color: lightblue;
    }
</style>
```

Este código agrega una regla CSS que establece el color de fondo del elemento `<body>` en azul claro.

Guarde el archivo y actualice la página en su navegador web. Debería ver una página similar a esta:

![](https://i.imgur.com/eAoR3zJ.png)

Como puede ver, el fondo de la página ahora es azul claro.

## Agregar comportamiento con JavaScript

CSS se usa para diseñar documentos HTML, pero no agrega ningún comportamiento a la página. Para eso, necesitamos usar JavaScript.

JavaScript es un lenguaje de programación que se utiliza para agregar interactividad a las páginas web. Con JavaScript, puede crear cosas como menús desplegables, validación de formularios y efectos animados.

Agreguemos una función de JavaScript simple a nuestra página. Agrega el siguiente código al elemento `<body>` de tu documento HTML:

```javascript
<script>
    function sayHello() {
        alert("Hello, world!");
    }
</script>
```

Este código define una función llamada `sayHello()` que muestra un cuadro de alerta que dice "¡Hola, mundo!".

Ahora, necesitamos agregar un elemento a nuestra página que llamará a esta función cuando se haga clic en ella. Agrega el siguiente código al elemento `<body>` de tu documento HTML:

```html
<button onclick="sayHello()">Click me!</button>
```

Este código agrega un botón a la página que, cuando se hace clic, llamará a la función `sayHello()`.

Guarde el archivo y actualice la página en su navegador web. Debería ver un botón similar a este:

![](https://i.imgur.com/B6iU4TJ.png)

Haga clic en el botón y debería ver un cuadro de alerta similar a este:

![](https://i.imgur.com/cCk4Afe.png)

¡Felicidades! Acaba de agregar su primer bit de interactividad a su página web.

## A dónde ir desde aquí

Ahora que ha aprendido los conceptos básicos de HTML, CSS y JavaScript, está listo para comenzar a crear sus propias páginas web y aplicaciones web. Si desea obtener más información, le recomendamos que consulte algunos de los recursos a continuación.

- [W3Schools](https://www.w3schools.com/) - Un sitio web con tutoriales y referencias para tecnologías de desarrollo web
- [Red de desarrolladores de Mozilla](https://developer.mozilla.org/) - Un sitio web con tutoriales y referencias para tecnologías de desarrollo web
- [Code Academy](https://www.codecademy.com/) - Una plataforma interactiva en línea para aprender a codificar