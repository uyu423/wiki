---
title: Working with Java's Regular Expressions API
description: 
published: true
date: 2023-02-13T17:17:37.649Z
tags: 
editor: markdown
dateCreated: 2023-02-13T17:17:30.351Z
---

- [Trabajar con la API de expresiones regulares de Java***Spanish** document is available*](/es/Knowledge-base/Java/working-with-java-s-regular-expressions-api)
{.links-list}
- [使用 Java 的正则表达式 API***Chinese Simplified** document is available*](/zh/Knowledge-base/Java/working-with-java-s-regular-expressions-api)
{.links-list}
- [Java의 정규식 API 작업***Korean** document is available*](/ko/Knowledge-base/Java/working-with-java-s-regular-expressions-api)
{.links-list}


# Working with Java's Regular Expressions API

Java's regular expression API is one of the most powerful in any language. It can be used to match strings, search for substrings, and replace substrings. In this article, we'll take a look at how to use the regular expression API to do each of these things.

## Matching Strings

The most basic use of the regular expression API is to match a string against a regular expression. This can be done with the `matches()` method of the `java.util.regex.Pattern` class. For example, to match a string against the regular expression `"\\d+"`, which matches one or more digits, we would do the following:

```java
String input = "12345";
String regex = "\\d+";

boolean matches = Pattern.matches(regex, input);
// matches is true
```

If the regular expression includes capture groups, then those groups can be accessed via the `matches()` method. For example, the regular expression `"(\\d)(\\d)"` has two capture groups. We can access those capture groups like this:

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

## Searching for Substrings

The regular expression API can also be used to search for substrings that match a regular expression. This can be done with the `find()` method of the `java.util.regex.Matcher` class. For example, to search for the substring `"\\d+"` in the string `"12345"`, we would do the following:

```java
String input = "12345";
String regex = "\\d+";

Matcher m = Pattern.compile(regex).matcher(input);

boolean found = m.find();
// found is true

// Get the substring that was found
String found = m.group(); // "12345"
```

Similarly to `matches()`, the `find()` method also supports capture groups. For example, the regular expression `"(\\d)(\\d)"` has two capture groups. We can access those capture groups like this:

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

## Replacing Substrings

The regular expression API can also be used to replace substrings that match a regular expression. This can be done with the `replaceAll()` method of the `java.util.regex.Matcher` class. For example, to replace all substrings that match the regular expression `"\\d"` with the string `"X"` in the string `"12345"`, we would do the following:

```java
String input = "12345";
String regex = "\\d";

Matcher m = Pattern.compile(regex).matcher(input);

String replaced = m.replaceAll("X");
// replaced is "XXXXX"
```

## Conclusion

In this article, we've looked at how to use Java's regular expression API to match strings, search for substrings, and replace substrings. We've also seen how to access capture groups. With this knowledge, you should be able to use the regular expression API to solve a variety of problems.