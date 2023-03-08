---
title: 025：使用Spring Boot和Spring Batch进行数据处理
description: 
published: true
date: 2023-02-03T17:33:27.674Z
tags: 
editor: markdown
dateCreated: 2023-02-03T17:33:26.015Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [025: Using Spring Boot and Spring Batch for data processing***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/025-using-spring-boot-and-spring-batch-for-data-processing)
{.links-list}


# 使用Spring Boot和Spring Batch进行数据处理

Spring Boot 是用于构建 Java 应用程序的流行框架。它使创建可以“直接运行”的独立的、生产级的基于 Spring 的应用程序变得容易。

Spring Batch 是批处理作业的框架。它提供了许多开箱即用的功能，例如作业处理统计信息、重试失败的作业、作业链接和分区。

在这篇文章中，我们将展示如何使用 Spring Boot 和 Spring Batch 来处理文件中的数据。我们将从 CSV 文件中读取数据，对其进行处理，然后将结果写入新的 CSV 文件。

## 设置项目

我们将从设置一个新的 Spring Boot 项目开始。我们将使用 [Spring Initializr](https://start.spring.io/) 创建项目。

![Spring Initializr](initializr.png)

我们将项目命名为“data-processing”，并选择“Web”和“Batch”依赖项。我们还将使用 `Java` 版本 8。

![Spring Initializr 依赖项](initializr-deps.png)

生成项目后，我们将把它导入到我们的 IDE 中。

## 配置 Spring Batch

Spring Batch 使用“JobRepository”来存储有关作业及其执行状态的信息。 `JobRepository` 是使用数据库实现的。

我们将配置“JobRepository”以使用内存中的 H2 数据库。我们将以下依赖项添加到我们的 pom.xml 中：

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

我们还将以下配置添加到我们的 application.properties 中：

```properties
spring.batch.job.enabled=true
spring.batch.job.table-prefix=BATCH_
spring.batch.initializer.enabled=true
```

这将启用“JobRepository”并创建必要的数据库表。

## 创建工作

一个 Spring Batch 作业由一个或多个 Step 组成。 “步骤”是一个独立的、自包含的工作单元。

我们将创建一个具有单个“步骤”的作业，该作业从 CSV 文件读取数据、处理数据并将结果写入新的 CSV 文件。

我们将从创建一个“Job”bean 开始：

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

`JobBuilderFactory` 用于创建 `JobBuilder`。 `JobBuilder` 用于创建 `Job`。

`StepBuilderFactory` 用于创建 `StepBuilder`。 `StepBuilder` 用于创建 `Step`。

`Job` 由单个 `Step` 组成。 `Step` 配置为从 `ItemReader` 读取数据，使用 `ItemProcessor` 处理它，并将结果写入 `ItemWriter`。

`Step` 还配置为以 10 项为单位读取和写入数据。

## 创建一个 ItemReader

`ItemReader` 负责从数据源读取数据。

我们将创建一个“FlatFileItemReader”来从 CSV 文件中读取数据：

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

`FlatFileItemReader` 被配置为从 `input` 文件中读取数据。 `input` 文件是使用 `application.properties` 文件中的 `input` 属性配置的。

`FlatFileItemReader` 也被配置为跳过文件的第一行。这是因为文件的第一行包含列标题。

`FlatFileItemReader` 配置有 `LineMapper`。 `LineMapper` 负责将一行数据映射到一个对象。

接下来我们将创建 `LineMapper` bean：

```java
@Bean
public LineMapper<Data> lineMapper() {
    DefaultLineMapper<Data> lineMapper = new DefaultLineMapper<>();
    lineMapper.setFieldSetMapper(fieldSetMapper());
    lineMapper.setLineTokenizer(lineTokenizer());
    return lineMapper;
}
```

`DefaultLineMapper` 配置有 `LineTokenizer` 和 `FieldSetMapper`。

`LineTokenizer` 负责将一行数据标记为字段。接下来我们将创建 LineTokenizer bean：

```java
@Bean
public LineTokenizer lineTokenizer() {
    DelimitedLineTokenizer tokenizer = new DelimitedLineTokenizer();
    tokenizer.setNames(new String[]{"id", "name", "age", "city"});
    return tokenizer;
}
```

`DelimitedLineTokenizer` 使用字段的名称进行配置。字段名称必须与 CSV 文件中的列标题匹配。

`FieldSetMapper` 负责将 `FieldSet` 映射到对象。接下来我们将创建 `FieldSetMapper` bean：

```java
@Bean
public FieldSetMapper<Data> fieldSetMapper() {
    BeanWrapperFieldSetMapper<Data> fieldSetMapper = new BeanWrapperFieldSetMapper<>();
    fieldSetMapper.setTargetType(Data.class);
    return fieldSetMapper;
}
```

`BeanWrapperFieldSetMapper` 配置了目标类型。目标类型是“FieldSet”将映射到的对象的类型。在我们的例子中，目标类型是“Data”类。

## 创建一个 ItemProcessor

`ItemProcessor` 负责处理从数据源读取的数据。

我们将创建一个简单的“ItemProcessor”，将数据转换为大写：

```java
@Bean
public ItemProcessor<Data, Data> itemProcessor() {
    return data -> {
        data.setName(data.getName().toUpperCase());
        return data;
    };
}
```

## 创建一个 ItemWriter

`ItemWriter` 负责将数据写入数据接收器。

我们将创建一个 `FlatFileItemWriter` 来将数据写入 CSV 文件：

```java
@Bean
public FlatFileItemWriter<Data> itemWriter(@Value("${output}") Resource resource) {
    FlatFileItemWriter<Data> writer = new FlatFileItemWriter<>();
    writer.setResource(resource);
    writer.setLineAggregator(lineAggregator());
    return writer;
}
```

`FlatFileItemWriter` 被配置为将数据写入 `output` 文件。 `output` 文件是使用 `application.properties` 文件中的 `output` 属性配置的。

`FlatFileItemWriter` 配置有 `LineAggregator`。 `LineAggregator` 负责将数据聚合成一行。

接下来我们将创建 `LineAggregator` bean：

```java
@Bean
public LineAggregator<Data> lineAggregator() {
    DelimitedLineAggregator<Data> lineAggregator = new DelimitedLineAggregator<>();
    lineAggregator.setDelimiter(",");
    lineAggregator.setFieldExtractor(fieldExtractor());
    return lineAggregator;
}
```

`DelimitedLineAggregator` 配置了一个分隔符和一个 `FieldExtractor`。

`FieldExtractor` 负责从对象中提取字段。接下来我们将创建“FieldExtractor”bean：

```java
@Bean
public FieldExtractor<Data> fieldExtractor() {
    BeanWrapperFieldExtractor<Data> fieldExtractor = new BeanWrapperFieldExtractor<>();
    fieldExtractor.setNames(new String[]{"id", "name", "age", "city"});
    return fieldExtractor;
}
```

`BeanWrapperFieldExtractor` 使用字段的名称进行配置。字段名称必须与 CSV 文件中的列标题匹配。

## 运行作业

我们可以从我们的 IDE 运行作业，或者我们可以将应用程序打包为 JAR 文件并从命令行运行它。

我们会将应用程序打包为 JAR 文件并从命令行运行它。

我们将以下配置添加到 `pom.xml` 文件中：

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

这会将应用程序打包为 JAR 文件。

我们将运行以下命令来打包应用程序：

```
mvn package
```

我们将运行以下命令来运行应用程序：

```
java -jar target/data-processing-0.0.1-SNAPSHOT.jar
```

## 结论

在这篇文章中，我们展示了如何使用 Spring Boot 和 Spring Batch 来处理文件中的数据。我们从 CSV 文件中读取数据，对其进行处理，并将结果写入新的 CSV 文件。