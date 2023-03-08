---
title: Desarrollo de Software 007: HTML, CSS y JavaScript
description: 
published: true
date: 2023-02-10T03:17:47.913Z
tags: 
editor: markdown
dateCreated: 2023-02-10T03:17:41.584Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Software Development 007: HTML, CSS and JavaScript***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-007-html-css-and-javascript)
{.links-list}


# Desarrollo de Software 007: HTML, CSS y JavaScript

Los fundamentos del desarrollo web consisten en tres tecnologías: HTML, CSS y JavaScript. En esta publicación, cubriremos los conceptos básicos de cada tecnología.

## HTML

HTML, o HyperText Markup Language, es el lenguaje de marcado estándar para documentos en la World Wide Web. Los elementos HTML son los componentes básicos de las páginas HTML.

### Sintaxis HTML básica

Un elemento HTML consta de una etiqueta de inicio, contenido y una etiqueta de finalización. La etiqueta de inicio está encerrada entre corchetes angulares y la etiqueta final también está encerrada entre corchetes angulares, pero incluye una barra inclinada antes del nombre del elemento.

Por ejemplo, el elemento `<p>` representa un párrafo de texto. La etiqueta de inicio `<p>` le dice al navegador web que el contenido adjunto es un párrafo, y la etiqueta de fin `</p>` le dice al navegador web que el párrafo ha terminado.

He aquí un ejemplo de un elemento de párrafo:

```html
<p>This is a paragraph of text.</p>
```

La mayoría de los elementos HTML pueden tener atributos, que se utilizan para proporcionar información adicional sobre el elemento. Los atributos se especifican en la etiqueta de inicio y normalmente se componen de un nombre y un valor, separados por un signo igual.

Por ejemplo, el elemento `<a>`, que representa un hipervínculo, tiene un atributo `href`, que especifica la URL de la página a la que se dirige el enlace.

Este es un ejemplo de un elemento de hipervínculo:

```html
<a href="https://www.example.com/">This is a link to an external website.</a>
```

### El elemento `<cabeza>`

El elemento `<head>` contiene información sobre el documento, como el título del documento, y se usa para cargar recursos externos, como hojas de estilo CSS y archivos JavaScript.

Aquí hay un ejemplo del elemento `<head>`:

```html
<head>
    <title>This is the document's title</title>
    <link rel="stylesheet" href="styles.css">
    <script src="script.js"></script>
</head>
```

### El elemento `<cuerpo>`

El elemento `<body>` contiene el contenido del documento, que se muestra en el navegador web.

Aquí hay un ejemplo del elemento `<body>`:

```html
<body>
    <!-- This is a comment -->
    <h1>This is a heading</h1>
    <p>This is a paragraph of text.</p>
    <ul>
        <li>This is a list item</li>
        <li>This is another list item</li>
    </ul>
</body>
```

## CSS

CSS, u hojas de estilo en cascada, es un lenguaje de hojas de estilo utilizado para describir la presentación de un documento escrito en un lenguaje de marcas. CSS se utiliza para diseñar todas las etiquetas HTML, incluidos los elementos `<body>`, `<head>` y `<html>` del documento.

Las reglas CSS se componen de selectores y declaraciones. Se utiliza un selector para especificar los elementos HTML a los que se aplica la regla CSS. Se utiliza una declaración para especificar las propiedades y los valores de CSS que se aplican a los elementos HTML especificados por el selector.

Las declaraciones CSS se componen de una propiedad y un valor, separados por dos puntos. Las declaraciones múltiples se pueden separar con un punto y coma.

Aquí hay un ejemplo de una regla CSS:

```css
p {
    color: red;
    font-size: 16px;
}
```

Esta regla CSS hará que todos los elementos `<p>` tengan un color rojo y un tamaño de fuente de 16px.

Las reglas CSS se pueden colocar en el elemento `<head>` de un documento HTML, en un archivo CSS separado o en línea dentro de un elemento HTML.

Aquí hay un ejemplo de un documento HTML con una regla CSS en línea:

```html
<html>
<head>
    <title>This is the document's title</title>
</head>
<body>
    <h1 style="color: red;">This is a heading</h1>
    <p>This is a paragraph of text.</p>
</body>
</html>
```

## JavaScript

JavaScript es un lenguaje de programación que se utiliza para hacer que las páginas web sean interactivas. El código JavaScript se puede colocar en el elemento `<head>` de un documento HTML, en un archivo JavaScript separado o en línea dentro de un elemento HTML.

Aquí hay un ejemplo de un documento HTML con un JavaScript en línea:

```html
<html>
<head>
    <title>This is the document's title</title>
</head>
<body>
    <button onclick="alert('This is an alert')">Click me!</button>
</body>
</html>
```

En este ejemplo, cuando se hace clic en el botón, aparecerá un cuadro de alerta con el texto "Esta es una alerta".

El código JavaScript también se puede usar para cambiar dinámicamente el contenido y el estilo de un documento HTML.

Aquí hay un ejemplo de JavaScript que cambia el texto de un elemento `<h1>`:

```html
<html>
<head>
    <title>This is the document's title</title>
</head>
<body>
    <h1 id="heading">This is a heading</h1>
    <script>
    document.getElementById("heading").innerHTML = "This is a new heading";
    </script>
</body>
</html>
```

En este ejemplo, el texto del elemento `<h1>` se cambia de "Este es un encabezado" a "Este es un nuevo encabezado" cuando se carga la página.

## Información adicional

- Para obtener más información sobre HTML, CSS y JavaScript, consulte los siguientes recursos:

    - [La especificación HTML del W3C](https://www.w3.org/TR/html/)
    - [La especificación CSS del W3C](https://www.w3.org/TR/CSS/)
    - [La especificación JavaScript del W3C](https://www.w3.org/TR/javascript/)
    - [Documentación HTML de Mozilla Developer Network] (https://developer.mozilla.org/en-US/docs/Web/HTML)
    - [Documentación CSS de Mozilla Developer Network] (https://developer.mozilla.org/en-US/docs/Web/CSS)
    - [Documentación de JavaScript de Mozilla Developer Network] (https://developer.mozilla.org/en-US/docs/Web/JavaScript)

## Advertencias

- No use el elemento `<script>` para cargar archivos JavaScript externos. Use el elemento `<script>` solo para el código JavaScript en línea.

## Peligros

- No use HTML, CSS o JavaScript para cargar archivos externos.