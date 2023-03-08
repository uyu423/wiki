---
title: 055: Spring Boot와 Apache Zeppelin을 사용하여 실시간 대시보드 애플리케이션 구축
description: 
published: true
date: 2023-02-04T19:33:12.989Z
tags: 
editor: markdown
dateCreated: 2023-02-04T19:33:11.174Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [055: Building a real-time dashboarding application using Spring Boot and Apache Zeppelin***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/055-building-a-real-time-dashboarding-application-using-spring-boot-and-apache-zeppelin)
{.links-list}


# Spring Boot 및 Apache Zeppelin을 사용하여 실시간 대시보드 애플리케이션 구축

이 게시물에서는 Spring Boot 및 Apache Zeppelin을 사용하여 실시간 대시보드 애플리케이션을 빌드하는 방법을 보여줍니다.

## 스프링부트란?

Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 만드는 간단한 방법을 제공하는 Java 기반 프레임워크입니다. 새 Spring 애플리케이션의 부트스트래핑 및 개발을 단순화하도록 설계되었습니다.

## 아파치 제플린이란?

Apache Zeppelin은 대화형 데이터 분석을 지원하는 웹 기반 노트북입니다. 데이터 시각화를 생성하고 SQL 쿼리를 실행하는 등의 작업을 수행할 수 있는 풍부한 언어별 인터프리터 세트를 제공합니다.

## 전제 조건

시작하기 전에 따라하기 위해 필요한 몇 가지 사항이 있습니다.

- 텍스트 편집기 또는 IDE. 우리는 Visual Studio Code를 사용할 것입니다.
- JDK(Java Development Kit) 버전 8 이상.
- 아파치 메이븐.

## 시작하기

먼저 텍스트 편집기에서 새 Maven 프로젝트를 만듭니다. 이름을 `spring-boot-zeppelin`으로 지정하겠습니다.

다음으로 `pom.xml` 파일에 다음 종속성을 추가해야 합니다.

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

`spring-boot-starter-web` 종속성은 Spring Boot 웹 애플리케이션을 만드는 데 사용됩니다. `zeppelin-server` 종속성은 애플리케이션에 Apache Zeppelin 서버를 포함하는 데 사용됩니다.

## 스프링 부트 애플리케이션 만들기

다음으로 Spring Boot 애플리케이션을 만들어야 합니다. 이를 위해 `SpringBootApplication` 클래스를 생성하고 `@SpringBootApplication` 주석으로 주석을 추가합니다.

```java
@SpringBootApplication
public class SpringBootZeppelinApplication {

	public static void main(String[] args) {
		SpringApplication.run(SpringBootZeppelinApplication.class, args);
	}

}
```

`@SpringBootApplication` 주석은 Spring Boot 애플리케이션에서 자동 구성 및 구성 요소 스캔을 활성화하는 데 사용됩니다.

## 제플린 노트북 만들기

다음으로 Zeppelin 노트북을 만들어야 합니다. 이를 위해 `Notebook` 클래스를 만들고 `@ZeppelinNotebook` 주석으로 주석을 추가합니다.

```java
@ZeppelinNotebook
public class Notebook {

	// our notebook code will go here

}
```

`@ZeppelinNotebook` 주석은 애플리케이션에서 Zeppelin 노트북 자동 구성을 활성화하는 데 사용됩니다.

## 노트북에 데이터 추가

이제 노트북을 만들었으니 데이터를 추가해 보겠습니다. `DataFrame`을 생성하고 노트북에 추가하여 이를 수행합니다.

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

`@DataFrame` 주석은 `data` 변수에 Zeppelin 데이터 프레임으로 취급되어야 하는 데이터가 포함되어 있음을 나타내는 데 사용됩니다.

## 대시보드 만들기

이제 노트북에 데이터를 추가했으므로 대시보드를 생성해 보겠습니다. 이를 위해 `Dashboard` 클래스를 생성하고 `@Dashboard` 주석으로 주석을 추가합니다.

```java
@Dashboard
public class Dashboard {

	// our dashboard code will go here

}
```

`@Dashboard` 주석은 애플리케이션에서 대시보드 자동 구성을 활성화하는 데 사용됩니다.

## 대시보드에 차트 추가하기

이제 대시보드가 생성되었으므로 차트를 추가해 보겠습니다. `LineChart`를 생성하고 대시보드에 추가하여 이 작업을 수행합니다.

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

`@LineChart` 주석은 `data` 변수에 라인 차트로 처리되어야 하는 데이터가 포함되어 있음을 나타내는 데 사용됩니다. `name`, `data`, `xField` 및 `yField` 속성은 차트를 구성하는 데 사용됩니다.

## 대시보드에 테이블 추가

이제 대시보드에 차트가 추가되었으므로 테이블을 추가해 보겠습니다. 이를 위해 `Table`을 생성하고 대시보드에 추가합니다.

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

`@Table` 주석은 `data` 변수에 테이블로 취급되어야 하는 데이터가 포함되어 있음을 나타내는 데 사용됩니다. `name` 및 `data` 속성은 테이블을 구성하는 데 사용됩니다.

## 대시보드에 지도 추가

대시보드에 테이블을 추가했으므로 테이블에 지도를 추가해 보겠습니다. '지도'를 만들고 대시보드에 추가하여 이 작업을 수행합니다.

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

`@Map` 주석은 `data` 변수에 맵으로 처리되어야 하는 데이터가 포함되어 있음을 나타내는 데 사용됩니다. `name` 및 `data` 속성은 맵을 구성하는 데 사용됩니다.

## 대시보드에 게이지 추가

이제 지도가 대시보드에 추가되었으므로 게이지를 추가해 보겠습니다. 이를 위해 `Gauge`를 생성하고 대시보드에 추가합니다.

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

`@Gauge` 주석은 `data` 변수에 게이지로 취급되어야 하는 데이터가 포함되어 있음을 나타내는 데 사용됩니다. `name`, `data`, `valueField`, `minValue` 및 `maxValue` 속성은 게이지를 구성하는 데 사용됩니다.

## 대시보드에 파이 차트 추가하기

대시보드에 게이지가 추가되었으므로 파이 차트를 추가해 보겠습니다. 'PieChart'를 만들어 대시보드에 추가하여 이 작업을 수행합니다.

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

`@PieChart` 주석은 `data` 변수에 원형 차트로 처리되어야 하는 데이터가 포함되어 있음을 나타내는 데 사용됩니다. `name`, `data` 및 `valueField` 속성은 원형 차트를 구성하는 데 사용됩니다.

## 대시보드에 산점도 추가

이제 원형 차트가 대시보드에 추가되었으므로 산점도를 추가해 보겠습니다. 이를 위해 `ScatterPlot`을 생성하고 대시보드에 추가합니다.

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

`@ScatterPlot` 주석은 `data` 변수에 산점도로 처리되어야 하는 데이터가 포함되어 있음을 나타내는 데 사용됩니다. `name`, `data`, `xField` 및 `yField` 속성은 산점도를 구성하는 데 사용됩니다.

## 대시보드에 막대 차트 추가

이제 산점도가 대시보드에 추가되었으므로 여기에 막대 차트를 추가해 보겠습니다. `BarChart`를 생성하고 대시보드에 추가하여 이 작업을 수행합니다.

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

`@BarChart` 주석은 `data` 변수에 막대 차트로 처리되어야 하는 데이터가 포함되어 있음을 나타내는 데 사용됩니다. `name`, `data`, `xField` 및 `yField` 속성은 막대 차트를 구성하는 데 사용됩니다.

## 대시보드에 영역 차트 추가

막대형 차트가 대시보드에 추가되었으므로 영역 차트를 추가해 보겠습니다. `AreaChart`를 생성하고 대시보드에 추가하여 이 작업을 수행합니다.

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

`@AreaChart` 주석은 `data` 변수에 영역 차트로 취급되어야 하는 데이터가 포함되어 있음을 나타내는 데 사용됩니다. `name`, `data`, `xField` 및 `yField` 속성은 영역 차트를 구성하는 데 사용됩니다.

## 대시보드에 히트맵 추가하기

이제 대시보드에 영역 차트가 추가되었으므로 여기에 히트맵을 추가해 보겠습니다. 이를 위해 '히트맵'을 생성하고 대시보드에 추가합니다.

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

`@Heatmap` 주석은 `data` 변수에 히트맵으로 처리되어야 하는 데이터가 포함되어 있음을 나타내는 데 사용됩니다. `name`, `data`, `xField` 및 `yField` 속성은 히트맵을 구성하는 데 사용됩니다.

## 대시보드에 거품형 차트 추가하기

히트맵이 대시보드에 추가되었으므로 거품형 차트를 추가해 보겠습니다. 이를 위해 `BubbleChart`를 생성하고 대시보드에 추가합니다.

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

`@BubbleChart` 주석은 `data` 변수에 거품형 차트로 취급되어야 하는 데이터가 포함되어 있음을 나타내는 데 사용됩니다. `name`, `data`, `xField`, `yField` 및 `sizeField` 속성은 거품형 차트를 구성하는 데 사용됩니다.

## 대시보드에 불릿 차트 추가하기

거품형 차트가 대시보드에 추가되었으므로 불릿 차트를 추가해 보겠습니다. 이를 위해 `BulletChart`를 생성하고 대시보드에 추가합니다.

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

`@BulletChart` 주석은 `data` 변수에 불릿 차트로 처리되어야 하는 데이터가 포함되어 있음을 나타내는 데 사용됩니다. `name`, `data`, `valueField`, `minValue` 및 `maxValue` 속성은 불릿 차트를 구성하는 데 사용됩니다.

## 애플리케이션 실행

이제 대시보드가 생성되었으므로 애플리케이션을 실행해 보겠습니다. 프로젝트의 루트에서 `mvn spring-boot:run` 명령을 실행하여 이를 수행할 수 있습니다.

애플리케이션이 시작되면 http://localhost:8080에서 대시보드에 액세스할 수 있습니다.

## 결론

이 게시물에서는 Spring Boot 및 Apache Zeppelin을 사용하여 실시간 대시보드 애플리케이션을 빌드하는 방법을 보여주었습니다.