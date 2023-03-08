---
title: Building a Spring Batch Application for Data Processing
description: 
published: true
date: 2023-02-18T12:07:44.797Z
tags: 
editor: markdown
dateCreated: 2023-02-18T12:07:43.346Z
---

- [데이터 처리를 위한 Spring Batch 애플리케이션 구축***Korean** document is available*](/ko/Knowledge-base/Backend/building-a-spring-batch-application-for-data-processing)
{.links-list}


# Building a Spring Batch Application for Data Processing

## Introduction

Spring Batch is a powerful processing framework for enterprise systems. It is
designed to handle high volume, high performance batch processing jobs.

In this article, we will show you how to develop a Spring Batch application to
read data from a CSV file and write it to an XML file. We will use Maven to
manage our project dependencies.


## What is Spring Batch?

Spring Batch is a lightweight, enterprise-scale framework for development of
robust batch applications. Spring Batch provides reusable functions that are
essential in processing large volumes of records, including logging/tracing,
transaction management, job processing statistics, job restart, skip, and
resource management.

Spring Batch builds upon the POJO-based development approach of the Spring
Framework, making it easy to use in any Java development environment. A key
advantage of the Spring Framework is its layer cake architecture, which
allows you to develop enterprise-class applications using a lightweight
infrastructure.

The primary goal of the Spring Batch Framework is to provide a robust
execution framework for batch applications. It also provides a foundation for
custom batch job implementations.

## System Requirements

For this example, we will use the following system requirements:

- JDK 1.8
- Maven 3.0+

## Project Structure

Our project will have the following structure:

```
├── pom.xml
├── src
│   └── main
│       └── java
│           └── com
│               └── javacodegeeks
│                   └── spring
│                       └── batch
│                           └── App.java
└── src
    └── main
        └── resources
            ├── input
            │   └── input.csv
            └── spring
                └── batch
                    └── jobs
                        └── job-config.xml
```

## Maven Dependencies

We will use the following Maven dependencies for our project:

- `spring-boot-starter-batch`: starter for using Spring Batch
- `org.springframework.batch:spring-batch-infrastructure`: contains core
functionality for the framework
- `org.codehaus.jackson:jackson-mapper-asl`: for mapping records from the
CSV file to objects
- `org.hsqldb:hsqldb`: in-memory database for storing processed records

Our `pom.xml` will look like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.javacodegeeks.spring.batch</groupId>
    <artifactId>spring-batch-example</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>jar</packaging>

    <name>spring-batch-example</name>
    <description>Spring Batch Example</description>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.3.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-batch</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.batch</groupId>
            <artifactId>spring-batch-infrastructure</artifactId>
            <version>3.0.7.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.codehaus.jackson</groupId>
            <artifactId>jackson-mapper-asl</artifactId>
            <version>1.9.13</version>
        </dependency>
        <dependency>
            <groupId>org.hsqldb</groupId>
            <artifactId>hsqldb</artifactId>
            <version>2.4.0</version>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```

## Spring Batch Job

A job in Spring Batch is an entity that encapsulates an independent,
cohesive unit of work. A job is composed of one or more steps, where each
step is an independent, sequential phase of the job. Each step can involve a
business process with potentially complex algorithms, calculations, and
business rules.

The following is a simple example of a Spring Batch job configured with two
steps. The first step is a Tasklet that reads data from a CSV file and
writes it to an XML file. The second step is a Tasklet that reads data from
the XML file and writes it to an in-memory database.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans:beans xmlns="http://www.springframework.org/schema/batch"
    xmlns:beans="http://www.springframework.org/schema/beans" 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/batch
        http://www.springframework.org/schema/batch/spring-batch.xsd">

    <beans:import resource="../config/context.xml"/>

    <beans:bean id="jobRepository" class="org.springframework.batch.core.repository.support.MapJobRepositoryFactoryBean">
        <beans:property name="transactionManager" ref="transactionManager"/>
    </beans:bean>

    <beans:bean id="transactionManager" class="org.springframework.batch.support.transaction.ResourcelessTransactionManager"/>

    <job-repository id="jobRepository" data-source="dataSource"/>

    <beans:bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource">
        <beans:property name="driverClassName" value="org.hsqldb.jdbcDriver"/>
        <beans:property name="url" value="jdbc:hsqldb:mem:testdb"/>
        <beans:property name="username" value="sa"/>
        <beans:property name="password" value=""/>
    </beans:bean>

    <beans:bean id="jobLauncher" class="org.springframework.batch.core.launch.support.SimpleJobLauncher">
        <beans:property name="jobRepository" ref="jobRepository"/>
    </beans:bean>

    <beans:bean id="csvFile" class="org.springframework.core.io.FileSystemResource" scope="step">
        <beans:constructor-arg value="#{jobParameters[csvFile]}"/>
    </beans:bean>

    <beans:bean id="xmlFile" class="org.springframework.core.io.FileSystemResource" scope="step">
        <beans:constructor-arg value="#{jobParameters[xmlFile]}"/>
    </beans:bean>

    <job id="job1" xmlns="http://www.springframework.org/schema/batch">
        <step id="step1">
            <tasklet>
                <chunk reader="csvFileItemReader" writer="xmlFileItemWriter" commit-interval="10"/>
            </tasklet>
        </step>
        <step id="step2">
            <tasklet>
                <chunk reader="xmlFileItemReader" writer="dbItemWriter" commit-interval="10"/>
            </tasklet>
        </step>
    </job>

    <beans:bean id="csvFileItemReader" class="org.springframework.batch.item.file.FlatFileItemReader">
        <beans:property name="resource" ref="csvFile"/>
        <beans:property name="lineMapper">
            <beans:bean class="org.springframework.batch.item.file.mapping.DefaultLineMapper">
                <beans:property name="lineTokenizer">
                    <beans:bean class="org.springframework.batch.item.file.transform.DelimitedLineTokenizer">
                        <beans:property name="names" value="id,name,dept,salary"/>
                    </beans:bean>
                </beans:property>
                <beans:property name="fieldSetMapper">
                    <beans:bean class="org.springframework.batch.item.file.mapping.BeanWrapperFieldSetMapper">
                        <beans:property name="targetType" value="com.javacodegeeks.spring.batch.Employee"/>
                    </beans:bean>
                </beans:property>
            </beans:bean>
        </beans:property>
    </beans:bean>

    <beans:bean id="xmlFileItemWriter" class="org.springframework.batch.item.xml.StaxEventItemWriter">
        <beans:property name="resource" ref="xmlFile"/>
        <beans:property name="marshaller" ref="employeeMarshaller"/>
        <beans:property name="rootTagName" value="employees"/>
    </beans:bean>

    <beans:bean id="employeeMarshaller" class="org.springframework.oxm.jaxb.Jaxb2Marshaller">
        <beans:property name="classesToBeBound">
            <beans:list>
                <beans:value>com.javacodegeeks.spring.batch.Employee</beans:value>
            </beans:list>
        </beans:property>
    </beans:bean>

    <beans:bean id="dbItemWriter" class="org.springframework.batch.item.database.JdbcBatchItemWriter">
        <beans:property name="dataSource" ref="dataSource"/>
        <beans:property name="sql" value="INSERT INTO EMPLOYEE (ID, NAME, DEPT, SALARY) VALUES (:id, :name, :dept, :salary)"/>
        <beans:property name="itemSqlParameterSourceProvider">
            <beans:bean class="org.springframework.batch.item.database.BeanPropertyItemSqlParameterSourceProvider"/>
        </beans:property>
    </beans:bean>

    <beans:bean id="xmlFileItemReader" class="org.springframework.batch.item.xml.StaxEventItemReader">
        <beans:property name="resource" ref="xmlFile"/>
        <beans:property name="fragmentRootElementName" value="employee"/>
        <beans:property name="unmarshaller" ref="employeeMarshaller"/>
    </beans:bean>

</beans:beans>
```

## Step 1: Reading From a CSV File

In the first step of our job, we will read data from a CSV file and write it
to an XML file. We will use a FlatFileItemReader to read data from the CSV
file.

The FlatFileItemReader reads data from a flat file and maps each line to an
Object. In our example, we will map each line to an Employee object.

We will use a DelimitedLineTokenizer to tokenize each line in the CSV file.
The DelimitedLineTokenizer is a subclass of the abstract
LineTokenizer class. It tokenizes a line by splitting it into fields.

We will use a BeanWrapperFieldSetMapper to map the tokens to Employee
object properties. The BeanWrapperFieldSetMapper is a subclass of the
abstract FieldSetMapper class. It maps the data in a FieldSet to
properties of a JavaBean.

## Step 2: Writing to an XML File

In the second step of our job, we will read data from the XML file and write
it to an in-memory database. We will use a StaxEventItemWriter to write
data to the XML file.

The StaxEventItemWriter is a subclass of the abstract
AbstractStaxEventItemWriter class. It writes items to an XML file using
StAX (Streaming API for XML).

We will use a Jaxb2Marshaller to marshal the Employee objects to XML. The
Jaxb2Marshaller is a subclass of the abstract
Marshaller class. It marshals Java objects to and from XML.

## Step 3: Writing to a Database

In the third step of our job, we will read data from the XML file and write
it to an in-memory database. We will use a JdbcBatchItemWriter to write
data to the database.

The JdbcBatchItemWriter is a subclass of the abstract
JdbcItemWriter class. It writes data to a database using JDBC.

We will use a BeanPropertyItemSqlParameterSourceProvider to provide
SQL parameters from the Employee objects. The
BeanPropertyItemSqlParameterSourceProvider is a subclass of the
abstract ItemSqlParameterSourceProvider class. It provides
SQL parameters from the properties of a JavaBean.

##Configuring the Job

We will configure our job in the `job-config.xml` file. The
`job-config.xml` file contains the configuration for our job.

## Running the Job

We will run our job using the following command:

```
java -jar target/spring-batch-example-0.0.1-SNAPSHOT.jar --job.name=job1 --csvFile=./input/input.csv --xmlFile=./output/output.xml
```

## Conclusion

In this article, we showed you how to develop a Spring Batch application to
read data from a CSV file and write it to an XML file. We also showed you how
to read data from the XML file and write it to an in-memory database.