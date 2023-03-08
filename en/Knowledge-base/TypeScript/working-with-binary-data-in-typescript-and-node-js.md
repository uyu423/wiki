---
title: Working with Binary Data in TypeScript and Node.js
description: 
published: true
date: 2023-02-10T09:17:45.554Z
tags: 
editor: markdown
dateCreated: 2023-02-10T09:17:38.479Z
---

- [Trabajar con datos binarios en TypeScript y Node.js***Spanish** document is available*](/es/Knowledge-base/TypeScript/working-with-binary-data-in-typescript-and-node-js)
{.links-list}
- [在 TypeScript 和 Node.js 中使用二进制数据***Chinese Simplified** document is available*](/zh/Knowledge-base/TypeScript/working-with-binary-data-in-typescript-and-node-js)
{.links-list}
- [TypeScript 및 Node.js에서 이진 데이터 작업***Korean** document is available*](/ko/Knowledge-base/TypeScript/working-with-binary-data-in-typescript-and-node-js)
{.links-list}


# Working with Binary Data in TypeScript and Node.js

IT developers often need to work with binary data. This may be because they are working with an API that returns binary data, or because they need to read or write binary data to a file. In TypeScript and Node.js, developers have different options for working with binary data.

## The Buffer Class

One way to work with binary data in Node.js is to use the `Buffer` class. This class is available globally, so there is no need to import it. The `Buffer` class provides several methods for reading and writing binary data.

To create a `Buffer` from a string, developers can use the `Buffer.from()` method. This method takes a string and an encoding as arguments. The encoding argument is optional and defaults to `utf8`. The following example creates a `Buffer` from a string using the `utf8` encoding:

    const buf = Buffer.from('hello world', 'utf8');

Developers can also write binary data to a `Buffer` using the `Buffer.alloc()` method. This method takes a number as an argument, which is the size of the `Buffer` in bytes. The following example creates an empty `Buffer` with a size of 10 bytes:

    const buf = Buffer.alloc(10);

Once a `Buffer` has been created, developers can write data to it using the `Buffer.write()` method. This method takes a string, an offset, and an encoding as arguments. The offset is the index in the `Buffer` where the string will be written. The encoding argument is optional and defaults to `utf8`. The following example writes the string ` 'hello world'` to the `Buffer` created in the previous example, starting at index 0:

    buf.write('hello world', 0, 'utf8');

To read data from a `Buffer`, developers can use the `Buffer.toString()` method. This method takes an encoding and optionally a start and end index as arguments. The following example reads the data from the `Buffer` created in the previous examples and outputs it as a string:

    console.log(buf.toString('utf8')); // 'hello world'

## The Uint8Array Class

Another way to work with binary data in TypeScript is to use the `Uint8Array` class. This class is available globally, so there is no need to import it. The `Uint8Array` class provides several methods for reading and writing binary data.

To create a `Uint8Array` from an array of numbers, developers can use the `Uint8Array.from()` method. This method takes an array of numbers as an argument. The following example creates a `Uint8Array` from an array of numbers:

    const arr = Uint8Array.from([1, 2, 3, 4, 5]);

To create a `Uint8Array` from a `Buffer`, developers can use the `Uint8Array.from()` method. This method takes a `Buffer` as an argument. The following example creates a `Uint8Array` from a `Buffer`:

    const buf = Buffer.from([1, 2, 3, 4, 5]);
    const arr = Uint8Array.from(buf);

Once a `Uint8Array` has been created, developers can write data to it using the `Uint8Array.set()` method. This method takes an array of numbers and optionally a start index as arguments. The start index is the index in the `Uint8Array` where the array of numbers will be written. The following example writes the array of numbers `[6, 7, 8, 9, 10]` to the `Uint8Array` created in the previous example, starting at index 0:

    arr.set([6, 7, 8, 9, 10], 0);

To read data from a `Uint8Array`, developers can use the `Uint8Array.subarray()` method. This method takes a start and end index as arguments. The following example reads the data from the `Uint8Array` created in the previous examples and outputs it as an array:

    console.log(arr.subarray(0, 5)); // [1, 2, 3, 4, 5]

## Converting Between Binary Data Types

In some cases, developers may need to convert between `Buffer` and `Uint8Array`. This can be done using the `Buffer.from()` and `Uint8Array.from()` methods. The following example creates a `Buffer` from a `Uint8Array`:

    const arr = Uint8Array.from([1, 2, 3, 4, 5]);
    const buf = Buffer.from(arr);

The following example creates a `Uint8Array` from a `Buffer`:

    const buf = Buffer.from([1, 2, 3, 4, 5]);
    const arr = Uint8Array.from(buf);

## Conclusion

Developers have different options for working with binary data in TypeScript and Node.js. The `Buffer` class provides several methods for working with binary data, and the `Uint8Array` class provides an alternative way of working with binary data. In some cases, developers may need to convert between `Buffer` and `Uint8Array`.