---
title: 使用 Java 的正则表达式 API
description: 
published: true
date: 2023-02-13T17:17:31.957Z
tags: 
editor: markdown
dateCreated: 2023-02-13T17:17:30.347Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Working with Java's Regular Expressions API***English** document is available*](/en/Knowledge-base/Java/working-with-java-s-regular-expressions-api)
{.links-list}


# 使用 Java 的正则表达式 API

Java 的正则表达式 API 是所有语言中最强大的 API 之一。它可用于匹配字符串、搜索子字符串和替换子字符串。在这篇文章中，我们将看看如何使用正则表达式 API 来完成这些事情。

## 匹配字符串

正则表达式 API 的最基本用途是将字符串与正则表达式进行匹配。这可以通过 java.util.regex.Pattern 类的 matches() 方法来完成。例如，要将字符串与匹配一个或多个数字的正则表达式“\\d+”匹配，我们将执行以下操作：

```java
String input = "12345";
String regex = "\\d+";

boolean matches = Pattern.matches(regex, input);
// matches is true
```

如果正则表达式包含捕获组，则可以通过“matches()”方法访问这些组。例如，正则表达式“(\\d)(\\d)”有两个捕获组。我们可以像这样访问这些捕获组：

```java
String input = "12";
String regex = "(\\d)(\\d)";

boolean matches = Pattern.matches(regex, input);
// matches is true

// Get the first capture group
Matcher m = Pattern.compile(regex).matcher(input);
m.matches();
String group1 = m.group(1); // "1"

// Get the second capture group
String group2 = m.group(2); // "2"
```

## 搜索子字符串

正则表达式 API 也可用于搜索与正则表达式匹配的子字符串。这可以通过 java.util.regex.Matcher 类的 find() 方法来完成。例如，要在字符串“12345”中搜索子字符串“\\d+”，我们将执行以下操作：

```java
String input = "12345";
String regex = "\\d+";

Matcher m = Pattern.compile(regex).matcher(input);

boolean found = m.find();
// found is true

// Get the substring that was found
String found = m.group(); // "12345"
```

与 `matches()` 类似，`find()` 方法也支持捕获组。例如，正则表达式“(\\d)(\\d)”有两个捕获组。我们可以像这样访问这些捕获组：

```java
String input = "12345";
String regex = "(\\d)(\\d)";

Matcher m = Pattern.compile(regex).matcher(input);

boolean found = m.find();
// found is true

// Get the first capture group
String group1 = m.group(1); // "1"

// Get the second capture group
String group2 = m.group(2); // "2"
```

## 替换子字符串

正则表达式 API 也可用于替换与正则表达式匹配的子字符串。这可以通过 java.util.regex.Matcher 类的 replaceAll() 方法来完成。例如，要将字符串“12345”中与正则表达式“\\d”匹配的所有子字符串替换为字符串“X”，我们将执行以下操作：

```java
String input = "12345";
String regex = "\\d";

Matcher m = Pattern.compile(regex).matcher(input);

String replaced = m.replaceAll("X");
// replaced is "XXXXX"
```

## 结论

在本文中，我们了解了如何使用 Java 的正则表达式 API 来匹配字符串、搜索子字符串和替换子字符串。我们还看到了如何访问捕获组。有了这些知识，您应该能够使用正则表达式 API 来解决各种问题。