---
title: Building Image and Video Processing Applications with TypeScript and Node.js
description: 
published: true
date: 2023-02-08T20:17:46.552Z
tags: 
editor: markdown
dateCreated: 2023-02-08T20:17:40.463Z
---

- [Creación de aplicaciones de procesamiento de imágenes y videos con TypeScript y Node.js***Spanish** document is available*](/es/Knowledge-base/TypeScript/building-image-and-video-processing-applications-with-typescript-and-node-js)
{.links-list}
- [使用 TypeScript 和 Node.js 构建图像和视频处理应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/TypeScript/building-image-and-video-processing-applications-with-typescript-and-node-js)
{.links-list}
- [TypeScript 및 Node.js로 이미지 및 비디오 처리 애플리케이션 구축***Korean** document is available*](/ko/Knowledge-base/TypeScript/building-image-and-video-processing-applications-with-typescript-and-node-js)
{.links-list}


# Building Image and Video Processing Applications with TypeScript and Node.js

Developers looking to create scalable image and video processing applications have many choices when it comes to programming languages. One option that is often overlooked is TypeScript. TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. It is a language that is both easy to learn for beginners and also has advanced features that experienced developers can take advantage of.

Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. It is used for developing server-side applications. Node.js applications are written in JavaScript and can be run on a variety of platforms, including Windows, macOS, and Linux.

In this article, we will show how to use TypeScript and Node.js to build an image processing application. We will be using the TypeScript library, gm, which is a wrapper around the GraphicsMagick library. GraphicsMagick is a cross-platform image processing toolkit that can be used to create, edit, and convert images.

The gm library provides a simple API for performing common image processing tasks, such as resizing, cropping, and converting images. It can be used to create both command-line and web applications. In this article, we will be creating a command-line application that will resize an image.

## Installing TypeScript and Node.js

Before we can start writing our application, we need to install TypeScript and Node.js. TypeScript can be installed using npm, the Node.js package manager. To install TypeScript, open a terminal and run the following command:

```
npm install -g typescript
```

This will install the TypeScript compiler, tsc, and the TypeScript language server, tsserver. The TypeScript compiler is used to compile TypeScript code into JavaScript code. The TypeScript language server provides language services, such as code completion and type checking, for TypeScript code.

Node.js can be downloaded from the Node.js website. Once Node.js has been installed, the npm command-line interface will be available.

## Creating a TypeScript Project

Now that we have TypeScript and Node.js installed, we can create a TypeScript project. To do this, we will use the npm init command. This command will create a package.json file, which is used to manage the dependencies of a Node.js project.

To create a TypeScript project, open a terminal and navigate to the directory where you want to create the project. Then, run the following command:

```
npm init
```

This will prompt you for a number of questions, such as the name and version of the project. For our project, we will set the name to "image-processing-app" and the version to "1.0.0".

Once the package.json file has been created, we can install the dependencies for our project. For our project, we will need to install the gm TypeScript definitions and the gm library. To do this, run the following command:

```
npm install --save @types/gm gm
```

This will install the gm TypeScript definitions and the gm library into the node_modules directory. The gm TypeScript definitions provide TypeScript bindings for the gm library.

## Resizing an Image

Now that we have our project set up, we can start writing our application. The first thing we need to do is import the gm library. We can do this by adding the following line to the top of our main.ts file:

```typescript
import * as gm from "gm";
```

This will import the gm namespace into our file. We can now use the gm namespace to access the functionality of the gm library.

The next thing we need to do is open our image. We can do this using the gm.open() function. This function takes the path to the image as its first argument and a callback function as its second argument. The callback function is called with an error object and a gm object. The gm object can be used to perform operations on the image.

We can open our image and pass the gm object to a resize() function as follows:

```typescript
gm.open("input.jpg", (err, image) => {
  if (err) {
    console.log(err);
  } else {
    resize(image);
  }
});
```

The resize() function will take the gm object and resize the image. We can define the resize() function as follows:

```typescript
function resize(image: gm.Image): void {
  image
    .resize(100, 100)
    .write("output.jpg", (err) => {
      if (err) {
        console.log(err);
      }
    });
}
```

This function will resize the image to 100x100 pixels and write the output to the output.jpg file.

To run our application, we can use the TypeScript compiler, tsc. We can compile our code by running the following command:

```
tsc main.ts
```

This will generate a main.js file in the current directory. We can run our application by running the following command:

```
node main.js
```

This will resize the input.jpg image and save the output to the output.jpg file.

## Conclusion

In this article, we have shown how to use TypeScript and Node.js to build an image processing application. We have seen how to use the gm library to resize an image. This application can be easily extended to perform other image processing tasks, such as cropping and converting images.