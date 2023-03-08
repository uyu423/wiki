---
title: Deep Dive into Java's System Class Loader
description: 
published: true
date: 2023-02-26T16:32:26.302Z
tags: 
editor: markdown
dateCreated: 2023-02-26T16:32:19.239Z
---

- [Java의 시스템 클래스 로더에 대해 자세히 알아보기***Korean** document is available*](/ko/Knowledge-base/Java/deep-dive-into-java-s-system-class-loader)
{.links-list}


# Deep Dive into Java's System Class Loader

The System Class Loader is the default class loader used by the Java Runtime Environment (JRE). It loads class files from the file system and class path. In this article, we will take a deep dive into how the System Class Loader works and how to use it.

## What is a Class Loader?

A class loader is a program that loads class files from a file system or network and makes them available to the Java Virtual Machine (JVM). Class loaders are used to load classes at run time.

There are three types of class loaders in Java:

- Bootstrap ClassLoader
- Extension ClassLoader
- System ClassLoader

The Bootstrap ClassLoader loads the core Java classes, such as java.lang.Object, from the rt.jar file. The Extension ClassLoader loads classes from the ext folder. The System ClassLoader loads classes from the classpath.

## How does the System Class Loader work?

The System Class Loader loads class files from the file system and class path. The file system is the file system of the local machine. The class path is a list of locations that the System Class Loader searches for class files.

The System Class Loader uses a three-step process to load class files:

1. The System Class Loader searches the file system for the class file.
2. If the class file is not found, the System Class Loader searches the class path for the class file.
3. If the class file is not found, the System Class Loader loads the class file from the network.

The System Class Loader can load class files from the file system, the class path, or the network.

## How to use the System Class Loader?

The System Class Loader can be used to load class files from the file system, the class path, or the network.

To load class files from the file system, you can use the java.lang.ClassLoader.getSystemResourceAsStream() method. This method returns an InputStream that can be used to read the class file from the file system.

To load class files from the class path, you can use the java.lang.ClassLoader.getSystemResourceAsStream() method. This method returns an InputStream that can be used to read the class file from the class path.

To load class files from the network, you can use the java.lang.ClassLoader.getSystemResourceAsStream() method. This method returns an InputStream that can be used to read the class file from the network.

## Conclusion

In this article, we have taken a deep dive into Java's System Class Loader. We have seen what a class loader is and how the System Class Loader works. We have also seen how to use the System Class Loader to load class files from the file system, the class path, or the network.