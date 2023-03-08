---
title: Web Assembly
description: 
published: true
date: 2023-02-12T04:56:18.421Z
tags: 
editor: markdown
dateCreated: 2023-02-12T04:56:15.923Z
---

- [Web Assembly***Japanese** document is available*](/ja/Knowledge-base/Dictionary/web-assembly)
{.links-list}
- [Web Assembly***Spanish** document is available*](/es/Knowledge-base/Dictionary/web-assembly)
{.links-list}
- [Web Assembly***Chinese Simplified** document is available*](/zh/Knowledge-base/Dictionary/web-assembly)
{.links-list}
- [Web Assembly***Korean** document is available*](/ko/Knowledge-base/Dictionary/web-assembly)
{.links-list}


# Overview

Web Assembly (WASM) is a new binary instruction format for a stack-based virtual machine. It is designed to be a portable, size- and load-time-efficient compilation target for programming languages, enabling deployment on the web for client and server applications.

# Description

Web Assembly (WASM) is a low-level, assembly-like language that is designed to be a compilation target for programming languages such as C, C++, Rust, and others. It is a binary instruction format that is designed to be efficient in terms of size, load time, and execution time. WASM is designed to be a portable target for compilation of high-level languages, allowing them to be deployed on the web for both client-side and server-side applications.

WASM is designed to be a safe, sandboxed execution environment, allowing code to run on the web without compromising the user’s security. It also provides a way to run code on the web that is more efficient than JavaScript, allowing for better performance and faster loading times.

WASM code is compiled ahead-of-time (AOT) into a binary format, which is then loaded and executed by a virtual machine. This virtual machine can be embedded in a web browser, or it can be implemented as a standalone application.

# History

Web Assembly was first announced in 2015 by the World Wide Web Consortium (W3C) as a part of the effort to create a new web platform. The initial version of the language was released in 2017 and has since seen several updates.

# Features

WASM provides a number of features that make it an attractive compilation target for web applications.

- It is a low-level, assembly-like language that is designed to be efficient in terms of size, load time, and execution time.
- It is a safe, sandboxed execution environment, allowing code to run on the web without compromising the user’s security.
- It provides a way to run code on the web that is more efficient than JavaScript, allowing for better performance and faster loading times.
- It is designed to be a portable target for compilation of high-level languages, allowing them to be deployed on the web for both client-side and server-side applications.

# Example

The following is an example of a simple program written in C and compiled to WASM:

```C
#include <stdio.h>

int main() {
  printf("Hello, World!\n");
  return 0;
}
```

This program can be compiled to WASM using a tool such as Emscripten:

```
emcc hello.c -o hello.wasm
```

This will produce a WASM binary, which can then be loaded and executed by a WASM virtual machine.

# Pros and Cons

WASM has a number of advantages over other web technologies:

- It is a safe, sandboxed execution environment, allowing code to run on the web without compromising the user’s security.
- It provides a way to run code on the web that is more efficient than JavaScript, allowing for better performance and faster loading times.
- It is designed to be a portable target for compilation of high-level languages, allowing them to be deployed on the web for both client-side and server-side applications.

However, there are also some disadvantages to using WASM:

- It is a relatively new technology and is still in development, so there may be bugs or compatibility issues.
- It is not as widely supported as other web technologies, so not all browsers may support it.
- It is not as easy to debug as other web technologies, so it may be difficult to troubleshoot issues.

# Related Technology

WASM is related to other web technologies such as JavaScript and WebGL. JavaScript is a scripting language that is used to create dynamic webpages, while WebGL is a graphics API that allows for hardware-accelerated 3D graphics in web browsers.

# Digression

WASM is an exciting new technology that has the potential to revolutionize the way web applications are developed. It provides a way to run code on the web that is more efficient than JavaScript, allowing for better performance and faster loading times. It is also designed to be a safe, sandboxed execution environment, allowing code to run on the web without compromising the user’s security.