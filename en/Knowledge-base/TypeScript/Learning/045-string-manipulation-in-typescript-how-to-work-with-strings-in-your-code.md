---
title: 045: String Manipulation in TypeScript: How to Work with Strings in Your Code
description: 
published: true
date: 2023-03-03T18:32:22.337Z
tags: 
editor: markdown
dateCreated: 2023-03-03T18:32:22.337Z
---

- [045: TypeScript에서 문자열 조작: 코드에서 문자열로 작업하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/045-string-manipulation-in-typescript-how-to-work-with-strings-in-your-code)
{.links-list}


String manipulation is an essential part of any programming language. In TypeScript, strings are a primitive data type and can be manipulated in various ways. In this post, we will explore some of the most useful string manipulation techniques in TypeScript.

## String Literals

A string literal is a sequence of characters enclosed in double or single quotes. In TypeScript, we can declare a string literal using either double or single quotes.

```typescript
const name: string = "John";
const message: string = 'Hello World!';
```

## String Concatenation

String concatenation is the process of combining two or more strings into one. In TypeScript, we can use the `+` operator to concatenate strings.

```typescript
const firstName: string = "John";
const lastName: string = "Doe";
const fullName: string = firstName + " " + lastName;
console.log(fullName); // Output: John Doe
```

We can also use the `+=` operator to append a string to an existing one.

```typescript
let message: string = "Hello";
message += " World!";
console.log(message); // Output: Hello World!
```

## String Interpolation

String interpolation is a way to embed expressions inside a string literal. In TypeScript, we can use the `${}` syntax to interpolate expressions inside a string literal.

```typescript
const name: string = "John";
const age: number = 30;
const message: string = `My name is ${name} and I am ${age} years old.`;
console.log(message); // Output: My name is John and I am 30 years old.
```

## String Methods

TypeScript provides several built-in methods for string manipulation. Here are some of the most commonly used methods:

### `charAt()`

The `charAt()` method returns the character at a specified index in a string.

```typescript
const str: string = "Hello World!";
console.log(str.charAt(0)); // Output: H
console.log(str.charAt(6)); // Output: W
```

### `substring()`

The `substring()` method returns a part of a string between two specified indices.

```typescript
const str: string = "Hello World!";
console.log(str.substring(0, 5)); // Output: Hello
console.log(str.substring(6)); // Output: World!
```

### `replace()`

The `replace()` method replaces a specified value with another value in a string.

```typescript
const str: string = "Hello World!";
console.log(str.replace("World", "Universe")); // Output: Hello Universe!
```

### `toLowerCase()` and `toUpperCase()`

The `toLowerCase()` method converts a string to lowercase, while the `toUpperCase()` method converts a string to uppercase.

```typescript
const str: string = "Hello World!";
console.log(str.toLowerCase()); // Output: hello world!
console.log(str.toUpperCase()); // Output: HELLO WORLD!
```

### `trim()`

The `trim()` method removes whitespace from both ends of a string.

```typescript
const str: string = "   Hello World!   ";
console.log(str.trim()); // Output: Hello World!
```

## Additional Information

Strings in TypeScript are immutable. This means that once a string is created, it cannot be modified. Instead, string manipulation methods return a new string that contains the modified value.

## Conclusion

In this post, we have explored some of the most useful string manipulation techniques in TypeScript. We have learned about string literals, concatenation, interpolation, and some built-in string methods. By mastering these techniques, you can write more efficient and effective TypeScript code.

## External Resources

- [TypeScript Strings](https://www.tutorialsteacher.com/typescript/typescript-string)
- [TypeScript String Methods](https://www.tutorialsteacher.com/typescript/typescript-string-methods)