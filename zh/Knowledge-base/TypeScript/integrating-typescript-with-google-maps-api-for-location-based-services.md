---
title: 将 TypeScript 与 Google Maps API 集成以提供基于位置的服务
description: 
published: true
date: 2023-02-06T18:55:23.336Z
tags: 
editor: markdown
dateCreated: 2023-02-06T18:55:17.687Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Integrating TypeScript with Google Maps API for Location-Based Services***English** document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-google-maps-api-for-location-based-services)
{.links-list}


# 将 TypeScript 与 Google Maps API 集成以提供基于位置的服务

TypeScript 是 JavaScript 的超集，支持类型检查和其他好处。 Google Maps API 是一种流行的定位服务 API，可实现交互式地图和地理编码。在本文中，我们将向您展示如何将 TypeScript 与 Google Maps API 集成以创建基于位置的服务。

## 什么是打字稿？

TypeScript 是 JavaScript 的超集，支持类型检查和其他好处。 TypeScript 易于与现有的 JavaScript 代码一起使用，并且可以逐步采用。

## 什么是谷歌地图 API？

Google Maps API 是一种流行的定位服务 API，可实现交互式地图和地理编码。该 API 可用于创建基于位置的服务，例如地图、搜索和导航。

## 如何将 TypeScript 与 Google Maps API 集成

要将 Google Maps API 与 TypeScript 结合使用，您需要创建一个 TypeScript 声明文件。 TypeScript 声明文件是包含 JavaScript 库的 TypeScript 类型信息的文件。 GitHub 上提供了 Google Maps API 的声明文件。

下载声明文件后，您可以使用以下代码行将其包含在您的 TypeScript 项目中：

```typescript
/// <reference path="google-maps-api.d.ts" />
```

您现在可以在 TypeScript 代码中使用 Google Maps API。例如，以下代码创建地图并向地图添加标记：

```typescript
var map: google.maps.Map;
var marker: google.maps.Marker;

map = new google.maps.Map(document.getElementById('map'), {
  zoom: 8,
  center: {lat: -34.397, lng: 150.644}
});

marker = new google.maps.Marker({
  position: {lat: -34.397, lng: 150.644},
  map: map
});
```

## 资源

- [打字稿](https://www.typescriptlang.org/)
- [谷歌地图 API](https://developers.google.com/maps/documentation/javascript/)
- [TypeScript 声明文件](https://www.typescriptlang.org/docs/handbook/declaration-files/introduction.html)
- [google-maps-api.d.ts](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/google-maps/index.d.ts)