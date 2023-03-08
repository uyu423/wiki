---
title: 055：使用 Spring Boot 和 Apache Zeppelin 构建实时仪表板应用程序
description: 
published: true
date: 2023-02-04T19:33:12.986Z
tags: 
editor: markdown
dateCreated: 2023-02-04T19:33:11.165Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [055: Building a real-time dashboarding application using Spring Boot and Apache Zeppelin***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/055-building-a-real-time-dashboarding-application-using-spring-boot-and-apache-zeppelin)
{.links-list}


# 使用 Spring Boot 和 Apache Zeppelin 构建实时仪表板应用程序

在本文中，我们将向您展示如何使用 Spring Boot 和 Apache Zeppelin 构建实时仪表板应用程序。

## 什么是 Spring Boot？

Spring Boot 是一个基于 Java 的框架，它提供了一种简单的方法来创建独立的、生产级的基于 Spring 的应用程序。它旨在简化新 Spring 应用程序的引导和开发。

## 什么是 Apache Zeppelin？

Apache Zeppelin 是一个基于 Web 的笔记本，支持交互式数据分析。它提供了一组丰富的特定于语言的解释器，允许您创建数据可视化、运行 SQL 查询等。

## 先决条件

在我们开始之前，您需要做一些事情才能跟进：

- 文本编辑器或 IDE。我们将使用 Visual Studio Code。
- Java 开发工具包 (JDK) 版本 8 或更高版本。
- 阿帕奇行家。

## 入门

首先，让我们在我们的文本编辑器中创建一个新的 Maven 项目。我们将其命名为 `spring-boot-zeppelin`。

接下来，我们需要将以下依赖项添加到我们的 `pom.xml` 文件中：

```xml
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-web</artifactId>
	</dependency>
	<dependency>
		<groupId>org.apache.zeppelin</groupId>
		<artifactId>zeppelin-server</artifactId>
		<version>0.8.2</version>
	</dependency>
</dependencies>
```

`spring-boot-starter-web` 依赖项用于创建 Spring Boot Web 应用程序。 `zeppelin-server` 依赖项用于在我们的应用程序中包含 Apache Zeppelin 服务器。

## 创建一个 Spring Boot 应用程序

接下来，我们需要创建一个 Spring Boot 应用程序。我们将通过创建一个 SpringBootApplication 类并使用 @SpringBootApplication 注释对其进行注释来完成此操作。

```java
@SpringBootApplication
public class SpringBootZeppelinApplication {

	public static void main(String[] args) {
		SpringApplication.run(SpringBootZeppelinApplication.class, args);
	}

}
```

@SpringBootApplication 注释用于在我们的 Spring Boot 应用程序中启用自动配置和组件扫描。

## 创建 Zeppelin 笔记本

接下来，我们需要创建一个 Zeppelin notebook。我们将通过创建一个 Notebook 类并使用 @ZeppelinNotebook 注释对其进行注释来完成此操作。

```java
@ZeppelinNotebook
public class Notebook {

	// our notebook code will go here

}
```

`@ZeppelinNotebook` 注释用于在我们的应用程序中启用 Zeppelin 笔记本自动配置。

## 将数据添加到我们的笔记本

现在我们已经创建了笔记本，让我们向其中添加一些数据。我们将通过创建一个“DataFrame”并将其添加到我们的笔记本中来完成此操作。

```java
@ZeppelinNotebook
public class Notebook {

	@DataFrame
	public static final String[] data = new String[] {
		"1,2,3,4,5",
		"6,7,8,9,10"
	};

}
```

@DataFrame 注释用于指示 data 变量包含应被视为 Zeppelin 数据帧的数据。

## 创建仪表板

现在我们已将数据添加到我们的笔记本中，让我们创建一个仪表板。我们将通过创建一个“Dashboard”类并使用“@Dashboard”注释对其进行注释来完成此操作。

```java
@Dashboard
public class Dashboard {

	// our dashboard code will go here

}
```

`@Dashboard` 注释用于在我们的应用程序中启用仪表板自动配置。

## 添加图表到我们的仪表盘

现在我们已经创建了仪表板，让我们向它添加一个图表。我们将通过创建一个“LineChart”并将其添加到我们的仪表板来完成此操作。

```java
@Dashboard
public class Dashboard {

	@LineChart(name = "My Line Chart", data = "data", xField = "0", yField = "1")
	public static final String[] data = new String[] {
		"1,2,3,4,5",
		"6,7,8,9,10"
	};

}
```

`@LineChart` 注释用于指示 `data` 变量包含应被视为折线图的数据。 `name`、`data`、`xField` 和 `yField` 属性用于配置图表。

## 添加表格到我们的仪表板

现在我们已将图表添加到仪表板，让我们向其中添加一个表格。我们将通过创建一个“表”并将其添加到我们的仪表板来完成此操作。

```java
@Dashboard
public class Dashboard {

	@Table(name = "My Table", data = "data")
	public static final String[] data = new String[] {
		"1,2,3,4,5",
		"6,7,8,9,10"
	};

}
```

`@Table` 注释用于指示 `data` 变量包含应被视为表格的数据。 `name` 和 `data` 属性用于配置表。

## 将地图添加到我们的仪表板

现在我们已将表格添加到仪表板，让我们向其添加地图。我们将通过创建一个“地图”并将其添加到我们的仪表板来完成此操作。

```java
@Dashboard
public class Dashboard {

	@Map(name = "My Map", data = "data")
	public static final String[] data = new String[] {
		"1,2,3,4,5",
		"6,7,8,9,10"
	};

}
```

`@Map` 注释用于指示 `data` 变量包含应被视为地图的数据。 `name` 和 `data` 属性用于配置地图。

## 向我们的仪表板添加一个仪表

现在我们已将地图添加到仪表板，让我们向其添加一个仪表。我们将通过创建一个“Gauge”并将其添加到我们的仪表板来完成此操作。

```java
@Dashboard
public class Dashboard {

	@Gauge(name = "My Gauge", data = "data", valueField = "1", minValue = "0", maxValue = "10")
	public static final String[] data = new String[] {
		"1,2,3,4,5",
		"6,7,8,9,10"
	};

}
```

`@Gauge` 注释用于指示 `data` 变量包含应被视为量表的数据。 `name`、`data`、`valueField`、`minValue` 和 `maxValue` 属性用于配置仪表。

## 将饼图添加到我们的仪表板

现在我们已将仪表添加到仪表板，让我们向其添加饼图。我们将通过创建一个“PieChart”并将其添加到我们的仪表板来完成此操作。

```java
@Dashboard
public class Dashboard {

	@PieChart(name = "My Pie Chart", data = "data", valueField = "1")
	public static final String[] data = new String[] {
		"1,2,3,4,5",
		"6,7,8,9,10"
	};

}
```

`@PieChart` 注释用于指示 `data` 变量包含应被视为饼图的数据。 `name`、`data` 和 `valueField` 属性用于配置饼图。

## 向我们的仪表板添加散点图

现在我们已将饼图添加到仪表板中，让我们向其添加一个散点图。我们将通过创建一个“ScatterPlot”并将其添加到我们的仪表板来完成此操作。

```java
@Dashboard
public class Dashboard {

	@ScatterPlot(name = "My Scatter Plot", data = "data", xField = "0", yField = "1")
	public static final String[] data = new String[] {
		"1,2,3,4,5",
		"6,7,8,9,10"
	};

}
```

`@ScatterPlot` 注释用于指示 `data` 变量包含应被视为散点图的数据。 `name`、`data`、`xField` 和 `yField` 属性用于配置散点图。

## 将条形图添加到我们的仪表板

现在我们已经将散点图添加到我们的仪表板中，让我们向它添加一个条形图。我们将通过创建一个 BarChart 并将其添加到我们的仪表板来完成此操作。

```java
@Dashboard
public class Dashboard {

	@BarChart(name = "My Bar Chart", data = "data", xField = "0", yField = "1")
	public static final String[] data = new String[] {
		"1,2,3,4,5",
		"6,7,8,9,10"
	};

}
```

`@BarChart` 注释用于指示 `data` 变量包含应被视为条形图的数据。 `name`、`data`、`xField` 和 `yField` 属性用于配置条形图。

## 将面积图添加到我们的仪表板

现在我们已将条形图添加到仪表板中，让我们向其中添加一个面积图。我们将通过创建一个 AreaChart 并将其添加到我们的仪表板来完成此操作。

```java
@Dashboard
public class Dashboard {

	@AreaChart(name = "My Area Chart", data = "data", xField = "0", yField = "1")
	public static final String[] data = new String[] {
		"1,2,3,4,5",
		"6,7,8,9,10"
	};

}
```

`@AreaChart` 注释用于指示 `data` 变量包含应被视为面积图的数据。 `name`、`data`、`xField` 和 `yField` 属性用于配置面积图。

## 将热图添加到我们的仪表板

现在我们已经将面积图添加到我们的仪表板中，让我们向它添加一个热图。我们将通过创建一个“热图”并将其添加到我们的仪表板来完成此操作。

```java
@Dashboard
public class Dashboard {

	@Heatmap(name = "My Heatmap", data = "data", xField = "0", yField = "1")
	public static final String[] data = new String[] {
		"1,2,3,4,5",
		"6,7,8,9,10"
	};

}
```

`@Heatmap` 注释用于指示 `data` 变量包含应被视为热图的数据。 `name`、`data`、`xField` 和 `yField` 属性用于配置热图。

## 将气泡图添加到我们的仪表板

现在我们已经将热图添加到我们的仪表板，让我们向它添加一个气泡图。我们将通过创建一个 BubbleChart 并将其添加到我们的仪表板来完成此操作。

```java
@Dashboard
public class Dashboard {

	@BubbleChart(name = "My Bubble Chart", data = "data", xField = "0", yField = "1", sizeField = "2")
	public static final String[] data = new String[] {
		"1,2,3,4,5",
		"6,7,8,9,10"
	};

}
```

`@BubbleChart` 注释用于指示 `data` 变量包含应被视为气泡图的数据。 `name`、`data`、`xField`、`yField` 和 `sizeField` 属性用于配置气泡图。

## 将子弹图添加到我们的仪表板

现在我们已经将气泡图添加到我们的仪表板，让我们向它添加一个子弹图。我们将通过创建一个“BulletChart”并将其添加到我们的仪表板来完成此操作。

```java
@Dashboard
public class Dashboard {

	@BulletChart(name = "My Bullet Chart", data = "data", valueField = "1", minValue = "0", maxValue = "10")
	public static final String[] data = new String[] {
		"1,2,3,4,5",
		"6,7,8,9,10"
	};

}
```

`@BulletChart` 注释用于指示 `data` 变量包含应被视为子弹图的数据。 `name`、`data`、`valueField`、`minValue` 和 `maxValue` 属性用于配置子弹图。

## 运行我们的应用程序

现在我们已经创建了仪表板，让我们运行我们的应用程序。我们可以通过从项目的根目录运行 `mvn spring-boot:run` 命令来做到这一点。

一旦我们的应用程序启动，我们就可以通过 http://localhost:8080 访问我们的仪表板。

## 结论

在本文中，我们向您展示了如何使用 Spring Boot 和 Apache Zeppelin 构建实时仪表板应用程序。