---
title: 042: String Manipulation in TypeScript: How to Work with Strings in Your Code
description: 
published: true
date: 2023-03-02T14:32:23.320Z
tags: 
editor: markdown
dateCreated: 2023-03-02T14:32:16.129Z
---

- [042: TypeScript에서 문자열 조작: 코드에서 문자열로 작업하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/042-string-manipulation-in-typescript-how-to-work-with-strings-in-your-code)
{.links-list}


String manipulation is an essential part of any programming language. In TypeScript, strings are objects that allow you to work with text data. In this post, we'll explore different ways to manipulate strings in TypeScript.

## Strings in TypeScript

In TypeScript, strings are a sequence of characters enclosed in quotes. You can use single quotes or double quotes to define a string. For example:

```typescript
let name: string = "John";
let message: string = 'Hello World!';
```

You can also use template literals to define a string that can contain placeholders. For example:

```typescript
let name: string = "John";
let message: string = `Hello ${name}!`;
```

### String Properties and Methods

Strings in TypeScript have several properties and methods that allow you to manipulate them. Here are some of the most commonly used properties and methods:

#### length

The length property returns the number of characters in a string. For example:

```typescript
let name: string = "John";
let length: number = name.length; // length is 4
```

#### toUpperCase and toLowerCase

The toUpperCase method returns a new string with all characters converted to uppercase. The toLowerCase method returns a new string with all characters converted to lowercase. For example:

```typescript
let name: string = "John";
let upperCaseName: string = name.toUpperCase(); // "JOHN"
let lowerCaseName: string = name.toLowerCase(); // "john"
```

#### indexOf and lastIndexOf

The indexOf method returns the index of the first occurrence of a specified value in a string. The lastIndexOf method returns the index of the last occurrence of a specified value in a string. For example:

```typescript
let message: string = "Hello World!";
let index: number = message.indexOf("o"); // index is 4
let lastIndex: number = message.lastIndexOf("o"); // lastIndex is 7
```

#### substring and slice

The substring method returns a new string that contains a specified part of a string. The slice method also returns a new string that contains a specified part of a string, but it allows negative values to indicate the position from the end of the string. For example:

```typescript
let message: string = "Hello World!";
let substring: string = message.substring(0, 5); // "Hello"
let slice: string = message.slice(-6); // "World!"
```

#### replace

The replace method replaces a specified value with another value in a string. For example:

```typescript
let message: string = "Hello World!";
let newMessage: string = message.replace("World", "John"); // "Hello John!"
```

### Additional Information

Strings in TypeScript are immutable, which means that once you create a string, you cannot modify it. However, you can create a new string by using string methods.

### Warnings

When working with strings in TypeScript, be careful with the types of variables you use. TypeScript is a strongly typed language, which means that you must assign the correct type to a variable. If you assign the wrong type, you may get unexpected results.

### Dangers

When working with strings that contain user input or data from external sources, be careful with security vulnerabilities such as SQL injection attacks or cross-site scripting attacks. Always sanitize user input and validate data from external sources.

## Conclusion

In this post, we explored different ways to manipulate strings in TypeScript. We covered string properties and methods such as length, toUpperCase, toLowerCase, indexOf, lastIndexOf, substring, slice, and replace. Remember to be careful with the types of variables you use and be mindful of security vulnerabilities when working with user input or data from external sources.

## External Resources

- [TypeScript Strings](https://www.tutorialsteacher.com/typescript/typescript-string)
- [MDN Web Docs: String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)