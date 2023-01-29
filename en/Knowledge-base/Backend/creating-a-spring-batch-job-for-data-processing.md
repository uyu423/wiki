---
title: Creating a Spring Batch job for data processing
description: 
published: true
date: 2023-01-29T20:26:56.970Z
tags: 
editor: markdown
dateCreated: 2023-01-29T20:26:56.970Z
---

- [데이터 처리를 위한 Spring Batch 작업 만들기***Korean** version of this document is available*](/ko/Knowledge-base/Backend/creating-a-spring-batch-job-for-data-processing)
{.links-list}

# Creating a Spring Batch job for data processing

In this blog post, we'll take a look at how to create a Spring Batch job for data processing. We'll go through the process of setting up a job, configuring it, and running it.

## Setting up a job

The first thing we need to do is set up a job. We can do this using the Spring Batch Job Builder API.

First, we need to create a JobBuilderFactory. We can do this by passing in a JobRepository and a PlatformTransactionManager:

```java
JobBuilderFactory jobBuilderFactory = new JobBuilderFactory(jobRepository, transactionManager);
```

Next, we need to create a JobBuilder. We can do this by passing in a JobBuilderFactory and a job name:

```java
JobBuilder jobBuilder = jobBuilderFactory.getJobBuilder("myJob");
```

Now we can use the JobBuilder to create our Job. We do this by adding steps to the Job. A Step is an independent, self-contained piece of work that can be executed by the Job.

In this example, we'll create a Step that reads data from a CSV file and writes it to a database. We can do this using the FlatFileItemReader and JdbcBatchItemWriter.

First, we need to create a FlatFileItemReader. We can do this by passing in a Resource and a lineMapper:

```java
FlatFileItemReader<Person> reader = new FlatFileItemReader<>();
reader.setResource(new ClassPathResource("people.csv"));
reader.setLineMapper(new DefaultLineMapper<Person>() {{
    setLineTokenizer(new DelimitedLineTokenizer() {{
        setNames(new String[] { "firstName", "lastName" });
    }});
    setFieldSetMapper(new BeanWrapperFieldSetMapper<Person>() {{
        setTargetType(Person.class);
    }});
}});
```

Next, we need to create a JdbcBatchItemWriter. We can do this by passing in a DataSource and a sql:

```java
JdbcBatchItemWriter<Person> writer = new JdbcBatchItemWriter<>();
writer.setDataSource(dataSource);
writer.setSql("INSERT INTO people (first_name, last_name) VALUES (:firstName, :lastName)");
writer.setItemSqlParameterSourceProvider(new BeanPropertyItemSqlParameterSourceProvider<>());
writer.afterPropertiesSet();
```

Now we can create our Step. We do this by passing in a StepBuilderFactory, a reader, and a writer:

```java
Step step = stepBuilderFactory.get("myStep")
        .<Person, Person>chunk(10)
        .reader(reader)
        .writer(writer)
        .build();
```

Finally, we can add our Step to the Job and build it:

```java
Job job = jobBuilder.start(step).build();
```

## Configuring a job

Now that we have our job set up, we need to configure it. We can do this using the JobLauncher and JobParametersBuilder.

First, we need to create a JobLauncher. We can do this by passing in a JobRepository:

```java
JobLauncher jobLauncher = new SimpleJobLauncher();
jobLauncher.setJobRepository(jobRepository);
```

Next, we need to create a JobParametersBuilder. We can do this by passing in a JobParameters:

```java
JobParametersBuilder jobParametersBuilder = new JobParametersBuilder();
jobParametersBuilder.addLong("runId", 1L);
```

Now we can launch our Job by passing in the Job and the JobParameters:

```java
jobLauncher.run(job, jobParametersBuilder.toJobParameters());
```

## Running a job

Now that our job is set up and configured, we can run it. We can do this using the JobLauncher and JobParametersBuilder.

First, we need to create a JobLauncher. We can do this by passing in a JobRepository:

```java
JobLauncher jobLauncher = new SimpleJobLauncher();
jobLauncher.setJobRepository(jobRepository);
```

Next, we need to create a JobParametersBuilder. We can do this by passing in a JobParameters:

```java
JobParametersBuilder jobParametersBuilder = new JobParametersBuilder();
jobParametersBuilder.addLong("runId", 1L);
```

Now we can launch our Job by passing in the Job and the JobParameters:

```java
jobLauncher.run(job, jobParametersBuilder.toJobParameters());
```