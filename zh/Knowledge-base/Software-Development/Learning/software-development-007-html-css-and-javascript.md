---
title: 软件开发 007：HTML、CSS 和 JavaScript
description: 
published: true
date: 2023-02-10T03:17:47.913Z
tags: 
editor: markdown
dateCreated: 2023-02-10T03:17:41.581Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Software Development 007: HTML, CSS and JavaScript***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-007-html-css-and-javascript)
{.links-list}


# 软件开发 007：HTML、CSS 和 JavaScript

Web 开发的基础包括三种技术：HTML、CSS 和 JavaScript。在本文中，我们将介绍每种技术的基础知识。

## HTML

HTML 或超文本标记语言是万维网上文档的标准标记语言。 HTML 元素是 HTML 页面的构建块。

### 基本 HTML 语法

HTML 元素由开始标记、内容和结束标记组成。开始标记包含在尖括号中，结束标记也包含在尖括号中，但在元素名称前包含一个正斜杠。

例如，`<p>` 元素表示一段文本。 `<p>` 开始标签告诉网络浏览器包含的内容是一个段落，`</p>` 结束标签告诉网络浏览器该段落已经结束。

下面是段落元素的示例：

```html
<p>This is a paragraph of text.</p>
```

大多数 HTML 元素都可以具有属性，这些属性用于提供有关该元素的附加信息。属性在开始标记中指定，通常由名称和值组成，用等号分隔。

例如，代表超链接的 `<a>` 元素有一个 `href` 属性，它指定链接指向的页面的 URL。

下面是一个超链接元素的示例：

```html
<a href="https://www.example.com/">This is a link to an external website.</a>
```

### `<head>` 元素

`<head>` 元素包含有关文档的信息，例如文档的标题，并用于加载外部资源，例如 CSS 样式表和 JavaScript 文件。

以下是 `<head>` 元素的示例：

```html
<head>
    <title>This is the document's title</title>
    <link rel="stylesheet" href="styles.css">
    <script src="script.js"></script>
</head>
```

### `<body>` 元素

`<body>` 元素包含文档的内容，由网络浏览器显示。

以下是 `<body>` 元素的示例：

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

CSS，即层叠样式表，是一种样式表语言，用于描述以标记语言编写的文档的呈现方式。 CSS 用于设置所有 HTML 标签的样式，包括文档的“<body>”、“<head>”和“<html>”元素。

CSS 规则由选择器和声明组成。选择器用于指定 CSS 规则适用的 HTML 元素。声明用于指定应用于由选择器指定的 HTML 元素的 CSS 属性和值。

CSS 声明由属性和值组成，以冒号分隔。多个声明可以用分号分隔。

下面是一个 CSS 规则的例子：

```css
p {
    color: red;
    font-size: 16px;
}
```

此 CSS 规则将使所有 `<p>` 元素都具有红色和 16px 的字体大小。

CSS 规则可以放置在 HTML 文档的“<head>”元素中、单独的 CSS 文件中或内嵌在 HTML 元素中。

下面是一个带有内联 CSS 规则的 HTML 文档示例：

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

JavaScript 是一种用于使网页具有交互性的编程语言。 JavaScript 代码可以放在 HTML 文档的“<head>”元素中、单独的 JavaScript 文件中，或者内嵌在 HTML 元素中。

下面是一个带有内联 JavaScript 的 HTML 文档示例：

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

在此示例中，当单击该按钮时，将出现一个带有文本“This is an alert”的警告框。

JavaScript 代码也可用于动态更改 HTML 文档的内容和样式。

以下是更改“<h1>”元素文本的 JavaScript 示例：

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

在此示例中，加载页面时，`<h1>` 元素的文本从“This is a heading”更改为“This is a new heading”。

## 附加信息

- 有关 HTML、CSS 和 JavaScript 的更多信息，请查看以下资源：

    - [W3C 的 HTML 规范](https://www.w3.org/TR/html/)
    - [W3C 的 CSS 规范](https://www.w3.org/TR/CSS/)
    - [W3C 的 JavaScript 规范](https://www.w3.org/TR/javascript/)
    - [Mozilla Developer Network 的 HTML 文档](https://developer.mozilla.org/en-US/docs/Web/HTML)
    - [Mozilla Developer Network 的 CSS 文档](https://developer.mozilla.org/en-US/docs/Web/CSS)
    - [Mozilla Developer Network 的 JavaScript 文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

## 警告

- 不要使用 `<script>` 元素加载外部 JavaScript 文件。仅使用 `<script>` 元素来内联 JavaScript 代码。

## 危险

- 不要使用 HTML、CSS 或 JavaScript 加载外部文件。