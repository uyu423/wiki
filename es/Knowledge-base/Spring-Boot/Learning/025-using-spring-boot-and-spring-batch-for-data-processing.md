---
title: 025: uso de Spring Boot y Spring Batch para el procesamiento de datos
description: 
published: true
date: 2023-02-03T17:33:27.667Z
tags: 
editor: markdown
dateCreated: 2023-02-03T17:33:26.016Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [025: Using Spring Boot and Spring Batch for data processing***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/025-using-spring-boot-and-spring-batch-for-data-processing)
{.links-list}


# Uso de Spring Boot y Spring Batch para el procesamiento de datos

Spring Boot es un marco popular para crear aplicaciones Java. Facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción que se pueden "simplemente ejecutar".

Spring Batch es un marco para trabajos de procesamiento por lotes. Proporciona muchas funciones listas para usar, como estadísticas de procesamiento de trabajos, reintentos de trabajos fallidos, encadenamiento de trabajos y creación de particiones.

En esta publicación, mostraremos cómo usar Spring Boot y Spring Batch para procesar datos en un archivo. Leeremos los datos de un archivo CSV, los procesaremos y escribiremos los resultados en un nuevo archivo CSV.

## Configuración del proyecto

Comenzaremos configurando un nuevo proyecto Spring Boot. Usaremos [Spring Initializr](https://start.spring.io/) para crear el proyecto.

![Inicializar resorte](inicializar.png)

Nombraremos al proyecto `procesamiento de datos` y seleccionaremos las dependencias `Web` y `Batch`. También usaremos la versión 8 de `Java`.

![Dependencias de Spring Initializr](initializr-deps.png)

Una vez generado el proyecto, lo importaremos a nuestro IDE.

## Configuración de Spring Batch

Spring Batch usa un `JobRepository` para almacenar información sobre los trabajos y su estado de ejecución. El `JobRepository` se implementa utilizando una base de datos.

Configuraremos `JobRepository` para usar una base de datos H2 en memoria. Agregaremos la siguiente dependencia a nuestro `pom.xml`:

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

También agregaremos la siguiente configuración a nuestra `application.properties`:

```properties
spring.batch.job.enabled=true
spring.batch.job.table-prefix=BATCH_
spring.batch.initializer.enabled=true
```

Esto habilitará el `Repositorio de trabajos` y creará las tablas de base de datos necesarias.

## Creando un trabajo

Un trabajo de Spring Batch se compone de uno o más 'Pasos'. Un 'Paso' es una unidad de trabajo independiente y autónoma.

Crearemos un trabajo con un solo `Paso` que lea datos de un archivo CSV, los procese y escriba los resultados en un nuevo archivo CSV.

Comenzaremos creando un bean `Job`:

```java
@Bean
public Job job(JobBuilderFactory jobBuilderFactory,
        StepBuilderFactory stepBuilderFactory,
        ItemReader<Data> itemReader,
        ItemProcessor<Data, Data> itemProcessor,
        ItemWriter<Data> itemWriter) {

    Step step = stepBuilderFactory.get("step")
            .<Data, Data>chunk(10)
            .reader(itemReader)
            .processor(itemProcessor)
            .writer(itemWriter)
            .build();

    return jobBuilderFactory.get("job")
            .start(step)
            .build();
}
```

La `JobBuilderFactory` se utiliza para crear un `JobBuilder`. El `JobBuilder` se utiliza para crear un `Trabajo`.

La `StepBuilderFactory` se usa para crear un `StepBuilder`. El `StepBuilder` se utiliza para crear un `Paso`.

El 'Trabajo' se compone de un solo 'Paso'. El 'Paso' está configurado para leer datos de un 'ItemReader', procesarlos usando un 'ItemProcessor' y escribir los resultados en un 'ItemWriter'.

El `Paso` también está configurado para leer y escribir datos en fragmentos de 10 elementos.

## Creando un ItemReader

El `ItemReader` es responsable de leer datos de una fuente de datos.

Crearemos un `FlatFileItemReader` para leer datos de un archivo CSV:

```java
@Bean
public FlatFileItemReader<Data> itemReader(@Value("${input}") Resource resource) {
    FlatFileItemReader<Data> reader = new FlatFileItemReader<>();
    reader.setResource(resource);
    reader.setLinesToSkip(1);
    reader.setLineMapper(lineMapper());
    return reader;
}
```

El `FlatFileItemReader` está configurado para leer datos del archivo de `entrada`. El archivo `input` se configura usando la propiedad `input` en el archivo `application.properties`.

El `FlatFileItemReader` también está configurado para omitir la primera línea del archivo. Esto se debe a que la primera línea del archivo contiene los encabezados de las columnas.

El `FlatFileItemReader` está configurado con un `LineMapper`. El `LineMapper` es responsable de mapear una línea de datos a un objeto.

A continuación crearemos el bean `LineMapper`:

```java
@Bean
public LineMapper<Data> lineMapper() {
    DefaultLineMapper<Data> lineMapper = new DefaultLineMapper<>();
    lineMapper.setFieldSetMapper(fieldSetMapper());
    lineMapper.setLineTokenizer(lineTokenizer());
    return lineMapper;
}
```

El `DefaultLineMapper` está configurado con un `LineTokenizer` y un `FieldSetMapper`.

El `LineTokenizer` es responsable de tokenizar una línea de datos en campos. A continuación, crearemos el bean `LineTokenizer`:

```java
@Bean
public LineTokenizer lineTokenizer() {
    DelimitedLineTokenizer tokenizer = new DelimitedLineTokenizer();
    tokenizer.setNames(new String[]{"id", "name", "age", "city"});
    return tokenizer;
}
```

El `DelimitedLineTokenizer` se configura con los nombres de los campos. Los nombres de los campos deben coincidir con los encabezados de columna en el archivo CSV.

El `FieldSetMapper` es responsable de mapear un `FieldSet` a un objeto. A continuación, crearemos el bean `FieldSetMapper`:

```java
@Bean
public FieldSetMapper<Data> fieldSetMapper() {
    BeanWrapperFieldSetMapper<Data> fieldSetMapper = new BeanWrapperFieldSetMapper<>();
    fieldSetMapper.setTargetType(Data.class);
    return fieldSetMapper;
}
```

El `BeanWrapperFieldSetMapper` está configurado con el tipo de destino. El tipo de destino es el tipo de objeto al que se asignará el `FieldSet`. En nuestro caso, el tipo de destino es la clase `Data`.

## Creando un ItemProcessor

El `ItemProcessor` es responsable de procesar los datos leídos desde la fuente de datos.

Crearemos un `ItemProcessor` simple que convierte los datos a mayúsculas:

```java
@Bean
public ItemProcessor<Data, Data> itemProcessor() {
    return data -> {
        data.setName(data.getName().toUpperCase());
        return data;
    };
}
```

## Creando un ItemWriter

El `ItemWriter` es responsable de escribir datos en un receptor de datos.

Crearemos un `FlatFileItemWriter` para escribir datos en un archivo CSV:

```java
@Bean
public FlatFileItemWriter<Data> itemWriter(@Value("${output}") Resource resource) {
    FlatFileItemWriter<Data> writer = new FlatFileItemWriter<>();
    writer.setResource(resource);
    writer.setLineAggregator(lineAggregator());
    return writer;
}
```

El `FlatFileItemWriter` está configurado para escribir datos en el archivo de `salida`. El archivo `output` se configura usando la propiedad `output` en el archivo `application.properties`.

El `FlatFileItemWriter` está configurado con un `LineAggregator`. El `LineAggregator` es responsable de agregar datos en una línea.

A continuación crearemos el bean `LineAggregator`:

```java
@Bean
public LineAggregator<Data> lineAggregator() {
    DelimitedLineAggregator<Data> lineAggregator = new DelimitedLineAggregator<>();
    lineAggregator.setDelimiter(",");
    lineAggregator.setFieldExtractor(fieldExtractor());
    return lineAggregator;
}
```

El `DelimitedLineAggregator` está configurado con un delimitador y un `FieldExtractor`.

El `FieldExtractor` es responsable de extraer campos de un objeto. A continuación crearemos el bean `FieldExtractor`:

```java
@Bean
public FieldExtractor<Data> fieldExtractor() {
    BeanWrapperFieldExtractor<Data> fieldExtractor = new BeanWrapperFieldExtractor<>();
    fieldExtractor.setNames(new String[]{"id", "name", "age", "city"});
    return fieldExtractor;
}
```

El `BeanWrapperFieldExtractor` se configura con los nombres de los campos. Los nombres de los campos deben coincidir con los encabezados de columna en el archivo CSV.

## Ejecutando el trabajo

Podemos ejecutar el trabajo desde nuestro IDE, o podemos empaquetar la aplicación como un archivo JAR y ejecutarlo desde la línea de comandos.

Empaquetaremos la aplicación como un archivo JAR y la ejecutaremos desde la línea de comandos.

Agregaremos la siguiente configuración al archivo `pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

Esto empaquetará la aplicación como un archivo JAR.

Ejecutaremos el siguiente comando para empaquetar la aplicación:

```
mvn package
```

Ejecutaremos el siguiente comando para ejecutar la aplicación:

```
java -jar target/data-processing-0.0.1-SNAPSHOT.jar
```

## Conclusión

En esta publicación, mostramos cómo usar Spring Boot y Spring Batch para procesar datos en un archivo. Leímos datos de un archivo CSV, los procesamos y escribimos los resultados en un nuevo archivo CSV.