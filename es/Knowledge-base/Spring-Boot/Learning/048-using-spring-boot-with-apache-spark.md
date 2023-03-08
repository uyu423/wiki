---
title: 048: Uso de Spring Boot con Apache Spark
description: 
published: true
date: 2023-02-04T14:32:59.240Z
tags: 
editor: markdown
dateCreated: 2023-02-04T14:32:57.535Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [048: Using Spring Boot with Apache Spark***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/048-using-spring-boot-with-apache-spark)
{.links-list}




# Uso de Spring Boot con Apache Spark

Spark es un potente motor de procesamiento de código abierto creado en torno a la velocidad, la facilidad de uso y el análisis sofisticado. No es de extrañar que la combinación de Spark y Spring Boot sea una opción popular para crear aplicaciones con uso intensivo de datos.

En esta publicación, le mostraremos cómo comenzar a usar Spark y Spring Boot. Cubriremos los aspectos básicos del trabajo con Spark, incluido cómo crear y ejecutar aplicaciones Spark. También le mostraremos cómo usar Spring Boot para que trabajar con Spark sea aún más fácil.

## ¿Qué es Chispa?

Spark es un motor rápido y general para el procesamiento de datos a gran escala. Originalmente fue desarrollado en AMPLab de UC Berkeley, y ahora es un proyecto de Apache con contribuciones de muchas empresas e individuos.

Spark está diseñado para usarse en una amplia gama de aplicaciones, desde ETL de datos simples hasta aprendizaje automático complejo y procesamiento de gráficos. Spark es particularmente adecuado para casos de uso que involucran cálculos iterativos, consultas interactivas o transmisión de datos.

Spark proporciona un amplio conjunto de funciones, incluida la compatibilidad con SQL, DataFrames, conjuntos de datos y una amplia variedad de algoritmos de aprendizaje automático. Además, Spark se puede usar junto con otras herramientas populares de big data, como Hadoop, Cassandra y Kafka.

## Primeros pasos con Spark

Spark se puede usar de varias maneras, incluidas aplicaciones independientes, scripts o como una biblioteca para otros lenguajes de programación. En esta sección, le mostraremos cómo crear y ejecutar una aplicación Spark simple en Scala.

### Creación de una aplicación Spark

El primer paso para crear una aplicación Spark es definir una clase que amplíe la clase SparkConf. La clase SparkConf le permite configurar ajustes de Spark, como la ubicación de su maestro de Spark y la cantidad de memoria que se usará para las aplicaciones de Spark.



clase MySparkConf extiende SparkConf {
   anular def getAll: Map[String, String] = {
     Mapa(
       "chispa.maestro" -> "local[*]",
       "chispa.ejecutor.memoria" -> "1g"
     )
   }
}

A continuación, debe crear una instancia de la clase SparkContext. La clase SparkContext es el principal punto de entrada para las aplicaciones Spark. Representa la conexión a un clúster de Spark y se usa para crear RDD, DataFrames y Datasets.



val sc = nuevo SparkContext(nuevo MySparkConf())

Ahora que tiene un SparkContext, puede comenzar a crear aplicaciones Spark. En este ejemplo, crearemos una aplicación simple que cuente las palabras en un archivo de texto.

Primero, necesitamos leer el archivo de texto usando el método SparkContext.textFile. Este método devuelve un RDD de cadenas, donde cada cadena es una línea del archivo de texto.



val textFile = sc.textFile("/ruta/al/archivo.txt")

A continuación, podemos usar el método RDD.flatMap para dividir cada línea en palabras. El método flatMap devuelve un nuevo RDD que contiene los resultados de aplicar una función a cada elemento del RDD original. En este caso, la función divide cada línea en palabras.



val palabras = textFile.flatMap(línea => línea.split(" "))

Finalmente, podemos usar el método RDD.count para contar el número de palabras en el RDD.



val cuenta = palabras.cuenta()

### Ejecutar una aplicación Spark

Las aplicaciones Spark se pueden ejecutar mediante el script spark-submit. La secuencia de comandos spark-submit toma una serie de argumentos, incluida la ubicación de su aplicación Spark y la cantidad de memoria a usar.

Para ejecutar la aplicación de ejemplo anterior, usaría el siguiente comando:

spark-submit --class MySparkApp --master local[*] --executor-memory 1g /ruta/a/jar/archivo.jar

## Uso de Spring Boot con Spark

Spring Boot es un marco Java popular que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción. Spring Boot es particularmente adecuado para crear microservicios.

Además de simplificar el proceso de creación de aplicaciones Spring independientes, Spring Boot también facilita el trabajo con una amplia variedad de fuentes de datos, incluido Spark.

En esta sección, le mostraremos cómo usar Spring Boot para crear una aplicación Spark. Usaremos la misma aplicación de ejemplo de la sección anterior, pero usaremos Spring Boot para simplificar el proceso de creación y ejecución de la aplicación.

### Creación de una aplicación Spring Boot

El primer paso para crear una aplicación Spring Boot es crear un nuevo proyecto Maven. Puede usar cualquier IDE compatible con Maven para hacer esto.

En el archivo pom.xml del proyecto, debe agregar las siguientes dependencias:

spring-boot-arrancador-padre
spring-boot-arranque-web
spring-boot-arrancador-datos-chispa

La dependencia spring-boot-starter-parent es el POM principal para todas las dependencias de Spring Boot. La dependencia spring-boot-starter-web se usa para agregar compatibilidad con Spring MVC. La dependencia spring-boot-starter-data-spark se usa para agregar compatibilidad con Spark.

A continuación, debe crear una nueva clase que anote con @SpringBootApplication. Esta clase contendrá el método principal para su aplicación.



@SpringBootApplication
clase pública MiAplicación {

   public static void main(String[] args) {
      SpringApplication.run(MyApplication.class, args);
   }
}

La anotación @SpringBootApplication es una anotación conveniente que se usa para agregar todas las siguientes anotaciones a su aplicación:

@Configuration: esta anotación se usa para indicar que una clase contiene información de configuración para una aplicación Spring.

@EnableAutoConfiguration: esta anotación se usa para habilitar la configuración automática de una aplicación Spring.

@ComponentScan: esta anotación se usa para habilitar el escaneo de componentes de una aplicación Spring.

### Crear un trabajo de Spark

Para crear un trabajo de Spark, debe crear una nueva clase que anote con @Configuration y @EnableSpark. La anotación @Configuration se usa para indicar que una clase contiene información de configuración para una aplicación Spring. La anotación @EnableSpark se usa para habilitar Spark en una aplicación Spring.



@Configuración
@EnableSpark
clase pública MySparkJob {

   @autocableado
   SparkContext privado sparkContext;

   @autocableado
   chispaConf privada SparkConf;

   @Frijol
   público SparkJob chispaJob () {
      // ... crea y devuelve SparkJob
   }
}

La anotación @Autowired se usa para inyectar SparkContext y SparkConf en el trabajo de Spark. La anotación @Bean se usa para indicar que un método crea un bean Spring.

En el método sparkJob, debe crear y devolver un SparkJob. Un SparkJob es un componente administrado por Spring que representa una aplicación Spark.



@Configuración
@EnableSpark
clase pública MySparkJob {

   @autocableado
   SparkContext privado sparkContext;

   @autocableado
   chispaConf privada SparkConf;

   @Frijol
   público SparkJob chispaJob () {
      devolver nuevo SparkJob() {
         @Anular
         ejecución de vacío público () {
            // ... ejecuta el trabajo de Spark
         }
      };
   }
}

En el método de ejecución, puede agregar el código Spark para su aplicación. En este ejemplo, usaremos el mismo código de la sección anterior.



@Configuración
@EnableSpark
clase pública MySparkJob {

   @autocableado
   SparkContext privado sparkContext;

   @autocableado
   chispaConf privada SparkConf;

   @Frijol
   público SparkJob chispaJob () {
      devolver nuevo SparkJob() {
         @Anular
         ejecución de vacío público () {
            val textFile = sparkContext.textFile("/ruta/al/archivo.txt")
            val palabras = textFile.flatMap(línea => línea.split(" "))
            val cuenta = palabras.cuenta()
         }
      };
   }
}

### Ejecutar una aplicación Spring Boot

Las aplicaciones Spring Boot se pueden ejecutar con el objetivo spring-boot-run. Este objetivo se puede ejecutar con el complemento Maven o la herramienta de línea de comandos Spring Boot.

Para ejecutar la aplicación de ejemplo anterior, usaría el siguiente comando:

mvn spring-boot:ejecutar

## Conclusión

En esta publicación, le mostramos cómo comenzar a usar Spark y Spring Boot. Hemos cubierto los conceptos básicos de trabajar con Spark, incluido cómo crear y ejecutar aplicaciones Spark. También le mostramos cómo usar Spring Boot para que trabajar con Spark sea aún más fácil.

Si está interesado en obtener más información sobre Spark y Spring Boot, hay varios recursos excelentes disponibles. En particular, recomendamos lo siguiente:

- La guía de inicio rápido de Spark: https://spark.apache.org/docs/latest/quick-start.html
- La documentación de Spring Boot: https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/
- La guía Spark con Spring Boot: https://spring.io/guides/gs/spark-on-spring-boot/