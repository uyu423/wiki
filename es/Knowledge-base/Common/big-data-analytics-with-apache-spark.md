---
title: Análisis de Big Data con Apache Spark
description: 
published: true
date: 2023-02-05T13:18:31.617Z
tags: 
editor: markdown
dateCreated: 2023-02-05T13:18:29.877Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Big Data Analytics with Apache Spark***English** document is available*](/en/Knowledge-base/Common/big-data-analytics-with-apache-spark)
{.links-list}


# Análisis de Big Data con Apache Spark

Con la popularidad cada vez mayor de los macrodatos, la demanda de análisis de macrodatos también va en aumento. Apache Spark es uno de los marcos de procesamiento de big data más populares y se usa ampliamente para el análisis de big data.

Spark es un motor de procesamiento de datos en memoria rápido con sólidas capacidades de transmisión y SQL. Puede manejar el procesamiento de datos por lotes y en tiempo real. Spark es fácil de usar y tiene un amplio conjunto de bibliotecas para procesamiento de datos, aprendizaje automático y procesamiento de gráficos.

En este artículo, discutiremos cómo realizar análisis de big data usando Apache Spark. Cubriremos los siguientes temas:

- Configuración de un entorno de desarrollo Spark
- Carga y procesamiento de datos en Spark
- Chispa SQL
- Transmisión de chispa
- Aprendizaje automático con Spark
- Procesamiento de gráficos con Spark

## Configuración de un entorno de desarrollo de Spark

Spark se puede instalar en un servidor independiente o en un grupo de máquinas. También se puede ejecutar en la nube. En este artículo, asumiremos que tiene una instalación de Spark independiente.

### Requisitos previos

Antes de comenzar, necesitará lo siguiente:

- Una máquina con al menos 4 GB de RAM y suficiente espacio en disco para almacenar los datos que desea procesar.
- Java 8 o superior.
- Apache Spark 2.4 o superior.

### Instalación de Spark

 1. Descargue la última versión de Apache Spark del [sitio web de Spark] (https://spark.apache.org/).
 2. Descomprima el archivo descargado. Esto creará un directorio llamado `spark-2.4.5-bin-hadoop2.7`.
 3. Mueva el directorio `spark-2.4.5-bin-hadoop2.7` a la ubicación donde desea instalar Spark.
 4. Configure la variable de entorno `SPARK_HOME` en el directorio `spark-2.4.5-bin-hadoop2.7`.
 5. Agregue el directorio `$SPARK_HOME/bin` a su variable de entorno `PATH`.

Ahora puede iniciar Spark shell ejecutando el comando `spark-shell`.

## Carga y procesamiento de datos en Spark

Spark puede cargar datos de una variedad de fuentes, incluidos HDFS, S3 y archivos locales. En esta sección, analizaremos cómo cargar datos desde un archivo local y procesarlos en Spark.

Primero, crearemos un archivo de texto llamado `sample.txt` con los siguientes contenidos:

```
This is a sample text file.
```

Ahora podemos cargar este archivo en Spark usando el método `spark.read.text()`:

```scala
val textFile = spark.read.text("sample.txt")
```

La variable `textFile` es un `Dataset[String]` que contiene el contenido del archivo `sample.txt`. Ahora podemos realizar varias operaciones en este conjunto de datos, como filtrado, transformación y agregación.

Por ejemplo, podemos usar el método `filter()` para filtrar las líneas que no contienen la palabra `sample`:

```scala
val filteredTextFile = textFile.filter(line => line.contains("sample"))
```

También podemos usar el método `map()` para transformar el conjunto de datos:

```scala
val mappedTextFile = textFile.map(line => line.toUpperCase())
```

Finalmente, podemos usar el método `groupBy()` para agrupar el conjunto de datos por la longitud de la línea:

```scala
val groupedTextFile = textFile.groupBy(line => line.length)
```

## Chispa SQL

Spark SQL es un módulo de Spark que te permite trabajar con datos estructurados. Proporciona una API DataFrame que se puede usar para cargar datos de una variedad de fuentes, como HDFS, S3 y archivos locales.

En esta sección, discutiremos cómo usar Spark SQL para cargar datos desde un archivo local y procesarlos.

Primero, crearemos un archivo de texto llamado `personas.txt` con los siguientes contenidos:

```
id,name,age
1,john,26
2,mary,29
3,jane,21
4,bob,27
```

Ahora podemos cargar este archivo en un Spark DataFrame usando el método `spark.read.csv()`:

```scala
val peopleDF = spark.read.csv("people.txt")
```

El DataFrame `peopleDF` tiene el siguiente esquema:

```
root
 |-- id: string (nullable = true)
 |-- name: string (nullable = true)
 |-- age: string (nullable = true)
```

Ahora podemos registrar este DataFrame como una vista temporal para que podamos ejecutar consultas SQL en él:

```scala
peopleDF.createOrReplaceTempView("people")
```

Ahora podemos ejecutar consultas SQL en la vista `personas`. Por ejemplo, podemos consultar la vista para encontrar los nombres de todas las personas mayores de 25 años:

```scala
spark.sql("SELECT name FROM people WHERE age > 25").show()
```

que debería dar salida a lo siguiente:

```
+-----+
| name|
+-----+
| john|
| mary|
|  bob|
+-----+
```

## Transmisión de chispas

Spark Streaming es un módulo de Spark que le permite procesar flujos de datos en tiempo real. Puede recibir flujos de datos en vivo de fuentes como Kafka, Flume y Twitter.

En esta sección, analizaremos cómo usar Spark Streaming para procesar una transmisión de datos en vivo desde Twitter.

Primero, deberá crear una aplicación API de Twitter. Puede hacerlo siguiendo las instrucciones de la [documentación para desarrolladores de Twitter] (https://developer.twitter.com/en/docs/basics/apps/overview).

Una vez que haya creado su aplicación de API de Twitter, deberá crear un archivo llamado `twitter.txt` con sus credenciales de API de Twitter. El archivo debe tener el siguiente formato:

```
consumerKey = <your consumer key>
consumerSecret = <your consumer secret>
accessToken = <your access token>
accessTokenSecret = <your access token secret>
```

Ahora puede iniciar Spark Streaming shell ejecutando el siguiente comando:

```
spark-shell --packages org.apache.spark:spark-streaming-twitter_2.11:2.4.5
```

Esto iniciará Spark Shell con el paquete `spark-streaming-twitter_2.11`.

Ahora podemos crear un contexto de Spark Streaming y configurar el directorio del punto de control:

```scala
import org.apache.spark._
import org.apache.spark.streaming._

val ssc = new StreamingContext(sc, Seconds(10))
ssc.checkpoint("checkpoint")
```

Ahora podemos crear una transmisión de Twitter usando el archivo `twitter.txt` que creamos anteriormente:

```scala
import org.apache.spark.streaming.twitter._

val twitterStream = TwitterUtils.createStream(ssc, None, Seq(args(0)))
```

El `twitterStream` es un `DStream[Status]` que contiene el flujo de Twitter en vivo. Ahora podemos realizar varias operaciones en este flujo, como transformación, filtrado y agregación.

Por ejemplo, podemos usar el método `map()` para transformar la transmisión:

```scala
val textStream = twitterStream.map(status => status.getText())
```

Ahora podemos usar el método `foreachRDD()` para procesar el flujo:

```scala
textStream.foreachRDD { (rdd, time) =>
  val count = rdd.count()
  println(s"Received ${count} tweets at time ${time}")
}
```

Finalmente, podemos iniciar el proceso de transmisión:

```scala
ssc.start()
```

## Aprendizaje automático con Spark

Spark MLlib es un módulo de Spark que proporciona varios algoritmos de aprendizaje automático. En esta sección, analizaremos cómo usar Spark MLlib para entrenar un modelo de aprendizaje automático.

Primero, crearemos un archivo de texto llamado `training.txt` con los siguientes contenidos:

```
id,features,label
1,[1.0,0.0,0.0],0.0
2,[0.0,1.0,0.0],1.0
3,[0.0,0.0,1.0],2.0
```

Ahora podemos cargar este archivo en un Spark DataFrame usando el método `spark.read.csv()`:

```scala
val trainingDF = spark.read.csv("training.txt")
```

El DataFrame `trainingDF` tiene el siguiente esquema:

```
root
 |-- id: string (nullable = true)
 |-- features: vector (nullable = true)
 |-- label: double (nullable = true)
```

Ahora podemos crear un objeto `LogisticRegression` y establecer los parámetros:

```scala
import org.apache.spark.ml.classification.LogisticRegression

val lr = new LogisticRegression()
  .setMaxIter(10)
  .setRegParam(0.01)
```

Ahora podemos entrenar el modelo usando el método `fit()`:

```scala
val model = lr.fit(trainingDF)
```

Ahora podemos guardar el modelo entrenado en un archivo:

```scala
model.write.overwrite().save("model")
```

## Procesamiento de gráficos con Spark

Spark GraphX es un módulo de Spark que proporciona varios algoritmos de procesamiento de gráficos. En esta sección, discutiremos cómo usar Spark GraphX para procesar un gráfico.

Primero, crearemos un archivo de texto llamado `edges.txt` con los siguientes contenidos:

```
src,dst,weight
1,2,1.0
2,3,2.0
3,4,3.0
4,1,4.0
```

Ahora podemos cargar este archivo en un Spark DataFrame usando el método `spark.read.csv()`:

```scala
val edgesDF = spark.read.csv("edges.txt")
```

El DataFrame `edgesDF` tiene el siguiente esquema:

```
root
 |-- src: string (nullable = true)
 |-- dst: string (nullable = true)
 |-- weight: double (nullable = true)
```

Ahora podemos crear un objeto `Graph` a partir del marco de datos `edgesDF`:

```scala
import org.apache.spark.graphx._

val graph = Graph.fromEdges(edgesDF, "weight")
```

El `graph` es un `Graph[Double, Double]` que contiene los bordes del marco de datos `edgesDF`. Ahora podemos realizar varias operaciones en este gráfico, como transformación, filtrado y agregación.

Por ejemplo, podemos usar el método `mapEdges()` para transformar los bordes:

```scala
val transformedGraph = graph.mapEdges(e => e.attr * 2)
```

También podemos usar el método `mapVertices()` para transformar los vértices:

```scala
val transformedGraph = graph.mapVertices { (id, attr) =>
  attr * 2
}
```

Finalmente, podemos usar el método `aggregateMessages()` para agregar los bordes:

```scala
val aggregatedGraph = graph.aggregateMessages[Double](
  ctx => ctx.sendToDst(ctx.srcAttr),
  (a, b) => a + b
)
```

## Conclusión

En este artículo, hemos discutido cómo realizar análisis de big data usando Apache Spark. Hemos cubierto los siguientes temas:

- Configuración de un entorno de desarrollo Spark
- Carga y procesamiento de datos en Spark
- Chispa SQL
- Transmisión de chispa
- Aprendizaje automático con Spark
- Procesamiento de gráficos con Spark

## Referencias

- [Documentación de Spark](https://spark.apache.org/docs/latest/)
- [Documentación de Spark SQL](https://spark.apache.org/docs/latest/sql-programming-guide.html)
- [Documentación de transmisión de Spark] (https://spark.apache.org/docs/latest/streaming-programming-guide.html)
- [Documentación de Spark MLlib] (https://spark.apache.org/docs/latest/ml-guide.html)
- [Documentación de Spark GraphX] (https://spark.apache.org/docs/latest/graphx-programming-guide.html)