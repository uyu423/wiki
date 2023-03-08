---
title: How to Build a Responsive Website with CSS Grid and Flexbox
description: 
published: true
date: 2023-02-24T13:33:01.245Z
tags: 
editor: markdown
dateCreated: 2023-02-24T13:32:59.860Z
---

- [CSS 그리드와 Flexbox로 반응형 웹사이트를 구축하는 방법***Korean** document is available*](/ko/Knowledge-base/Common/how-to-build-a-responsive-website-with-css-grid-and-flexbox)
{.links-list}


# How to Build a Responsive Website with CSS Grid and Flexbox

With the widespread adoption of mobile devices, it's important that websites are designed to provide an optimal viewing experience on all screen sizes. CSS Grid and Flexbox are two technologies that can be used to create responsive websites.

CSS Grid is a two-dimensional layout system that allows elements to be positioned on a web page in columns and rows. Flexbox is a one-dimensional layout system that can be used to position elements in a single row or column.

In this article, we'll show you how to use CSS Grid and Flexbox to create a responsive website. We'll also provide some tips on using media queries to make your website even more responsive.

## Using CSS Grid

CSS Grid is a powerful tool for creating responsive websites. To use CSS Grid, you need to define a grid layout. This can be done using the CSS ```display``` property.

```css
.container {
  display: grid;
}
```

Once you have defined a grid layout, you can start to add elements to it. To add an element to a grid, you need to specify the ```grid-column``` and ```grid-row``` properties.

```css
.container {
  display: grid;
}

.item {
  grid-column: 1;
  grid-row: 1;
}
```

You can also use the ```grid-template-columns``` and ```grid-template-rows``` properties to define the size of the columns and rows in your grid.

```css
.container {
  display: grid;
  grid-template-columns: 200px 200px;
  grid-template-rows: 200px 200px;
}

.item {
  grid-column: 1;
  grid-row: 1;
}
```

If you want to learn more about using CSS Grid, we recommend reading the following article: [A Complete Guide to Grid](https://css-tricks.com/snippets/css/a-complete-guide-grid/).

## Using Flexbox

Flexbox is a one-dimensional layout system that can be used to position elements in a single row or column. To use Flexbox, you need to define a flex container. This can be done using the CSS ```display``` property.

```css
.container {
  display: flex;
}
```

Once you have defined a flex container, you can start to add elements to it. To add an element to a flex container, you need to specify the ```flex-grow```, ```flex-shrink```, and ```flex-basis``` properties.

```css
.container {
  display: flex;
}

.item {
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: 200px;
}
```

You can also use the ```flex-direction``` property to control the direction of the flex items. By default, flex items are arranged in a row. But you can use the ```flex-direction``` property to change this.

```css
.container {
  display: flex;
  flex-direction: column;
}

.item {
  flex-grow: 1;
  flex-shrink: 1;
  flex-basis: 200px;
}
```

If you want to learn more about using Flexbox, we recommend reading the following article: [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).

## Making Your Website More Responsive

In addition to using CSS Grid and Flexbox, you can also use media queries to make your website more responsive. Media queries allow you to change the CSS rules that are applied to a website based on the width of the screen.

For example, you could use a media query to change the layout of a website on mobile devices.

```css
@media (max-width: 768px) {
  .container {
    display: flex;
    flex-direction: column;
  }

  .item {
    flex-grow: 1;
    flex-shrink: 1;
    flex-basis: 200px;
  }
}
```

You can also use media queries to change the CSS rules that are applied to a website based on the orientation of the device. For example, you could use a media query to change the layout of a website on a tablet that is being held in landscape mode.

```css
@media (orientation: landscape) {
  .container {
    display: grid;
    grid-template-columns: 200px 200px;
    grid-template-rows: 200px 200px;
  }

  .item {
    grid-column: 1;
    grid-row: 1;
  }
}
```

If you want to learn more about using media queries, we recommend reading the following article: [A Beginner's Guide to Responsive Web Design](https://www.sitepoint.com/beginners-guide-responsive-web-design/).

## Conclusion

In this article, we've shown you how to use CSS Grid and Flexbox to create a responsive website. We've also provided some tips on using media queries to make your website even more responsive.

If you want to learn more about responsive web design, we recommend reading the following article: [Responsive Web Design Fundamentals](https://developers.google.com/web/fundamentals/design-and-ux/responsive/).