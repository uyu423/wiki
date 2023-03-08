---
title: Getting Started with Web Development: HTML, CSS, and JavaScript
description: 
published: true
date: 2023-02-15T19:56:01.680Z
tags: 
editor: markdown
dateCreated: 2023-02-15T19:55:59.774Z
---

- [Primeros pasos con el desarrollo web: HTML, CSS y JavaScript***Spanish** document is available*](/es/Knowledge-base/Common/getting-started-with-web-development-html-css-and-javascript)
{.links-list}
- [Web 开发入门：HTML、CSS 和 JavaScript***Chinese Simplified** document is available*](/zh/Knowledge-base/Common/getting-started-with-web-development-html-css-and-javascript)
{.links-list}
- [웹 개발 시작하기: HTML, CSS 및 JavaScript***Korean** document is available*](/ko/Knowledge-base/Common/getting-started-with-web-development-html-css-and-javascript)
{.links-list}


# Getting Started with Web Development: HTML, CSS, and JavaScript

The internet has become an integral part of our lives. We use it for everything from keeping in touch with friends and family to paying our bills and buying our groceries. The World Wide Web has come a long way since it was first invented in 1989, and it’s now possible to do almost anything online.

If you’ve ever wanted to create your own website or web application, you’re in luck. With just a little bit of know-how, you can be up and running in no time. In this article, we’ll take you through the basics of web development, from choosing a development environment to writing your first line of code. By the end, you’ll have all the information you need to get started on your own project.

## What is web development?

Web development is the process of creating and maintaining websites. It encompasses everything from building a website from scratch to adding new features to an existing site.

Web development is a broad term that can be used to describe a variety of different roles, such as web design, web engineering, and web content management. In general, web developers are responsible for the coding, design, and layout of a website. They may also be involved in the development of web applications, which are programs that run on a web server and are accessed by users through a web browser.

## Choosing a development environment

The first step in getting started with web development is to choose a development environment. This is the software that you’ll use to write your code and manage your project.

There are a few different options available, but we recommend using [Visual Studio Code](https://code.visualstudio.com/). It’s a free and open-source code editor from Microsoft that’s available for Windows, macOS, and Linux. It has excellent support for a variety of programming languages, including HTML, CSS, and JavaScript.

Once you’ve downloaded and installed Visual Studio Code, you’re ready to start coding.

## Writing your first line of code

The next step is to write your first line of code. For this, we’re going to use a simple text editor like Notepad or TextEdit.

Open your text editor and type the following:

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

This code creates a basic web page with a title and a single header element. The `<!DOCTYPE html>` declaration tells the web browser that this is an HTML document. The `<html>`, `<head>`, and `<body>` elements are the basic building blocks of an HTML page. The `<head>` element contains information about the page, such as the title, and the `<body>` element contains the page’s content.

The `<h1>` element is a heading element, and it’s used to create a heading on the page. In this case, we’ve used it to create a heading that says “Hello, world!”.

To save the file, select File > Save As from the menu and choose HTML from the file type drop-down menu. Name the file `index.html` and save it to your computer.

## Viewing your web page

Now that you’ve written your first line of code, it’s time to view your web page in a web browser.

To do this, open the index.html file you just created in your web browser. If you’re using Chrome, you can do this by selecting File > Open File from the menu.

You should see a page that looks something like this:

![](https://i.imgur.com/JD7iK7I.png)

Congratulations! You’ve just created your first web page.

## Adding style with CSS

Now that you’ve created a basic web page, it’s time to add some style. CSS (Cascading Style Sheets) is a language that’s used to style HTML documents. With CSS, you can control the color, font, and layout of your web page.

Let’s start by adding a bit of color to our page. We can do this by adding a CSS rule to our page.

Add the following code to the `<head>` element of your HTML document:

```css
<style>
    body {
        background-color: lightblue;
    }
</style>
```

This code adds a CSS rule that sets the background color of the `<body>` element to light blue.

Save the file and refresh the page in your web browser. You should see a page that looks like this:

![](https://i.imgur.com/eAoR3zJ.png)

As you can see, the background of the page is now light blue.

## Adding behavior with JavaScript

CSS is used to style HTML documents, but it doesn’t add any behavior to the page. For that, we need to use JavaScript.

JavaScript is a programming language that’s used to add interactivity to web pages. With JavaScript, you can create things like drop-down menus, form validation, and animated effects.

Let’s add a simple JavaScript function to our page. Add the following code to the `<body>` element of your HTML document:

```javascript
<script>
    function sayHello() {
        alert("Hello, world!");
    }
</script>
```

This code defines a function called `sayHello()` that displays an alert box that says “Hello, world!”.

Now, we need to add an element to our page that will call this function when it’s clicked. Add the following code to the `<body>` element of your HTML document:

```html
<button onclick="sayHello()">Click me!</button>
```

This code adds a button to the page that, when clicked, will call the `sayHello()` function.

Save the file and refresh the page in your web browser. You should see a button that looks like this:

![](https://i.imgur.com/B6iU4TJ.png)

Click the button, and you should see an alert box that looks like this:

![](https://i.imgur.com/cCk4Afe.png)

Congratulations! You’ve just added your first bit of interactivity to your web page.

## Where to go from here

Now that you’ve learned the basics of HTML, CSS, and JavaScript, you’re ready to start creating your own web pages and web applications. If you want to learn more, we recommend checking out some of the resources below.

- [W3Schools](https://www.w3schools.com/) - A website with tutorials and references for web development technologies
- [Mozilla Developer Network](https://developer.mozilla.org/) - A website with tutorials and references for web development technologies
- [Code Academy](https://www.codecademy.com/) - An online interactive platform for learning to code