---
title: 025: Using Spring Boot and Spring Batch for data processing
description: 
published: true
date: 2023-02-03T17:33:30.977Z
tags: 
editor: markdown
dateCreated: 2023-02-03T17:33:26.018Z
---

- [025: uso de Spring Boot y Spring Batch para el procesamiento de datos***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/025-using-spring-boot-and-spring-batch-for-data-processing)
{.links-list}
- [025：使用Spring Boot和Spring Batch进行数据处理***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/025-using-spring-boot-and-spring-batch-for-data-processing)
{.links-list}
- [025: 데이터 처리를 위해 Spring Boot와 Spring Batch 사용하기***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/025-using-spring-boot-and-spring-batch-for-data-processing)
{.links-list}


# Using Spring Boot and Spring Batch for data processing

Spring Boot is a popular framework for building Java applications. It makes it easy to create stand-alone, production-grade Spring-based applications that can be "just run".

Spring Batch is a framework for batch processing jobs. It provides many features out of the box, such as job processing statistics, retrying failed jobs, job chaining, and partitioning.

In this post, we'll show how to use Spring Boot and Spring Batch to process data in a file. We'll read data from a CSV file, process it, and write the results to a new CSV file.

## Setting up the project

We'll start by setting up a new Spring Boot project. We'll use the [Spring Initializr](https://start.spring.io/) to create the project.

![Spring Initializr](initializr.png)

We'll name the project `data-processing`, and we'll select the `Web` and `Batch` dependencies. We'll also use the `Java` version 8.

![Spring Initializr dependencies](initializr-deps.png)

Once the project has been generated, we'll import it into our IDE.

## Configuring Spring Batch

Spring Batch uses a `JobRepository` to store information about jobs and their execution status. The `JobRepository` is implemented using a database.

We'll configure the `JobRepository` to use an in-memory H2 database. We'll add the following dependency to our `pom.xml`:

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

We'll also add the following configuration to our `application.properties`:

```properties
spring.batch.job.enabled=true
spring.batch.job.table-prefix=BATCH_
spring.batch.initializer.enabled=true
```

This will enable the `JobRepository` and create the necessary database tables.

## Creating a job

A Spring Batch job is composed of one or more `Step`s. A `Step` is an independent, self-contained unit of work.

We'll create a job with a single `Step` that reads data from a CSV file, processes it, and writes the results to a new CSV file.

We'll start by creating a `Job` bean:

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

The `JobBuilderFactory` is used to create a `JobBuilder`. The `JobBuilder` is used to create a `Job`.

The `StepBuilderFactory` is used to create a `StepBuilder`. The `StepBuilder` is used to create a `Step`.

The `Job` is composed of a single `Step`. The `Step` is configured to read data from an `ItemReader`, process it using an `ItemProcessor`, and write the results to an `ItemWriter`.

The `Step` is also configured to read and write data in chunks of 10 items.

## Creating an ItemReader

The `ItemReader` is responsible for reading data from a data source.

We'll create a `FlatFileItemReader` to read data from a CSV file:

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

The `FlatFileItemReader` is configured to read data from the `input` file. The `input` file is configured using the `input` property in the `application.properties` file.

The `FlatFileItemReader` is also configured to skip the first line of the file. This is because the first line of the file contains the column headers.

The `FlatFileItemReader` is configured with a `LineMapper`. The `LineMapper` is responsible for mapping a line of data to an object.

We'll create the `LineMapper` bean next:

```java
@Bean
public LineMapper<Data> lineMapper() {
    DefaultLineMapper<Data> lineMapper = new DefaultLineMapper<>();
    lineMapper.setFieldSetMapper(fieldSetMapper());
    lineMapper.setLineTokenizer(lineTokenizer());
    return lineMapper;
}
```

The `DefaultLineMapper` is configured with a `LineTokenizer` and a `FieldSetMapper`.

The `LineTokenizer` is responsible for tokenizing a line of data into fields. We'll create the `LineTokenizer` bean next:

```java
@Bean
public LineTokenizer lineTokenizer() {
    DelimitedLineTokenizer tokenizer = new DelimitedLineTokenizer();
    tokenizer.setNames(new String[]{"id", "name", "age", "city"});
    return tokenizer;
}
```

The `DelimitedLineTokenizer` is configured with the names of the fields. The names of the fields must match the column headers in the CSV file.

The `FieldSetMapper` is responsible for mapping a `FieldSet` to an object. We'll create the `FieldSetMapper` bean next:

```java
@Bean
public FieldSetMapper<Data> fieldSetMapper() {
    BeanWrapperFieldSetMapper<Data> fieldSetMapper = new BeanWrapperFieldSetMapper<>();
    fieldSetMapper.setTargetType(Data.class);
    return fieldSetMapper;
}
```

The `BeanWrapperFieldSetMapper` is configured with the target type. The target type is the type of the object that the `FieldSet` will be mapped to. In our case, the target type is the `Data` class.

## Creating an ItemProcessor

The `ItemProcessor` is responsible for processing data read from the data source.

We'll create a simple `ItemProcessor` that converts the data to uppercase:

```java
@Bean
public ItemProcessor<Data, Data> itemProcessor() {
    return data -> {
        data.setName(data.getName().toUpperCase());
        return data;
    };
}
```

## Creating an ItemWriter

The `ItemWriter` is responsible for writing data to a data sink.

We'll create a `FlatFileItemWriter` to write data to a CSV file:

```java
@Bean
public FlatFileItemWriter<Data> itemWriter(@Value("${output}") Resource resource) {
    FlatFileItemWriter<Data> writer = new FlatFileItemWriter<>();
    writer.setResource(resource);
    writer.setLineAggregator(lineAggregator());
    return writer;
}
```

The `FlatFileItemWriter` is configured to write data to the `output` file. The `output` file is configured using the `output` property in the `application.properties` file.

The `FlatFileItemWriter` is configured with a `LineAggregator`. The `LineAggregator` is responsible for aggregating data into a line.

We'll create the `LineAggregator` bean next:

```java
@Bean
public LineAggregator<Data> lineAggregator() {
    DelimitedLineAggregator<Data> lineAggregator = new DelimitedLineAggregator<>();
    lineAggregator.setDelimiter(",");
    lineAggregator.setFieldExtractor(fieldExtractor());
    return lineAggregator;
}
```

The `DelimitedLineAggregator` is configured with a delimiter and a `FieldExtractor`.

The `FieldExtractor` is responsible for extracting fields from an object. We'll create the `FieldExtractor` bean next:

```java
@Bean
public FieldExtractor<Data> fieldExtractor() {
    BeanWrapperFieldExtractor<Data> fieldExtractor = new BeanWrapperFieldExtractor<>();
    fieldExtractor.setNames(new String[]{"id", "name", "age", "city"});
    return fieldExtractor;
}
```

The `BeanWrapperFieldExtractor` is configured with the names of the fields. The names of the fields must match the column headers in the CSV file.

## Running the job

We can run the job from our IDE, or we can package the application as a JAR file and run it from the command line.

We'll package the application as a JAR file and run it from the command line.

We'll add the following configuration to the `pom.xml` file:

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

This will package the application as a JAR file.

We'll run the following command to package the application:

```
mvn package
```

We'll run the following command to run the application:

```
java -jar target/data-processing-0.0.1-SNAPSHOT.jar
```

## Conclusion

In this post, we've shown how to use Spring Boot and Spring Batch to process data in a file. We've read data from a CSV file, processed it, and written the results to a new CSV file.