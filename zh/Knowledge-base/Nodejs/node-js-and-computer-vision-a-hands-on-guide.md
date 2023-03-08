---
title: Node.js 和计算机视觉：实践指南
description: 
published: true
date: 2023-02-09T04:18:36.032Z
tags: 
editor: markdown
dateCreated: 2023-02-09T04:18:29.705Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Node.js and Computer Vision: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-computer-vision-a-hands-on-guide)
{.links-list}


# Node.js 和计算机视觉：实践指南

在 Web 开发领域，Node.js 是一种流行的服务器端 JavaScript 运行时环境。它被 Netflix、沃尔玛和 eBay 等大公司使用。它不仅适用于 Web 开发。 Node.js 在构建桌面应用程序和嵌入式系统开发方面也很受欢迎。

Node.js 被广泛采用的一个领域是计算机视觉。在本文中，我们将了解什么是计算机视觉以及如何使用 Node.js 构建动手解决方案。

## 什么是计算机视觉？

计算机视觉是人工智能的一个领域，涉及如何让计算机理解数字图像。这涉及图像识别、对象检测和图像分类等任务。

计算机视觉是一个广阔的领域，有许多不同的应用。它用于自动驾驶汽车、面部识别和医学图像分析。

## Node.js 和计算机视觉

有几种不同的方法可以将 Node.js 用于计算机视觉。最流行的两个是开源库 OpenCV 和商业库 Sightengine。

OpenCV 是最流行的计算机视觉库，并且绑定了许多编程语言，包括 Node.js。它用于广泛的应用程序，包括安全、机器人和增强现实。

Sightengine 是一个专注于图像识别的商业计算机视觉库。它提供免费试用并有一个 Node.js 客户端库。

在本文中，我们将重点关注 OpenCV，因为它是两个库中更受欢迎的一个。

## OpenCV 入门

OpenCV是一个开源库，所以可以免费安装。安装它的最简单方法是使用 Node.js 包管理器 npm。

```
npm install opencv
```

这将安装最新版本的 OpenCV。

安装 OpenCV 后，您可以在 Node.js 代码中要求它。

```javascript
const cv = require('opencv');
```

## 读取图像

任何计算机视觉项目的第一步都是读取图像。 OpenCV 的 readImage 函数让这一切变得简单。

```javascript
cv.readImage('image.jpg', (err, img) => {
  if (err) {
    console.error(err);
  } else {
    // Do something with the image
  }
});
```

这将读取图像 `image.jpg` 并将其作为 `img` 对象提供。

## 转换图像

OpenCV 支持多种图像格式，包括 JPEG、PNG 和 TIFF。但是，并非所有功能都支持所有格式。例如，`threshold` 函数仅支持灰度图像。

要将图像转换为灰度，您可以使用 `cvtColor` 函数。

```javascript
cv.cvtColor(img, cv.COLOR_BGR2GRAY, (err, grayImg) => {
  if (err) {
    console.error(err);
  } else {
    // Do something with the grayscale image
  }
});
```

这会将图像“img”转换为灰度并将其作为“grayImg”提供。

## 对图像进行阈值处理

阈值化是计算机视觉中的常见操作。它用于将图像转换为二进制图像，其中每个像素为黑色或白色。

OpenCV 提供了一个“threshold”函数，它获取图像和阈值。强度大于阈值的像素被转换为白色，强度小于阈值的像素被转换为黑色。

```javascript
cv.threshold(grayImg, 127, 255, cv.THRESH_BINARY, (err, binImg) => {
  if (err) {
    console.error(err);
  } else {
    // Do something with the binary image
  }
});
```

这将阈值为 127 的图像“grayImg”。生成的图像将作为“binImg”提供。

## 反转图像

在某些情况下，反转图像可能很有用。这可以通过 `bitwise_not` 函数来完成。

```javascript
cv.bitwise_not(binImg, (err, invImg) => {
  if (err) {
    console.error(err);
  } else {
    // Do something with the inverted image
  }
});
```

这将反转图像 binImg 并将结果提供为 invImg。

## 保存图片

处理图像后，您可能希望保存结果。 OpenCV 为此提供了 `saveImage` 函数。

```javascript
cv.saveImage('output.jpg', invImg);
```

这会将图像“invImg”保存为“output.jpg”。

## 结论

在本文中，我们了解了什么是计算机视觉以及如何使用 Node.js 构建动手解决方案。我们介绍了如何安装 OpenCV、如何读取和转换图像、如何对图像进行阈值处理以及如何保存图像。

这只是计算机视觉的冰山一角。如果您有兴趣了解更多信息，我建议您查看以下资源。

## 资源

- [OpenCV 文档](https://docs.opencv.org/4.1.0/)
- [Sightengine 文档](https://sightengine.com/docs/reference/nodejs)
- [维基百科上的计算机视觉](https://en.wikipedia.org/wiki/Computer_vision)