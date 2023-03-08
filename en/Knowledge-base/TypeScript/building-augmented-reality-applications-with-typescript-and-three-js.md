---
title: Building Augmented Reality Applications with TypeScript and Three.js
description: 
published: true
date: 2023-01-31T17:17:21.167Z
tags: 
editor: markdown
dateCreated: 2023-01-31T17:17:17.444Z
---

- [TypeScript 및 Three.js로 증강 현실 애플리케이션 구축***Korean** version of this document is available*](/ko/Knowledge-base/TypeScript/building-augmented-reality-applications-with-typescript-and-three-js)
{.links-list}
- [TypeScript と Three.js を使用した拡張現実アプリケーションの構築***Japanese** version of this document is available*](/ja/Knowledge-base/TypeScript/building-augmented-reality-applications-with-typescript-and-three-js)
{.links-list}
- [使用 TypeScript 和 Three.js 构建增强现实应用程序***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/TypeScript/building-augmented-reality-applications-with-typescript-and-three-js)
{.links-list}



# Building Augmented Reality Applications with TypeScript and Three.js

With the release of ARKit and ARCore, augmented reality (AR) is becoming more mainstream. These new SDKs allow developers to create AR experiences for millions of users on iOS and Android devices.

However, developing AR applications can be a challenge. The SDKs are constantly changing and there are few resources available to help developers get started.

This article will show you how to use TypeScript and Three.js to create AR applications for the web. We'll cover setting up a development environment, creating a simple AR scene, and deploying the application to a web server.

## Setting up your development environment

Before we can start building our AR application, we need to set up our development environment.

First, you'll need to install [Node.js](https://nodejs.org/en/). Node.js is a JavaScript runtime that allows you to run JavaScript code outside of a web browser. We'll use Node.js to run a local web server for our application.

Next, you'll need to install [TypeScript](https://www.typescriptlang.org/). TypeScript is a superset of JavaScript that adds static type checking and other features. We'll use TypeScript to write our AR application.

Finally, you'll need to install [Three.js](https://threejs.org/). Three.js is a JavaScript library for creating 3D graphics. We'll use Three.js to create our AR scene.

## Creating a simple AR scene

Now that we have our development environment set up, we can start creating our AR scene.

First, we need to create a new TypeScript file and import Three.js:

```typescript
import * as THREE from 'three';
```

Next, we need to create a new Three.js scene:

```typescript
const scene = new THREE.Scene();
```

Now we can add some objects to our scene. Let's start with a simple cube:

```typescript
const geometry = new THREE.BoxGeometry(1, 1, 1);
const material = new THREE.MeshBasicMaterial({ color: 0xff0000 });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);
```

Finally, we need to render our scene:

```typescript
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

renderer.render(scene, camera);
```

If everything went well, you should see a red cube in your web browser.

## Deploying your application

Now that we have a basic AR scene, we need to deploy it to a web server.

First, we need to install the [http-server](https://www.npmjs.com/package/http-server) Node.js module:

```
npm install -g http-server
```

Next, we need to compile our TypeScript code to JavaScript:

```
tsc main.ts
```

Finally, we can start the web server:

```
http-server
```

You can now access your application at http://localhost:8080.

## Conclusion

In this article, we've seen how to use TypeScript and Three.js to create AR applications for the web. We've covered setting up a development environment, creating a simple AR scene, and deploying the application to a web server.

If you're interested in learning more about AR development, check out the following resources:

- [ARKit 101](https://www.raywenderlich.com/160517/arkit-101-using-arkit-build-augmented-reality-apps)
- [ARCore 101](https://www.raywenderlich.com/166886/arcore-101-arkit-equivalent-android)
- [A-Frame](https://aframe.io/)