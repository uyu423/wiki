---
title: 利用 Java 的日期和时间 API 进行精确的时间管理
description: 
published: true
date: 2023-02-17T06:55:47.875Z
tags: 
editor: markdown
dateCreated: 2023-02-17T06:55:39.860Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Leveraging Java's Date and Time API for Precise Time Management***English** document is available*](/en/Knowledge-base/Java/leveraging-java-s-date-and-time-api-for-precise-time-management)
{.links-list}


# 利用 Java 的日期和时间 API 进行精确的时间管理

Java 的日期和时间 API 是一套强大而全面的日期和时间管理工具。它提供了许多可用于在 Java 应用程序中进行精确时间管理的功能。

在本文中，我们将了解日期和时间 API 的一些主要功能，以及如何使用它们进行精确的时间管理。我们还将看到一些代码示例来演示这些功能的实际应用。

## 获取当前日期和时间

使用日期和时间时最常见的任务之一是获取当前日期和时间。日期和时间 API 使用“Instant”类的静态“now()”方法使这项任务变得简单。此方法返回表示当前日期和时间的“Instant”对象。

```java
Instant now = Instant.now();
```

## 格式化日期和时间

一旦我们有了一个“Instant”对象，我们就可以使用“format()”方法将其格式化为我们喜欢的格式。此方法将“DateTimeFormatter”对象作为参数。此格式化程序对象定义了我们希望显示日期和时间的格式。

`DateTimeFormatter` 类中有许多可用的内置格式化程序。例如，我们可以使用 `ofLocalizedDateTime()` 方法来获取以本地化方式格式化日期和时间的格式化程序。

```java
DateTimeFormatter formatter = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.FULL);
String formattedDateTime = now.format(formatter);
```

上面的代码使用 `FULL` 格式样式格式化 `Instant` 对象 `now`。这种样式会产生一个日期和时间字符串，看起来像这样：`Monday, May 4, 2020 10:15:30 PM PDT`。

## 解析日期和时间

除了格式化日期和时间，日期和时间 API 还允许我们解析它们。当我们需要将日期和时间的字符串表示形式转换为“Instant”对象时，这会很有用。

就像格式化一样，我们使用 DateTimeFormatter 对象来解析日期和时间。同样，有许多可用的内置格式化程序。我们可以使用 `ofPattern()` 方法创建一个使用自定义日期和时间模式的格式化程序。

```java
String dateTimeString = "2020-05-04 22:15:30";
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
Instant instant = Instant.parse(dateTimeString, formatter);
```

上面的代码使用模式“yyyy-MM-dd HH:mm:ss”解析字符串“dateTimeString”。此模式定义了日期和时间字符串的结构。生成的“Instant”对象可以像任何其他“Instant”对象一样使用。

## 管理时区

使用日期和时间时的另一个常见任务是处理时区。日期和时间 API 通过提供“ZoneId”类使处理时区变得容易。此类表示时区标识符。

我们可以使用 `ZoneId` 类的静态 `of()` 方法来获取特定时区的 `ZoneId` 对象。例如，我们可以像这样获取太平洋时区的“ZoneId”对象：

```java
ZoneId zoneId = ZoneId.of("America/Los_Angeles");
```

一旦我们有了一个 ZoneId 对象，我们就可以用它把一个 Instant 对象转换成一个 ZonedDateTime 对象。该对象表示特定时区的日期和时间。

```java
ZonedDateTime zonedDateTime = now.atZone(zoneId);
```

我们还可以使用 `ZoneId` 对象来格式化特定时区的日期和时间字符串。

```java
DateTimeFormatter formatter = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.FULL);
String formattedDateTime = zonedDateTime.format(formatter);
```

## 调整日期和时间

日期和时间 API 的另一个有用特性是能够调整日期和时间。这可以使用 `Instant` 和 `ZonedDateTime` 类的 `with()` 方法来完成。

此方法将“TemporalAdjuster”对象作为参数。此对象定义日期或时间应如何调整。有许多可用的内置调整器，例如 `next()`、`nextOrSame()`、`previous()`、`previousOrSame()` 和 `firstDayOfMonth()`。

```java
Instant instant = now.with(next(DayOfWeek.MONDAY));
```

上面的代码调整了“Instant”对象“now”，使其代表下一个星期一。

## 测量时间

除了处理日期和时间之外，日期和时间 API 还提供了一种测量时间的方法。这对于计算某些操作需要多长时间很有用。

我们可以使用 Duration 类来测量两个 Instant 对象之间的时间量。例如，我们可以像这样测量“now”和“instant”之间的持续时间：

```java
Duration duration = Duration.between(now, instant);
```

然后我们可以使用 `getSeconds()` 方法来获取持续时间中的总秒数。

```java
long seconds = duration.getSeconds();
```

## 结论

Java 的日期和时间 API 是一组用于处理日期和时间的强大工具。它提供了许多可用于在 Java 应用程序中进行精确时间管理的功能。在本文中，我们了解了日期和时间 API 的一些关键特性，以及如何使用它们进行精确的时间管理。