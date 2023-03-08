---
title: Software Development 007: HTML, CSS and JavaScript
description: 
published: true
date: 2023-02-10T03:17:43.313Z
tags: 
editor: markdown
dateCreated: 2023-02-10T03:17:41.588Z
---

- [Desarrollo de Software 007: HTML, CSS y JavaScript***Spanish** document is available*](/es/Knowledge-base/Software-Development/Learning/software-development-007-html-css-and-javascript)
{.links-list}
- [软件开发 007：HTML、CSS 和 JavaScript***Chinese Simplified** document is available*](/zh/Knowledge-base/Software-Development/Learning/software-development-007-html-css-and-javascript)
{.links-list}
- [소프트웨어 개발 007: HTML, CSS 및 JavaScript***Korean** document is available*](/ko/Knowledge-base/Software-Development/Learning/software-development-007-html-css-and-javascript)
{.links-list}


# Software Development 007: HTML, CSS and JavaScript

The basics of web development consist of three technologies: HTML, CSS, and JavaScript. In this post, we'll cover the basics of each technology.

## HTML

HTML, or HyperText Markup Language, is the standard markup language for documents on the World Wide Web. HTML elements are the building blocks of HTML pages.

### Basic HTML Syntax

An HTML element is consists of a start tag, content, and an end tag. The start tag is enclosed in angle brackets, and the end tag is also enclosed in angle brackets but includes a forward slash before the element name.

For example, the `<p>` element represents a paragraph of text. The `<p>` start tag tells the web browser that the enclosed content is a paragraph, and the `</p>` end tag tells the web browser that the paragraph has ended.

Here's an example of a paragraph element:

```html
<p>This is a paragraph of text.</p>
```

Most HTML elements can have attributes, which are used to provide additional information about the element. Attributes are specified in the start tag and are usually made up of a name and a value, separated by an equals sign.

For example, the `<a>` element, which represents a hyperlink, has an `href` attribute, which specifies the URL of the page that the link goes to.

Here's an example of a hyperlink element:

```html
<a href="https://www.example.com/">This is a link to an external website.</a>
```

### The `<head>` Element

The `<head>` element contains information about the document, such as the document's title, and is used to load external resources, such as CSS stylesheets and JavaScript files.

Here's an example of the `<head>` element:

```html
<head>
    <title>This is the document's title</title>
    <link rel="stylesheet" href="styles.css">
    <script src="script.js"></script>
</head>
```

### The `<body>` Element

The `<body>` element contains the document's content, which is displayed by the web browser.

Here's an example of the `<body>` element:

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

CSS, or Cascading Style Sheets, is a style sheet language used for describing the presentation of a document written in a markup language. CSS is used to style all HTML tags, including the document's `<body>`, `<head>`, and `<html>` elements.

CSS rules are made up of selectors and declarations. A selector is used to specify the HTML element(s) that the CSS rule applies to. A declaration is used to specify the CSS properties and values that are applied to the HTML element(s) specified by the selector.

CSS declarations are made up of a property and a value, separated by a colon. Multiple declarations can be separated by a semicolon.

Here's an example of a CSS rule:

```css
p {
    color: red;
    font-size: 16px;
}
```

This CSS rule will make all `<p>` elements have a red color and a font size of 16px.

CSS rules can be placed in the `<head>` element of an HTML document, in a separate CSS file, or inline within an HTML element.

Here's an example of an HTML document with an inline CSS rule:

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

JavaScript is a programming language that is used to make web pages interactive. JavaScript code can be placed in the `<head>` element of an HTML document, in a separate JavaScript file, or inline within an HTML element.

Here's an example of an HTML document with an inline JavaScript:

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

In this example, when the button is clicked, an alert box will appear with the text "This is an alert."

JavaScript code can also be used to dynamically change the content and style of an HTML document.

Here's an example of a JavaScript that changes the text of an `<h1>` element:

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

In this example, the text of the `<h1>` element is changed from "This is a heading" to "This is a new heading" when the page is loaded.

## Additional Information

- For more information about HTML, CSS, and JavaScript, check out the following resources:

    - [The W3C's HTML specification](https://www.w3.org/TR/html/)
    - [The W3C's CSS specification](https://www.w3.org/TR/CSS/)
    - [The W3C's JavaScript specification](https://www.w3.org/TR/javascript/)
    - [Mozilla Developer Network's HTML documentation](https://developer.mozilla.org/en-US/docs/Web/HTML)
    - [Mozilla Developer Network's CSS documentation](https://developer.mozilla.org/en-US/docs/Web/CSS)
    - [Mozilla Developer Network's JavaScript documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

## Warnings

- Do not use the `<script>` element to load external JavaScript files. Use the `<script>` element only to inline JavaScript code.

## Dangers

- Do not use HTML, CSS, or JavaScript to load external files.