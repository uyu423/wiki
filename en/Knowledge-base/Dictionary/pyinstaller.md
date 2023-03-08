---
title: PyInstaller
description: 
published: true
date: 2023-02-07T04:19:06.005Z
tags: 
editor: markdown
dateCreated: 2023-02-07T04:18:59.654Z
---

- [PyInstaller***Japanese** document is available*](/ja/Knowledge-base/Dictionary/pyinstaller)
{.links-list}
- [PyInstaller***Spanish** document is available*](/es/Knowledge-base/Dictionary/pyinstaller)
{.links-list}
- [PyInstaller***Chinese Simplified** document is available*](/zh/Knowledge-base/Dictionary/pyinstaller)
{.links-list}
- [PyInstaller***Korean** document is available*](/ko/Knowledge-base/Dictionary/pyinstaller)
{.links-list}


# Overview
PyInstaller is a program that packages Python programs into stand-alone executables, under Windows, Mac, and Linux. It is designed to be used by Python developers who need to distribute their applications to users who may or may not have Python installed.

# Description
PyInstaller is a free and open-source tool for converting Python programs into stand-alone executables. It is designed to be used by Python developers who need to distribute their applications to users who may or may not have Python installed. The program works by analyzing the Python program and collecting the necessary files and libraries needed to run it. It then packages these files into a single executable file that can be run on any machine, regardless of whether or not Python is installed.

PyInstaller supports Python 2.7, 3.4, 3.5, 3.6, and 3.7, and can package applications for Windows, Mac, and Linux. It can also package Python programs as single-file executables, which can be useful for distributing applications without revealing the source code.

# History
PyInstaller was first released in 2005, and is currently maintained by a team of volunteers. It has seen steady growth in popularity since its initial release, with over 2 million downloads as of 2020.

# Features
PyInstaller has a number of features that make it useful for Python developers. These include:

- Support for multiple platforms: PyInstaller can package applications for Windows, Mac, and Linux.
- Single-file executables: PyInstaller can package Python programs as single-file executables, which can be useful for distributing applications without revealing the source code.
- Automatic dependency detection: PyInstaller automatically detects and packages the necessary files and libraries needed to run a Python program.
- Bundled Python interpreter: PyInstaller can bundle a Python interpreter with the application, allowing it to run on machines without Python installed.

# Example
In this example, we will use PyInstaller to package a simple Python program into a stand-alone executable. The program prints the string "Hello, world!" to the console.

First, we create a file called "hello.py" with the following contents:

```
print("Hello, world!")
```

Next, we run the following command to package the program into a stand-alone executable:

```
pyinstaller hello.py
```

PyInstaller will create a folder called "dist" containing the executable file. This file can be run on any machine, regardless of whether or not Python is installed.

# Pros and Cons
Pros

- Easy to use: PyInstaller is easy to use and requires minimal setup.
- Cross-platform: PyInstaller can package applications for Windows, Mac, and Linux.
- Single-file executables: PyInstaller can package Python programs as single-file executables, which can be useful for distributing applications without revealing the source code.

Cons

- Limited support: PyInstaller only supports Python 2.7, 3.4, 3.5, 3.6, and 3.7.
- No GUI: PyInstaller does not have a GUI, so it must be used from the command line.

# Related Technology
PyOxidizer is another tool for packaging Python programs into stand-alone executables. It is designed to be more robust and feature-rich than PyInstaller, but it is still in early development.