---
title: 051: Using Spring Boot with Spring XD
description: 
published: true
date: 2023-02-04T17:32:34.896Z
tags: 
editor: markdown
dateCreated: 2023-02-04T17:32:29.569Z
---

- [051: Uso de Spring Boot con Spring XD***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/051-using-spring-boot-with-spring-xd)
{.links-list}
- [051：将 Spring Boot 与 Spring XD 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/051-using-spring-boot-with-spring-xd)
{.links-list}
- [051: Spring XD와 함께 Spring Boot 사용하기***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/051-using-spring-boot-with-spring-xd)
{.links-list}


# Using Spring Boot with Spring XD

Spring Boot is a great way to get up and running with Spring applications quickly. It provides many features out of the box, including auto-configuration, embedded servers, and starter dependencies.

Spring XD is a tool for building data pipelines. It can ingest data from many sources, process it in various ways, and output it to many sinks.

In this post, we'll learn how to use Spring Boot with Spring XD. We'll start with a simple example that ingests data from a file and outputs it to a database. Then we'll explore some of the more advanced features of Spring XD.

## Prerequisites

Before we get started, we need to install a few things:

* [Java 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [Maven 3](https://maven.apache.org/download.cgi)
* [Spring Boot CLI](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#getting-started-installing-the-cli)
* [Spring XD](https://spring.io/projects/spring-xd)

## Hello World

Let's start with a simple example. We'll create a file called `data.txt` with the following contents:

```
Hello, world!
```

Next, we'll create a Spring XD stream that ingests data from this file and outputs it to the console. We can do this with the following command:

```
xd:>stream create --name hello --definition "file --dir=./ --pattern=data.txt | log" --deploy
```

This stream has two components: a file source and a log sink. The file source is configured to read from the `./` directory (the current directory) and look for files with the pattern `data.txt`. The log sink simply outputs the data to the console.

We can see the stream running with the following command:

```
xd:>stream list
```

And we can see the output of the stream with the following command:

```
xd:>log hello
```

## Database Output

In the previous example, we outputted the data to the console. But in many cases, we'll want to output the data to a database. Spring XD makes this easy with the `jdbc` sink.

First, we need to create a database. We'll use [H2](http://www.h2database.com/html/main.html), which is a lightweight database that can run in memory. We can create a database with the following command:

```
xd:>jdbc create --name mydb --url jdbc:h2:mem:mydb
```

This will create a database called `mydb` in memory.

Next, we need to create a table in this database. We'll use the following SQL:

```sql
CREATE TABLE messages (
  id IDENTITY,
  message VARCHAR(255)
);
```

We can execute this SQL with the following command:

```
xd:>jdbc execute --name mydb --sql "CREATE TABLE messages (id IDENTITY, message VARCHAR(255))"
```

Now we have a database and a table, we can create a stream that outputs the data to this table. We can do this with the following command:

```
xd:>stream create --name db --definition "file --dir=./ --pattern=data.txt | jdbc --name=mydb --tableName=messages --columns=message" --deploy
```

This stream is similar to the previous one, but it has a `jdbc` sink instead of a `log` sink. The `jdbc` sink is configured to write to the `messages` table in the `mydb` database. The `columns` property specifies which columns in the table should be populated with data from the stream.

We can verify that the data has been inserted into the database with the following SQL:

```sql
SELECT * FROM messages;
```

## Processor

In the previous examples, we've seen how to ingest data from a file and output it to either the console or a database. But in many cases, we'll want to process the data in some way before outputting it. Spring XD makes this easy with processors.

Processors can transform the data in any way we want. In this example, we'll create a processor that converts the data to uppercase. We can do this with the following command:

```
xd:>processor create --name uppercase --definition "transform --expression=payload.toUpperCase()" --deploy
```

This processor has a single `transform` module. The `transform` module takes an expression that is evaluated for each piece of data in the stream. In this case, the expression is `payload.toUpperCase()`, which converts the data to uppercase.

Now we can modify our `db` stream to use this processor:

```
xd:>stream create --name db --definition "file --dir=./ --pattern=data.txt | uppercase | jdbc --name=mydb --tableName=messages --columns=message" --deploy
```

We can verify that the data has been inserted into the database with the following SQL:

```sql
SELECT * FROM messages;
```

## Summary

In this post, we've learned how to use Spring Boot with Spring XD. We've seen how to create a stream that ingests data from a file and outputs it to either the console or a database. And we've seen how to use a processor to transform the data before it is outputted.