---
title: Java의 정규식 API 작업
description: 
published: true
date: 2023-02-13T17:17:31.942Z
tags: 
editor: markdown
dateCreated: 2023-02-13T17:17:30.346Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Working with Java's Regular Expressions API***English** document is available*](/en/Knowledge-base/Java/working-with-java-s-regular-expressions-api)
{.links-list}


# Java의 정규식 API로 작업하기

Java의 정규식 API는 모든 언어에서 가장 강력한 것 중 하나입니다. 문자열 일치, 하위 문자열 검색 및 하위 문자열 교체에 사용할 수 있습니다. 이 문서에서는 정규식 API를 사용하여 이러한 각 작업을 수행하는 방법을 살펴보겠습니다.

## 일치하는 문자열

정규식 API의 가장 기본적인 용도는 문자열을 정규식과 일치시키는 것입니다. 이는 `java.util.regex.Pattern` 클래스의 `matches()` 메서드를 사용하여 수행할 수 있습니다. 예를 들어 하나 이상의 숫자와 일치하는 정규 표현식 `"\\d+"`에 대해 문자열을 일치시키려면 다음을 수행합니다.

```java
String input = "12345";
String regex = "\\d+";

boolean matches = Pattern.matches(regex, input);
// matches is true
```

정규식에 캡처 그룹이 포함된 경우 해당 그룹은 `matches()` 메서드를 통해 액세스할 수 있습니다. 예를 들어 정규식 `"(\\d)(\\d)"`에는 두 개의 캡처 그룹이 있습니다. 다음과 같이 해당 캡처 그룹에 액세스할 수 있습니다.

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

## 하위 문자열 검색

정규식 API를 사용하여 정규식과 일치하는 하위 문자열을 검색할 수도 있습니다. 이는 `java.util.regex.Matcher` 클래스의 `find()` 메서드를 사용하여 수행할 수 있습니다. 예를 들어 문자열 `"12345"`에서 하위 문자열 `"\\d+"`를 검색하려면 다음을 수행합니다.

```java
String input = "12345";
String regex = "\\d+";

Matcher m = Pattern.compile(regex).matcher(input);

boolean found = m.find();
// found is true

// Get the substring that was found
String found = m.group(); // "12345"
```

`matches()`와 마찬가지로 `find()` 메서드도 캡처 그룹을 지원합니다. 예를 들어 정규식 `"(\\d)(\\d)"`에는 두 개의 캡처 그룹이 있습니다. 다음과 같이 해당 캡처 그룹에 액세스할 수 있습니다.

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

## 하위 문자열 바꾸기

정규식 API를 사용하여 정규식과 일치하는 하위 문자열을 바꿀 수도 있습니다. 이는 `java.util.regex.Matcher` 클래스의 `replaceAll()` 메서드를 사용하여 수행할 수 있습니다. 예를 들어 정규식 `"\\d"`와 일치하는 모든 하위 문자열을 문자열 `"12345"`에서 문자열 `"X"`로 바꾸려면 다음을 수행합니다.

```java
String input = "12345";
String regex = "\\d";

Matcher m = Pattern.compile(regex).matcher(input);

String replaced = m.replaceAll("X");
// replaced is "XXXXX"
```

## 결론

이 기사에서는 Java의 정규식 API를 사용하여 문자열을 일치시키고 하위 문자열을 검색하고 하위 문자열을 바꾸는 방법을 살펴보았습니다. 또한 캡처 그룹에 액세스하는 방법도 살펴보았습니다. 이러한 지식을 바탕으로 정규식 API를 사용하여 다양한 문제를 해결할 수 있어야 합니다.