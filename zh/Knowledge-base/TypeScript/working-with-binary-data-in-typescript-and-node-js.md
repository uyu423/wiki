---
title: 在 TypeScript 和 Node.js 中使用二进制数据
description: 
published: true
date: 2023-02-10T09:17:40.968Z
tags: 
editor: markdown
dateCreated: 2023-02-10T09:17:38.476Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Working with Binary Data in TypeScript and Node.js***English** document is available*](/en/Knowledge-base/TypeScript/working-with-binary-data-in-typescript-and-node-js)
{.links-list}


# 在 TypeScript 和 Node.js 中处理二进制数据

IT 开发人员经常需要处理二进制数据。这可能是因为他们正在使用返回二进制数据的 API，或者因为他们需要读取二进制数据或将二进制数据写入文件。在 TypeScript 和 Node.js 中，开发人员有不同的选项来处理二进制数据。

## 缓冲区类

在 Node.js 中处理二进制数据的一种方法是使用“Buffer”类。这个类是全局可用的，所以不需要导入它。 `Buffer` 类提供了多种读取和写入二进制数据的方法。

要从字符串创建“Buffer”，开发人员可以使用“Buffer.from()”方法。此方法将字符串和编码作为参数。编码参数是可选的，默认为“utf8”。以下示例使用 utf8 编码从字符串创建一个 Buffer：

    const buf = Buffer.from('你好世界', 'utf8');

开发人员还可以使用 `Buffer.alloc()` 方法将二进制数据写入 `Buffer`。此方法将数字作为参数，即“Buffer”的大小（以字节为单位）。以下示例创建一个大小为 10 字节的空“Buffer”：

    const buf = Buffer.alloc(10);

创建“Buffer”后，开发人员可以使用“Buffer.write()”方法向其中写入数据。此方法将字符串、偏移量和编码作为参数。偏移量是将写入字符串的“缓冲区”中的索引。编码参数是可选的，默认为“utf8”。以下示例将字符串“hello world”写入上一示例中创建的“Buffer”，从索引 0 开始：

    buf.write('你好世界', 0, 'utf8');

要从 `Buffer` 中读取数据，开发人员可以使用 `Buffer.toString()` 方法。此方法采用编码和可选的开始和结束索引作为参数。以下示例从前面示例中创建的“Buffer”中读取数据并将其输出为字符串：

    console.log(buf.toString('utf8')); // '你好世界'

## Uint8Array 类

在 TypeScript 中处理二进制数据的另一种方法是使用“Uint8Array”类。这个类是全局可用的，所以不需要导入它。 `Uint8Array` 类提供了多种读取和写入二进制数据的方法。

要从数字数组创建“Uint8Array”，开发人员可以使用“Uint8Array.from()”方法。此方法将数字数组作为参数。以下示例从数字数组创建一个“Uint8Array”：

    const arr = Uint8Array.from([1, 2, 3, 4, 5]);

要从 `Buffer` 创建 `Uint8Array`，开发人员可以使用 `Uint8Array.from()` 方法。此方法将“Buffer”作为参数。以下示例从 `Buffer` 创建一个 `Uint8Array`：

    const buf = Buffer.from([1, 2, 3, 4, 5]);
    const arr = Uint8Array.from(buf);

创建“Uint8Array”后，开发人员可以使用“Uint8Array.set()”方法向其中写入数据。此方法采用数字数组和可选的起始索引作为参数。起始索引是“Uint8Array”中将写入数字数组的索引。以下示例将数字数组“[6, 7, 8, 9, 10]”写入上一个示例中创建的“Uint8Array”，从索引 0 开始：

    arr.set([6, 7, 8, 9, 10], 0);

要从 `Uint8Array` 读取数据，开发人员可以使用 `Uint8Array.subarray()` 方法。此方法将开始和结束索引作为参数。以下示例从前面示例中创建的“Uint8Array”中读取数据并将其输出为数组：

    console.log(arr.subarray(0, 5)); // [1, 2, 3, 4, 5]

## 在二进制数据类型之间转换

在某些情况下，开发人员可能需要在 `Buffer` 和 `Uint8Array` 之间进行转换。这可以使用 Buffer.from() 和 Uint8Array.from() 方法来完成。以下示例从 `Uint8Array` 创建一个 `Buffer`：

    const arr = Uint8Array.from([1, 2, 3, 4, 5]);
    const buf = Buffer.from(arr);

以下示例从 `Buffer` 创建一个 `Uint8Array`：

    const buf = Buffer.from([1, 2, 3, 4, 5]);
    const arr = Uint8Array.from(buf);

## 结论

开发人员在 TypeScript 和 Node.js 中使用二进制数据有不同的选择。 `Buffer` 类提供了多种处理二进制数据的方法，`Uint8Array` 类提供了另一种处理二进制数据的方法。在某些情况下，开发人员可能需要在 `Buffer` 和 `Uint8Array` 之间进行转换。