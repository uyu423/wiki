---
title: 정확한 시간 관리를 위해 Java의 날짜 및 시간 API 활용
description: 
published: true
date: 2023-02-17T06:55:47.875Z
tags: 
editor: markdown
dateCreated: 2023-02-17T06:55:39.861Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Leveraging Java's Date and Time API for Precise Time Management***English** document is available*](/en/Knowledge-base/Java/leveraging-java-s-date-and-time-api-for-precise-time-management)
{.links-list}


# 정확한 시간 관리를 위해 Java의 날짜 및 시간 API 활용

Java의 날짜 및 시간 API는 날짜 및 시간을 관리하기 위한 강력하고 포괄적인 도구 집합입니다. Java 애플리케이션에서 정확한 시간 관리를 위해 활용할 수 있는 많은 기능을 제공합니다.

이 기사에서는 Date and Time API의 몇 가지 주요 기능과 정확한 시간 관리를 위해 어떻게 사용할 수 있는지 살펴보겠습니다. 또한 이러한 기능을 실제로 보여주는 몇 가지 코드 예제도 볼 수 있습니다.

## 현재 날짜와 시간 얻기

날짜 및 시간으로 작업할 때 가장 일반적인 작업 중 하나는 현재 날짜 및 시간을 가져오는 것입니다. 날짜 및 시간 API는 `Instant` 클래스의 정적 `now()` 메서드를 사용하여 이 작업을 쉽게 만듭니다. 이 메서드는 현재 날짜와 시간을 나타내는 `Instant` 개체를 반환합니다.

```java
Instant now = Instant.now();
```

## 날짜 및 시간 서식 지정

`Instant` 개체가 있으면 `format()` 메서드를 사용하여 원하는 대로 형식을 지정할 수 있습니다. 이 메서드는 `DateTimeFormatter` 개체를 인수로 사용합니다. 이 포맷터 개체는 날짜와 시간을 표시할 형식을 정의합니다.

`DateTimeFormatter` 클래스에서 사용할 수 있는 많은 내장 포맷터가 있습니다. 예를 들어 `ofLocalizedDateTime()` 메서드를 사용하여 현지화된 방식으로 날짜 및 시간 형식을 지정하는 포맷터를 가져올 수 있습니다.

```java
DateTimeFormatter formatter = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.FULL);
String formattedDateTime = now.format(formatter);
```

위의 코드는 `FULL` 형식 스타일을 사용하여 `Instant` 객체 `now` 형식을 지정합니다. 이 스타일은 'Monday, May 4, 2020 10:15:30 PM PDT'와 같은 날짜 및 시간 문자열을 생성합니다.

## 날짜 및 시간 구문 분석

날짜 및 시간 형식 지정 외에도 날짜 및 시간 API를 사용하여 구문 분석할 수도 있습니다. 이것은 날짜와 시간의 문자열 표현을 `Instant` 객체로 변환해야 할 때 유용할 수 있습니다.

서식 지정과 마찬가지로 `DateTimeFormatter` 개체를 사용하여 날짜와 시간을 구문 분석합니다. 다시 말하지만, 사용할 수 있는 내장 포맷터가 많이 있습니다. 사용자 지정 날짜 및 시간 패턴을 사용하는 포맷터를 만들기 위해 `ofPattern()` 메서드를 사용할 수 있습니다.

```java
String dateTimeString = "2020-05-04 22:15:30";
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
Instant instant = Instant.parse(dateTimeString, formatter);
```

위의 코드는 `yyyy-MM-dd HH:mm:ss` 패턴을 사용하여 `dateTimeString` 문자열을 구문 분석합니다. 이 패턴은 날짜 및 시간 문자열이 구성되는 방식을 정의합니다. 생성된 `Instant` 개체는 다른 `Instant` 개체처럼 사용할 수 있습니다.

## 시간대 관리

날짜 및 시간으로 작업할 때 또 다른 일반적인 작업은 시간대를 다루는 것입니다. 날짜 및 시간 API를 사용하면 `ZoneId` 클래스를 제공하여 시간대 작업을 쉽게 할 수 있습니다. 이 클래스는 시간대 식별자를 나타냅니다.

`ZoneId` 클래스의 정적 `of()` 메서드를 사용하여 특정 시간대에 대한 `ZoneId` 개체를 가져올 수 있습니다. 예를 들어 다음과 같이 태평양 시간대에 대한 `ZoneId` 개체를 가져올 수 있습니다.

```java
ZoneId zoneId = ZoneId.of("America/Los_Angeles");
```

`ZoneId` 객체가 있으면 이를 사용하여 `Instant` 객체를 `ZonedDateTime` 객체로 변환할 수 있습니다. 이 객체는 특정 시간대의 날짜와 시간을 나타냅니다.

```java
ZonedDateTime zonedDateTime = now.atZone(zoneId);
```

또한 `ZoneId` 개체를 사용하여 특정 시간대의 날짜 및 시간 문자열을 형식화할 수 있습니다.

```java
DateTimeFormatter formatter = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.FULL);
String formattedDateTime = zonedDateTime.format(formatter);
```

## 날짜 및 시간 조정

Date and Time API의 또 다른 유용한 기능은 날짜와 시간을 조정하는 기능입니다. 이는 `Instant` 및 `ZonedDateTime` 클래스의 `with()` 메서드를 사용하여 수행할 수 있습니다.

이 메서드는 `TemporalAdjuster` 개체를 인수로 사용합니다. 이 개체는 날짜 또는 시간을 조정하는 방법을 정의합니다. `next()`, `nextOrSame()`, `previous()`, `previousOrSame()` 및 `firstDayOfMonth()`와 같은 많은 내장 조절기가 있습니다.

```java
Instant instant = now.with(next(DayOfWeek.MONDAY));
```

위의 코드는 다음 월요일을 나타내도록 `Instant` 객체 `now`를 조정합니다.

## 측정 시간

날짜 및 시간 작업 외에도 날짜 및 시간 API는 시간을 측정하는 방법도 제공합니다. 이는 특정 작업이 소요되는 시간을 측정하는 데 유용할 수 있습니다.

`Duration` 클래스를 사용하여 두 `Instant` 객체 사이의 시간을 측정할 수 있습니다. 예를 들어 `now`와 `instant` 사이의 기간을 다음과 같이 측정할 수 있습니다.

```java
Duration duration = Duration.between(now, instant);
```

그런 다음 'getSeconds()' 메서드를 사용하여 기간의 총 초 수를 가져올 수 있습니다.

```java
long seconds = duration.getSeconds();
```

## 결론

Java의 날짜 및 시간 API는 날짜 및 시간 작업을 위한 강력한 도구 세트입니다. Java 애플리케이션에서 정확한 시간 관리를 위해 활용할 수 있는 많은 기능을 제공합니다. 이 기사에서는 날짜 및 시간 API의 몇 가지 주요 기능과 이를 정확한 시간 관리에 사용하는 방법을 살펴보았습니다.