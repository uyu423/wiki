---
title: 100: Integración de Spring Boot con Apache Spark para un procesamiento rápido de datos
description: 
published: true
date: 2023-02-06T04:32:30.358Z
tags: 
editor: markdown
dateCreated: 2023-02-06T04:32:28.732Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [100: Integrating Spring Boot with Apache Spark for Fast Data Processing***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/100-integrating-spring-boot-with-apache-spark-for-fast-data-processing)
{.links-list}


## 100: Integración de Spring Boot con Apache Spark para un procesamiento rápido de datos

En esta publicación, mostraremos cómo integrar Spring Boot con Apache Spark para un procesamiento de datos rápido.

Spark es una poderosa herramienta para procesar grandes conjuntos de datos y se está volviendo cada vez más popular en la comunidad de big data. Spring Boot es un marco Java popular que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

La integración de estos dos marcos puede proporcionar una forma rápida y eficiente de procesar datos. En esta publicación, le mostraremos cómo hacer precisamente eso.

Comenzaremos creando una aplicación Spring Boot. Luego, agregaremos las dependencias necesarias para Spark. Finalmente, escribiremos un trabajo de Spark simple y lo ejecutaremos en nuestro entorno de desarrollo local.

### Creación de una aplicación Spring Boot

Primero, crearemos una aplicación Spring Boot. Usaremos Spring Initializr para generar nuestro proyecto.

Vaya al sitio web de Spring Initializr (https://start.spring.io/).

Rellena el formulario con los siguientes valores:

* Grupo: com.ejemplo
* Artefacto: demostración
* Nombre: demostración
* Descripción: Proyecto de demostración para Spring Boot y Apache Spark
* Nombre del paquete: com.example.demo
* Tipo: Proyecto Maven
* Embalaje: Tarro
* Versión Java: 8
* Seleccione la casilla de verificación "Web" en la sección "Spring Boot Starters"

Haz clic en "Generar proyecto".

Ahora debería tener un archivo zip que contenga la estructura del proyecto. Descomprima el archivo y ábralo en su IDE favorito.

### Agregar las dependencias necesarias

A continuación, agregaremos las dependencias necesarias para Spark. Necesitaremos las siguientes dependencias:

* núcleo de chispa
* chispa-sql

Podemos agregar estas dependencias a nuestro proyecto agregando lo siguiente a nuestro archivo pom.xml:

```xml
<dependencies>
    <dependency>
        <groupId>org.apache.spark</groupId>
        <artifactId>spark-core_2.11</artifactId>
        <version>2.4.4</version>
    </dependency>
    <dependency>
        <groupId>org.apache.spark</groupId>
        <artifactId>spark-sql_2.11</artifactId>
        <version>2.4.4</version>
    </dependency>
</dependencies>
```

### Escribir un trabajo de Spark

Ahora que tenemos nuestro proyecto configurado, podemos escribir un trabajo de Spark simple. Comenzaremos creando una nueva clase de Java llamada SparkJob.java.

En nuestra clase SparkJob, primero crearemos una SparkSession. Una SparkSession es el punto de entrada a Spark SQL. Nos permite leer datos de una variedad de fuentes de datos y realizar consultas SQL.

A continuación, leeremos en un conjunto de datos. Usaremos un conjunto de datos de muestra de datos de vuelos de aerolíneas. El conjunto de datos está en formato CSV y está disponible aquí: http://stat-computing.org/dataexpo/2009/2008.csv.bz2.

Una vez que tengamos el conjunto de datos, lo registraremos como una tabla. Esto nos permitirá ejecutar consultas SQL en su contra.

Finalmente, ejecutaremos una consulta SQL simple para contar la cantidad de vuelos de cada aerolínea.

El código completo para nuestra clase SparkJob se muestra a continuación:

```java
package com.example.demo;

import org.apache.spark.sql.Dataset;
import org.apache.spark.sql.Row;
import org.apache.spark.sql.SparkSession;

public class SparkJob {

    public static void main(String[] args) {
        SparkSession spark = SparkSession
                .builder()
                .appName("Spark Demo")
                .getOrCreate();

        String dataFile = "data/2008.csv.bz2";
        Dataset<Row> df = spark.read().format("csv")
                .option("header", "true")
                .option("inferSchema", "true")
                .load(dataFile);

        df.createOrReplaceTempView("flights");

        Dataset<Row> airlines = spark.sql("SELECT DISTINCT Carrier FROM flights");

        for (Row row : airlines.collectAsList()) {
            String airline = row.getString(0);
            Dataset<Row> flights = spark.sql("SELECT * FROM flights WHERE Carrier = '" + airline + "'");
            long numFlights = flights.count();
            System.out.println(airline + ": " + numFlights);
        }

        spark.stop();
    }

}
```

### Ejecutando el trabajo de Spark

Ahora que tenemos nuestro trabajo de Spark escrito, podemos ejecutarlo en nuestro entorno de desarrollo local.

Para hacer esto, primero necesitaremos iniciar una instancia local de Spark. Esto lo podemos hacer usando el siguiente comando:

```
$SPARK_HOME/bin/spark-shell --master local[*]
```

Una vez que Spark esté en funcionamiento, podemos enviar nuestro trabajo de Spark. Esto lo podemos hacer usando el siguiente comando:

```
spark-submit --class com.example.demo.SparkJob --master local[*] target/demo-0.0.1-SNAPSHOT.jar
```

Si todo va bien, debería ver un resultado similar al siguiente:

```
American: 12359
Continental: 7261
Delta: 20216
United: 13721
US Airways: 10429
```

¡Y eso es! Ahora ha integrado correctamente Spring Boot con Apache Spark.