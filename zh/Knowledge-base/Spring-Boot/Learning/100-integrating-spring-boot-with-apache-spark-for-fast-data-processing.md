---
title: 100：将 Spring Boot 与 Apache Spark 集成以实现快速数据处理
description: 
published: true
date: 2023-02-06T04:32:30.351Z
tags: 
editor: markdown
dateCreated: 2023-02-06T04:32:28.730Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [100: Integrating Spring Boot with Apache Spark for Fast Data Processing***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/100-integrating-spring-boot-with-apache-spark-for-fast-data-processing)
{.links-list}


## 100：将 Spring Boot 与 Apache Spark 集成以实现快速数据处理

在本文中，我们将展示如何将 Spring Boot 与 Apache Spark 集成以实现快速数据处理。

Spark 是处理大型数据集的强大工具，在大数据社区中越来越受欢迎。 Spring Boot 是一种流行的 Java 框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序。

集成这两个框架可以提供一种快速、高效的数据处理方式。在这篇文章中，我们将向您展示如何做到这一点。

我们将从创建一个 Spring Boot 应用程序开始。然后，我们将为 Spark 添加必要的依赖项。最后，我们将编写一个简单的 Spark 作业并在我们的本地开发环境中运行它。

### 创建一个 Spring Boot 应用程序

首先，我们将创建一个 Spring Boot 应用程序。我们将使用 Spring Initializr 来生成我们的项目。

转到 Spring Initializr 网站 (https://start.spring.io/)。

使用以下值填写表单：

* 组：com.example
* 神器：demo
* 名称：演示
* 描述：Spring Boot 和 Apache Spark 的演示项目
* 包名：com.example.demo
* 类型：Maven 项目
* 包装：罐装
* Java 版本：8
*选择“Spring Boot Starters”部分下的“Web”复选框

单击“生成项目”。

您现在应该有一个包含项目结构的 zip 文件。解压缩文件并在您喜欢的 IDE 中打开它。

### 添加必要的依赖

接下来，我们将为 Spark 添加必要的依赖项。我们需要以下依赖项：

*火花核心
*火花-SQL

我们可以通过将以下内容添加到我们的 pom.xml 文件来将这些依赖项添加到我们的项目中：

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

### 编写 Spark 作业

现在我们已经设置了项目，我们可以编写一个简单的 Spark 作业。我们将从创建一个名为 SparkJob.java 的新 Java 类开始。

在我们的 SparkJob 类中，我们将首先创建一个 SparkSession。 SparkSession 是 Spark SQL 的入口点。它允许我们从各种数据源读取数据并执行 SQL 查询。

接下来，我们将读入一个数据集。我们将使用航空公司航班数据的示例数据集。数据集采用 CSV 格式，可在此处获取：http://stat-computing.org/dataexpo/2009/2008.csv.bz2。

一旦我们有了数据集，我们将把它注册为一个表。这将允许我们对其运行 SQL 查询。

最后，我们将运行一个简单的 SQL 查询来计算每家航空公司的航班数量。

我们的 SparkJob 类的完整代码如下所示：

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

### 运行 Spark 作业

现在我们已经编写了 Spark 作业，我们可以在本地开发环境中运行它。

为此，我们需要先启动一个本地 Spark 实例。我们可以使用以下命令执行此操作：

```
$SPARK_HOME/bin/spark-shell --master local[*]
```

一旦 Spark 启动并运行，我们就可以提交我们的 Spark 作业。我们可以使用以下命令执行此操作：

```
spark-submit --class com.example.demo.SparkJob --master local[*] target/demo-0.0.1-SNAPSHOT.jar
```

如果一切顺利，您应该会看到类似于以下内容的输出：

```
American: 12359
Continental: 7261
Delta: 20216
United: 13721
US Airways: 10429
```

就是这样！您现在已成功将 Spring Boot 与 Apache Spark 集成。