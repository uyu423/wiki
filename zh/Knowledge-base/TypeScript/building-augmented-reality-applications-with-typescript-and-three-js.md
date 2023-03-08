---
title: 使用 TypeScript 和 Three.js 构建增强现实应用程序
description: 
published: true
date: 2023-01-31T17:17:19.070Z
tags: 
editor: markdown
dateCreated: 2023-01-31T17:17:17.455Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Building Augmented Reality Applications with TypeScript and Three.js***English** version of this document is available*](/en/Knowledge-base/TypeScript/building-augmented-reality-applications-with-typescript-and-three-js)
{.links-list}



# 使用 TypeScript 和 Three.js 构建增强现实应用程序

随着 ARKit 和 ARCore 的发布，增强现实 (AR) 正变得越来越主流。这些新的 SDK 允许开发人员为 iOS 和 Android 设备上的数百万用户创建 AR 体验。

然而，开发 AR 应用程序可能是一项挑战。 SDK 不断变化，可用于帮助开发人员入门的资源很少。

本文将向您展示如何使用 TypeScript 和 Three.js 为 Web 创建 AR 应用程序。我们将介绍设置开发环境、创建简单的 AR 场景以及将应用程序部署到 Web 服务器。

## 设置你的开发环境

在我们开始构建我们的 AR 应用程序之前，我们需要设置我们的开发环境。

首先，您需要安装 [Node.js](https://nodejs.org/en/)。 Node.js 是一个 JavaScript 运行时，允许您在 Web 浏览器之外运行 JavaScript 代码。我们将使用 Node.js 为我们的应用程序运行本地 Web 服务器。

接下来，您需要安装 [TypeScript](https://www.typescriptlang.org/)。 TypeScript 是 JavaScript 的超集，增加了静态类型检查和其他功能。我们将使用 TypeScript 编写我们的 AR 应用程序。

最后，您需要安装 [Three.js](https://threejs.org/)。 Three.js 是一个用于创建 3D 图形的 JavaScript 库。我们将使用 Three.js 来创建我们的 AR 场景。

## 创建一个简单的 AR 场景

现在我们已经设置好开发环境，可以开始创建 AR 场景了。

首先，我们需要创建一个新的 TypeScript 文件并导入 Three.js：

```typescript
import * as THREE from 'three';
```

接下来，我们需要创建一个新的 Three.js 场景：

```typescript
const scene = new THREE.Scene();
```

现在我们可以向场景中添加一些对象。让我们从一个简单的立方体开始：

```typescript
const geometry = new THREE.BoxGeometry(1, 1, 1);
const material = new THREE.MeshBasicMaterial({ color: 0xff0000 });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);
```

最后，我们需要渲染我们的场景：

```typescript
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

renderer.render(scene, camera);
```

如果一切顺利，您应该会在网络浏览器中看到一个红色立方体。

## 部署你的应用程序

现在我们有了一个基本的 AR 场景，我们需要将它部署到 Web 服务器上。

首先，我们需要安装 [http-server](https://www.npmjs.com/package/http-server) Node.js 模块：

```
npm install -g http-server
```

接下来，我们需要将 TypeScript 代码编译为 JavaScript：

```
tsc main.ts
```

最后，我们可以启动网络服务器：

```
http-server
```

您现在可以通过 http://localhost:8080 访问您的应用程序。

## 结论

在本文中，我们了解了如何使用 TypeScript 和 Three.js 为 Web 创建 AR 应用程序。我们介绍了设置开发环境、创建简单的 AR 场景以及将应用程序部署到 Web 服务器。

如果您有兴趣了解有关 AR 开发的更多信息，请查看以下资源：

- [ARKit 101](https://www.raywenderlich.com/160517/arkit-101-using-arkit-build-augmented-reality-apps)
- [ARCore 101](https://www.raywenderlich.com/166886/arcore-101-arkit-equivalent-android)
- [A-Frame](https://aframe.io/)