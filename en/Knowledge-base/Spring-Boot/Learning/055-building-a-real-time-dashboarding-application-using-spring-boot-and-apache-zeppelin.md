---
title: 055: Building a real-time dashboarding application using Spring Boot and Apache Zeppelin
description: 
published: true
date: 2023-02-04T19:33:16.577Z
tags: 
editor: markdown
dateCreated: 2023-02-04T19:33:11.176Z
---

- [055: Creación de una aplicación de tableros en tiempo real con Spring Boot y Apache Zeppelin***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/055-building-a-real-time-dashboarding-application-using-spring-boot-and-apache-zeppelin)
{.links-list}
- [055：使用 Spring Boot 和 Apache Zeppelin 构建实时仪表板应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/055-building-a-real-time-dashboarding-application-using-spring-boot-and-apache-zeppelin)
{.links-list}
- [055: Spring Boot와 Apache Zeppelin을 사용하여 실시간 대시보드 애플리케이션 구축***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/055-building-a-real-time-dashboarding-application-using-spring-boot-and-apache-zeppelin)
{.links-list}


# Building a real-time dashboarding application using Spring Boot and Apache Zeppelin

In this post, we'll show you how to build a real-time dashboarding application using Spring Boot and Apache Zeppelin.

## What is Spring Boot?

Spring Boot is a Java-based framework that provides a simple way to create stand-alone, production-grade Spring-based applications. It is designed to simplify the bootstrapping and development of a new Spring application. 

## What is Apache Zeppelin?

Apache Zeppelin is a web-based notebook that enables interactive data analytics. It provides a rich set of language-specific interpreters that allow you to create data visualizations, run SQL queries, and so on.

## Prerequisites

Before we get started, there are a few things you'll need to have in order to follow along:

- A text editor or IDE. We'll be using Visual Studio Code.
- The Java Development Kit (JDK) version 8 or above.
- Apache Maven.

## Getting Started

First, let's create a new Maven project in our text editor. We'll name it `spring-boot-zeppelin`.

Next, we need to add the following dependencies to our `pom.xml` file:

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

The `spring-boot-starter-web` dependency is used to create a Spring Boot web application. The `zeppelin-server` dependency is used to include the Apache Zeppelin server in our application.

## Creating a Spring Boot Application

Next, we need to create a Spring Boot application. We'll do this by creating a `SpringBootApplication` class and annotating it with the `@SpringBootApplication` annotation.

```java
@SpringBootApplication
public class SpringBootZeppelinApplication {

	public static void main(String[] args) {
		SpringApplication.run(SpringBootZeppelinApplication.class, args);
	}

}
```

The `@SpringBootApplication` annotation is used to enable auto-configuration and component scanning in our Spring Boot application.

## Creating a Zeppelin Notebook

Next, we need to create a Zeppelin notebook. We'll do this by creating a `Notebook` class and annotating it with the `@ZeppelinNotebook` annotation.

```java
@ZeppelinNotebook
public class Notebook {

	// our notebook code will go here

}
```

The `@ZeppelinNotebook` annotation is used to enable Zeppelin notebook auto-configuration in our application.

## Adding Data to our Notebook

Now that we have our notebook created, let's add some data to it. We'll do this by creating a `DataFrame` and adding it to our notebook.

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

The `@DataFrame` annotation is used to indicate that the `data` variable contains data that should be treated as a Zeppelin dataframe.

## Creating a Dashboard

Now that we have our data added to our notebook, let's create a dashboard. We'll do this by creating a `Dashboard` class and annotating it with the `@Dashboard` annotation.

```java
@Dashboard
public class Dashboard {

	// our dashboard code will go here

}
```

The `@Dashboard` annotation is used to enable dashboard auto-configuration in our application.

## Adding a Chart to our Dashboard

Now that we have our dashboard created, let's add a chart to it. We'll do this by creating a `LineChart` and adding it to our dashboard.

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

The `@LineChart` annotation is used to indicate that the `data` variable contains data that should be treated as a line chart. The `name`, `data`, `xField`, and `yField` properties are used to configure the chart.

## Adding a Table to our Dashboard

Now that we have our chart added to our dashboard, let's add a table to it. We'll do this by creating a `Table` and adding it to our dashboard.

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

The `@Table` annotation is used to indicate that the `data` variable contains data that should be treated as a table. The `name` and `data` properties are used to configure the table.

## Adding a Map to our Dashboard

Now that we have our table added to our dashboard, let's add a map to it. We'll do this by creating a `Map` and adding it to our dashboard.

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

The `@Map` annotation is used to indicate that the `data` variable contains data that should be treated as a map. The `name` and `data` properties are used to configure the map.

## Adding a Gauge to our Dashboard

Now that we have our map added to our dashboard, let's add a gauge to it. We'll do this by creating a `Gauge` and adding it to our dashboard.

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

The `@Gauge` annotation is used to indicate that the `data` variable contains data that should be treated as a gauge. The `name`, `data`, `valueField`, `minValue`, and `maxValue` properties are used to configure the gauge.

## Adding a Pie Chart to our Dashboard

Now that we have our gauge added to our dashboard, let's add a pie chart to it. We'll do this by creating a `PieChart` and adding it to our dashboard.

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

The `@PieChart` annotation is used to indicate that the `data` variable contains data that should be treated as a pie chart. The `name`, `data`, and `valueField` properties are used to configure the pie chart.

## Adding a Scatter Plot to our Dashboard

Now that we have our pie chart added to our dashboard, let's add a scatter plot to it. We'll do this by creating a `ScatterPlot` and adding it to our dashboard.

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

The `@ScatterPlot` annotation is used to indicate that the `data` variable contains data that should be treated as a scatter plot. The `name`, `data`, `xField`, and `yField` properties are used to configure the scatter plot.

## Adding a Bar Chart to our Dashboard

Now that we have our scatter plot added to our dashboard, let's add a bar chart to it. We'll do this by creating a `BarChart` and adding it to our dashboard.

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

The `@BarChart` annotation is used to indicate that the `data` variable contains data that should be treated as a bar chart. The `name`, `data`, `xField`, and `yField` properties are used to configure the bar chart.

## Adding a Area Chart to our Dashboard

Now that we have our bar chart added to our dashboard, let's add an area chart to it. We'll do this by creating an `AreaChart` and adding it to our dashboard.

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

The `@AreaChart` annotation is used to indicate that the `data` variable contains data that should be treated as an area chart. The `name`, `data`, `xField`, and `yField` properties are used to configure the area chart.

## Adding a Heatmap to our Dashboard

Now that we have our area chart added to our dashboard, let's add a heatmap to it. We'll do this by creating a `Heatmap` and adding it to our dashboard.

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

The `@Heatmap` annotation is used to indicate that the `data` variable contains data that should be treated as a heatmap. The `name`, `data`, `xField`, and `yField` properties are used to configure the heatmap.

## Adding a Bubble Chart to our Dashboard

Now that we have our heatmap added to our dashboard, let's add a bubble chart to it. We'll do this by creating a `BubbleChart` and adding it to our dashboard.

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

The `@BubbleChart` annotation is used to indicate that the `data` variable contains data that should be treated as a bubble chart. The `name`, `data`, `xField`, `yField`, and `sizeField` properties are used to configure the bubble chart.

## Adding a Bullet Chart to our Dashboard

Now that we have our bubble chart added to our dashboard, let's add a bullet chart to it. We'll do this by creating a `BulletChart` and adding it to our dashboard.

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

The `@BulletChart` annotation is used to indicate that the `data` variable contains data that should be treated as a bullet chart. The `name`, `data`, `valueField`, `minValue`, and `maxValue` properties are used to configure the bullet chart.

## Running our Application

Now that we have our dashboard created, let's run our application. We can do this by running the `mvn spring-boot:run` command from the root of our project.

Once our application has started, we can access our dashboard at http://localhost:8080.

## Conclusion

In this post, we've shown you how to build a real-time dashboarding application using Spring Boot and Apache Zeppelin.