---
title: 055: Creación de una aplicación de tableros en tiempo real con Spring Boot y Apache Zeppelin
description: 
published: true
date: 2023-02-04T19:33:12.897Z
tags: 
editor: markdown
dateCreated: 2023-02-04T19:33:11.177Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [055: Building a real-time dashboarding application using Spring Boot and Apache Zeppelin***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/055-building-a-real-time-dashboarding-application-using-spring-boot-and-apache-zeppelin)
{.links-list}


# Creación de una aplicación de tableros en tiempo real usando Spring Boot y Apache Zeppelin

En esta publicación, le mostraremos cómo crear una aplicación de tablero en tiempo real usando Spring Boot y Apache Zeppelin.

## ¿Qué es Spring Boot?

Spring Boot es un marco basado en Java que proporciona una forma sencilla de crear aplicaciones basadas en Spring independientes y de grado de producción. Está diseñado para simplificar el arranque y el desarrollo de una nueva aplicación Spring.

## ¿Qué es Apache Zeppelin?

Apache Zeppelin es un cuaderno basado en la web que permite el análisis de datos interactivo. Proporciona un amplio conjunto de intérpretes específicos del idioma que le permiten crear visualizaciones de datos, ejecutar consultas SQL, etc.

## Requisitos previos

Antes de comenzar, hay algunas cosas que deberá tener para seguir:

- Un editor de texto o IDE. Usaremos Visual Studio Code.
- El kit de desarrollo de Java (JDK) versión 8 o superior.
- Experto Apache.

## Empezando

Primero, creemos un nuevo proyecto Maven en nuestro editor de texto. Lo llamaremos `spring-boot-zeppelin`.

A continuación, debemos agregar las siguientes dependencias a nuestro archivo `pom.xml`:

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

La dependencia `spring-boot-starter-web` se usa para crear una aplicación web Spring Boot. La dependencia `zeppelin-server` se usa para incluir el servidor Apache Zeppelin en nuestra aplicación.

## Creación de una aplicación Spring Boot

A continuación, necesitamos crear una aplicación Spring Boot. Haremos esto creando una clase `SpringBootApplication` y anotándola con la anotación `@SpringBootApplication`.

```java
@SpringBootApplication
public class SpringBootZeppelinApplication {

	public static void main(String[] args) {
		SpringApplication.run(SpringBootZeppelinApplication.class, args);
	}

}
```

La anotación `@SpringBootApplication` se usa para habilitar la configuración automática y el escaneo de componentes en nuestra aplicación Spring Boot.

## Creación de un cuaderno Zeppelin

A continuación, necesitamos crear un cuaderno Zeppelin. Haremos esto creando una clase `Notebook` y anotándola con la anotación `@ZeppelinNotebook`.

```java
@ZeppelinNotebook
public class Notebook {

	// our notebook code will go here

}
```

La anotación `@ZeppelinNotebook` se utiliza para habilitar la configuración automática del portátil Zeppelin en nuestra aplicación.

## Agregando datos a nuestro cuaderno

Ahora que tenemos nuestro cuaderno creado, vamos a agregarle algunos datos. Haremos esto creando un `DataFrame` y agregándolo a nuestro cuaderno.

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

La anotación `@DataFrame` se utiliza para indicar que la variable `data` contiene datos que deben tratarse como un marco de datos de Zeppelin.

## Creación de un panel

Ahora que hemos agregado nuestros datos a nuestro cuaderno, creemos un tablero. Haremos esto creando una clase `Dashboard` y anotándola con la anotación `@Dashboard`.

```java
@Dashboard
public class Dashboard {

	// our dashboard code will go here

}
```

La anotación `@Dashboard` se usa para habilitar la configuración automática del tablero en nuestra aplicación.

## Agregando un Gráfico a nuestro Tablero

Ahora que hemos creado nuestro tablero, agreguemos un gráfico. Haremos esto creando un `LineChart` y agregándolo a nuestro tablero.

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

La anotación `@LineChart` se utiliza para indicar que la variable `data` contiene datos que deben tratarse como un gráfico de líneas. Las propiedades `name`, `data`, `xField` y `yField` se utilizan para configurar el gráfico.

## Agregar una tabla a nuestro tablero

Ahora que hemos agregado nuestro gráfico a nuestro tablero, agreguemos una tabla. Haremos esto creando una `Tabla` y agregándola a nuestro tablero.

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

La anotación `@Table` se utiliza para indicar que la variable `data` contiene datos que deben tratarse como una tabla. Las propiedades `name` y `data` se utilizan para configurar la tabla.

## Agregando un Mapa a nuestro Tablero

Ahora que hemos agregado nuestra tabla a nuestro tablero, agreguemos un mapa. Haremos esto creando un `Mapa` y agregándolo a nuestro tablero.

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

La anotación `@Map` se utiliza para indicar que la variable `data` contiene datos que deben tratarse como un mapa. Las propiedades `name` y `data` se utilizan para configurar el mapa.

## Agregar un indicador a nuestro tablero

Ahora que hemos agregado nuestro mapa a nuestro tablero, agreguemos un indicador. Haremos esto creando un 'Indicador' y agregándolo a nuestro tablero.

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

La anotación `@Gauge` se utiliza para indicar que la variable `data` contiene datos que deben tratarse como un indicador. Las propiedades `name`, `data`, `valueField`, `minValue` y `maxValue` se utilizan para configurar el indicador.

## Agregar un gráfico circular a nuestro tablero

Ahora que hemos agregado nuestro indicador a nuestro tablero, agreguemos un gráfico circular. Haremos esto creando un `PieChart` y agregándolo a nuestro tablero.

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

La anotación `@PieChart` se utiliza para indicar que la variable `data` contiene datos que deben tratarse como un gráfico circular. Las propiedades `name`, `data` y `valueField` se utilizan para configurar el gráfico circular.

## Agregar un diagrama de dispersión a nuestro tablero

Ahora que hemos agregado nuestro gráfico circular a nuestro tablero, agreguemos un diagrama de dispersión. Haremos esto creando un `ScatterPlot` y agregándolo a nuestro tablero.

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

La anotación `@ScatterPlot` se usa para indicar que la variable `data` contiene datos que deben tratarse como un diagrama de dispersión. Las propiedades `name`, `data`, `xField` y `yField` se utilizan para configurar el gráfico de dispersión.

## Agregar un gráfico de barras a nuestro tablero

Ahora que hemos agregado nuestro diagrama de dispersión a nuestro tablero, agreguemos un gráfico de barras. Haremos esto creando un `BarChart` y agregándolo a nuestro tablero.

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

La anotación `@BarChart` se utiliza para indicar que la variable `data` contiene datos que deben tratarse como un gráfico de barras. Las propiedades `name`, `data`, `xField` y `yField` se utilizan para configurar el gráfico de barras.

## Agregar un gráfico de área a nuestro tablero

Ahora que hemos agregado nuestro gráfico de barras a nuestro tablero, agreguemos un gráfico de área. Haremos esto creando un `AreaChart` y agregándolo a nuestro tablero.

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

La anotación `@AreaChart` se utiliza para indicar que la variable `data` contiene datos que deben tratarse como un gráfico de área. Las propiedades `name`, `data`, `xField` y `yField` se utilizan para configurar el gráfico de área.

## Agregando un mapa de calor a nuestro Dashboard

Ahora que hemos agregado nuestro gráfico de área a nuestro tablero, agreguemos un mapa de calor. Haremos esto creando un `Heatmap` y agregándolo a nuestro tablero.

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

La anotación `@Heatmap` se usa para indicar que la variable `data` contiene datos que deben tratarse como un mapa de calor. Las propiedades `name`, `data`, `xField` e `yField` se utilizan para configurar el mapa de calor.

## Agregar un gráfico de burbujas a nuestro tablero

Ahora que hemos agregado nuestro mapa de calor a nuestro tablero, agreguemos un gráfico de burbujas. Haremos esto creando un `BubbleChart` y agregándolo a nuestro tablero.

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

La anotación `@BubbleChart` se utiliza para indicar que la variable `data` contiene datos que deben tratarse como un gráfico de burbujas. Las propiedades `name`, `data`, `xField`, `yField` y `sizeField` se utilizan para configurar el gráfico de burbujas.

## Agregar un gráfico de viñetas a nuestro tablero

Ahora que hemos agregado nuestro gráfico de burbujas a nuestro tablero, agreguemos un gráfico de viñetas. Haremos esto creando un `BulletChart` y agregándolo a nuestro tablero.

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

La anotación `@BulletChart` se utiliza para indicar que la variable `data` contiene datos que deben tratarse como un gráfico de viñetas. Las propiedades `name`, `data`, `valueField`, `minValue` y `maxValue` se utilizan para configurar el gráfico de viñetas.

## Ejecutando nuestra aplicación

Ahora que tenemos nuestro tablero creado, ejecutemos nuestra aplicación. Podemos hacer esto ejecutando el comando `mvn spring-boot:run` desde la raíz de nuestro proyecto.

Una vez iniciada nuestra aplicación, podemos acceder a nuestro panel de control en http://localhost:8080.

## Conclusión

En esta publicación, le mostramos cómo crear una aplicación de tablero en tiempo real usando Spring Boot y Apache Zeppelin.