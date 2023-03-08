---
title: 025: 데이터 처리를 위해 Spring Boot와 Spring Batch 사용하기
description: 
published: true
date: 2023-02-03T17:33:27.655Z
tags: 
editor: markdown
dateCreated: 2023-02-03T17:33:26.008Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [025: Using Spring Boot and Spring Batch for data processing***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/025-using-spring-boot-and-spring-batch-for-data-processing)
{.links-list}


# 데이터 처리를 위해 Spring Boot와 Spring Batch 사용

Spring Boot는 Java 애플리케이션을 구축하는 데 널리 사용되는 프레임워크입니다. "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다.

Spring Batch는 일괄 처리 작업을 위한 프레임워크입니다. 작업 처리 통계, 실패한 작업 재시도, 작업 체인 및 파티셔닝과 같은 많은 기능을 즉시 제공합니다.

이 게시물에서는 Spring Boot 및 Spring Batch를 사용하여 파일의 데이터를 처리하는 방법을 보여줍니다. CSV 파일에서 데이터를 읽고 처리한 다음 결과를 새 CSV 파일에 씁니다.

## 프로젝트 설정

새로운 Spring Boot 프로젝트를 설정하는 것으로 시작하겠습니다. [Spring Initializr](https://start.spring.io/)를 사용하여 프로젝트를 생성하겠습니다.

![스프링 이니셜라이저](initializr.png)

프로젝트 이름을 'data-processing'으로 지정하고 'Web' 및 'Batch' 종속 항목을 선택합니다. 또한 `Java` 버전 8을 사용합니다.

![Spring Initializr 의존성](initializr-deps.png)

프로젝트가 생성되면 IDE로 가져옵니다.

## 스프링 배치 설정

Spring Batch는 'JobRepository'를 사용하여 작업 및 실행 상태에 대한 정보를 저장합니다. `JobRepository`는 데이터베이스를 사용하여 구현됩니다.

메모리 내 H2 데이터베이스를 사용하도록 `JobRepository`를 구성합니다. `pom.xml`에 다음 종속성을 추가합니다.

```xml
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

또한 `application.properties`에 다음 구성을 추가합니다.

```properties
spring.batch.job.enabled=true
spring.batch.job.table-prefix=BATCH_
spring.batch.initializer.enabled=true
```

이렇게 하면 `JobRepository`가 활성화되고 필요한 데이터베이스 테이블이 생성됩니다.

## 직업 만들기

Spring Batch 작업은 하나 이상의 `Step`으로 구성됩니다. '단계'는 독립적이고 독립적인 작업 단위입니다.

CSV 파일에서 데이터를 읽고 처리하고 결과를 새 CSV 파일에 쓰는 단일 `단계`로 작업을 생성합니다.

먼저 `Job` bean을 생성합니다.

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

`JobBuilderFactory`는 `JobBuilder`를 생성하는 데 사용됩니다. `JobBuilder`는 `Job`을 생성하는 데 사용됩니다.

`StepBuilderFactory`는 `StepBuilder`를 생성하는 데 사용됩니다. `StepBuilder`는 `Step`을 생성하는 데 사용됩니다.

`Job`은 단일 `Step`으로 구성됩니다. `Step`은 `ItemReader`에서 데이터를 읽고 `ItemProcessor`를 사용하여 데이터를 처리하고 `ItemWriter`에 결과를 쓰도록 구성됩니다.

'Step'도 10개 항목 단위로 데이터를 읽고 쓰도록 구성되어 있습니다.

## 아이템 리더 만들기

`ItemReader`는 데이터 소스에서 데이터 읽기를 담당합니다.

CSV 파일에서 데이터를 읽기 위해 `FlatFileItemReader`를 생성합니다.

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

`FlatFileItemReader`는 `input` 파일에서 데이터를 읽도록 구성됩니다. `input` 파일은 `application.properties` 파일의 `input` 속성을 사용하여 구성됩니다.

`FlatFileItemReader`도 파일의 첫 번째 줄을 건너뛰도록 구성됩니다. 이는 파일의 첫 번째 줄에 열 머리글이 포함되어 있기 때문입니다.

`FlatFileItemReader`는 `LineMapper`로 구성됩니다. `LineMapper`는 데이터 라인을 개체에 매핑하는 역할을 합니다.

다음으로 `LineMapper` 빈을 생성합니다:

```java
@Bean
public LineMapper<Data> lineMapper() {
    DefaultLineMapper<Data> lineMapper = new DefaultLineMapper<>();
    lineMapper.setFieldSetMapper(fieldSetMapper());
    lineMapper.setLineTokenizer(lineTokenizer());
    return lineMapper;
}
```

`DefaultLineMapper`는 `LineTokenizer` 및 `FieldSetMapper`로 구성됩니다.

`LineTokenizer`는 데이터 라인을 필드로 토큰화하는 역할을 합니다. 다음으로 `LineTokenizer` 빈을 생성합니다:

```java
@Bean
public LineTokenizer lineTokenizer() {
    DelimitedLineTokenizer tokenizer = new DelimitedLineTokenizer();
    tokenizer.setNames(new String[]{"id", "name", "age", "city"});
    return tokenizer;
}
```

`DelimitedLineTokenizer`는 필드 이름으로 구성됩니다. 필드 이름은 CSV 파일의 열 헤더와 일치해야 합니다.

'FieldSetMapper'는 'FieldSet'을 개체에 매핑하는 역할을 합니다. 다음으로 `FieldSetMapper` 빈을 생성합니다:

```java
@Bean
public FieldSetMapper<Data> fieldSetMapper() {
    BeanWrapperFieldSetMapper<Data> fieldSetMapper = new BeanWrapperFieldSetMapper<>();
    fieldSetMapper.setTargetType(Data.class);
    return fieldSetMapper;
}
```

`BeanWrapperFieldSetMapper`는 대상 유형으로 구성됩니다. 대상 유형은 'FieldSet'이 매핑될 개체의 유형입니다. 우리의 경우 대상 유형은 `Data` 클래스입니다.

## 아이템 프로세서 만들기

`ItemProcessor`는 데이터 소스에서 읽은 데이터를 처리하는 역할을 합니다.

데이터를 대문자로 변환하는 간단한 `ItemProcessor`를 생성합니다.

```java
@Bean
public ItemProcessor<Data, Data> itemProcessor() {
    return data -> {
        data.setName(data.getName().toUpperCase());
        return data;
    };
}
```

## ItemWriter 만들기

'ItemWriter'는 데이터 싱크에 데이터 쓰기를 담당합니다.

데이터를 CSV 파일에 쓰기 위해 `FlatFileItemWriter`를 생성합니다.

```java
@Bean
public FlatFileItemWriter<Data> itemWriter(@Value("${output}") Resource resource) {
    FlatFileItemWriter<Data> writer = new FlatFileItemWriter<>();
    writer.setResource(resource);
    writer.setLineAggregator(lineAggregator());
    return writer;
}
```

`FlatFileItemWriter`는 `output` 파일에 데이터를 쓰도록 구성됩니다. `output` 파일은 `application.properties` 파일의 `output` 속성을 사용하여 구성됩니다.

`FlatFileItemWriter`는 `LineAggregator`로 구성됩니다. `LineAggregator`는 데이터를 라인으로 집계하는 역할을 합니다.

다음으로 `LineAggregator` 빈을 생성합니다:

```java
@Bean
public LineAggregator<Data> lineAggregator() {
    DelimitedLineAggregator<Data> lineAggregator = new DelimitedLineAggregator<>();
    lineAggregator.setDelimiter(",");
    lineAggregator.setFieldExtractor(fieldExtractor());
    return lineAggregator;
}
```

`DelimitedLineAggregator`는 구분 기호와 `FieldExtractor`로 구성됩니다.

'FieldExtractor'는 개체에서 필드를 추출하는 역할을 합니다. 다음으로 `FieldExtractor` 빈을 생성합니다:

```java
@Bean
public FieldExtractor<Data> fieldExtractor() {
    BeanWrapperFieldExtractor<Data> fieldExtractor = new BeanWrapperFieldExtractor<>();
    fieldExtractor.setNames(new String[]{"id", "name", "age", "city"});
    return fieldExtractor;
}
```

`BeanWrapperFieldExtractor`는 필드 이름으로 구성됩니다. 필드 이름은 CSV 파일의 열 헤더와 일치해야 합니다.

## 작업 실행

IDE에서 작업을 실행하거나 응용 프로그램을 JAR 파일로 패키징하고 명령줄에서 실행할 수 있습니다.

애플리케이션을 JAR 파일로 패키징하고 명령줄에서 실행합니다.

`pom.xml` 파일에 다음 구성을 추가합니다.

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

그러면 애플리케이션이 JAR 파일로 패키징됩니다.

다음 명령을 실행하여 애플리케이션을 패키징합니다.

```
mvn package
```

다음 명령을 실행하여 애플리케이션을 실행합니다.

```
java -jar target/data-processing-0.0.1-SNAPSHOT.jar
```

## 결론

이 게시물에서는 Spring Boot 및 Spring Batch를 사용하여 파일의 데이터를 처리하는 방법을 보여 주었습니다. CSV 파일에서 데이터를 읽고 처리한 다음 결과를 새 CSV 파일에 기록했습니다.