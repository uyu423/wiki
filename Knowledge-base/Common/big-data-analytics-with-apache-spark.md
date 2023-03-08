---
title: Apache Spark를 사용한 빅 데이터 분석
description: 
published: true
date: 2023-02-05T13:18:31.542Z
tags: 
editor: markdown
dateCreated: 2023-02-05T13:18:29.868Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Big Data Analytics with Apache Spark***English** document is available*](/en/Knowledge-base/Common/big-data-analytics-with-apache-spark)
{.links-list}


# Apache Spark를 사용한 빅데이터 분석

빅데이터의 인기가 높아지면서 빅데이터 분석에 대한 수요도 증가하고 있습니다. Apache Spark는 가장 널리 사용되는 빅 데이터 처리 프레임워크 중 하나이며 빅 데이터 분석에 널리 사용됩니다.

Spark는 강력한 SQL 및 스트리밍 기능을 갖춘 빠른 인메모리 데이터 처리 엔진입니다. 배치 및 실시간 데이터 처리를 모두 처리할 수 있습니다. Spark는 사용하기 쉽고 데이터 처리, 기계 학습 및 그래프 처리를 위한 풍부한 라이브러리 세트를 가지고 있습니다.

이 기사에서는 Apache Spark를 사용하여 빅 데이터 분석을 수행하는 방법에 대해 설명합니다. 다음 주제를 다룰 것입니다.

- Spark 개발 환경 설정
- Spark에서 데이터 로드 및 처리
- 스파크 SQL
- 스파크 스트리밍
- Spark를 사용한 기계 학습
- Spark로 그래프 처리

## Spark 개발 환경 설정

Spark는 독립 실행형 서버 또는 시스템 클러스터에 설치할 수 있습니다. 클라우드에서도 실행할 수 있습니다. 이 문서에서는 독립 실행형 Spark 설치가 있다고 가정합니다.

### 전제 조건

시작하기 전에 다음이 필요합니다.

- 최소 4GB의 RAM과 처리하려는 데이터를 저장하기에 충분한 디스크 공간이 있는 시스템.
- 자바 8 이상.
- 아파치 스파크 2.4 이상.

### 스파크 설치하기

 1. [Spark 웹사이트](https://spark.apache.org/)에서 최신 버전의 Apache Spark를 다운로드합니다.
 2. 다운로드한 파일의 압축을 풉니다. 그러면 `spark-2.4.5-bin-hadoop2.7`이라는 디렉토리가 생성됩니다.
 3. `spark-2.4.5-bin-hadoop2.7` 디렉터리를 Spark를 설치하려는 위치로 이동합니다.
 4. `SPARK_HOME` 환경 변수를 `spark-2.4.5-bin-hadoop2.7` 디렉토리로 설정합니다.
 5. `$SPARK_HOME/bin` 디렉터리를 `PATH` 환경 변수에 추가합니다.

이제 `spark-shell` 명령을 실행하여 Spark 셸을 시작할 수 있습니다.

## Spark에서 데이터 로드 및 처리

Spark는 HDFS, S3 및 로컬 파일을 비롯한 다양한 소스에서 데이터를 로드할 수 있습니다. 이 섹션에서는 로컬 파일에서 데이터를 로드하고 Spark에서 처리하는 방법에 대해 설명합니다.

먼저 다음 내용으로 `sample.txt`라는 텍스트 파일을 만듭니다.

```
This is a sample text file.
```

이제 `spark.read.text()` 메서드를 사용하여 이 파일을 Spark에 로드할 수 있습니다.

```scala
val textFile = spark.read.text("sample.txt")
```

`textFile` 변수는 `sample.txt` 파일의 내용을 포함하는 `Dataset[String]`입니다. 이제 이 데이터 세트에서 필터링, 변환 및 집계와 같은 다양한 작업을 수행할 수 있습니다.

예를 들어 `filter()` 메서드를 사용하여 `sample`이라는 단어가 포함되지 않은 행을 필터링할 수 있습니다.

```scala
val filteredTextFile = textFile.filter(line => line.contains("sample"))
```

`map()` 메서드를 사용하여 데이터셋을 변환할 수도 있습니다.

```scala
val mappedTextFile = textFile.map(line => line.toUpperCase())
```

마지막으로 `groupBy()` 메서드를 사용하여 라인 길이별로 데이터셋을 그룹화할 수 있습니다.

```scala
val groupedTextFile = textFile.groupBy(line => line.length)
```

## 스파크 SQL

Spark SQL은 구조화된 데이터로 작업할 수 있는 Spark 모듈입니다. HDFS, S3 및 로컬 파일과 같은 다양한 소스에서 데이터를 로드하는 데 사용할 수 있는 DataFrame API를 제공합니다.

이 섹션에서는 Spark SQL을 사용하여 로컬 파일에서 데이터를 로드하고 처리하는 방법에 대해 설명합니다.

먼저 다음 내용으로 `people.txt`라는 텍스트 파일을 만듭니다.

```
id,name,age
1,john,26
2,mary,29
3,jane,21
4,bob,27
```

이제 `spark.read.csv()` 메서드를 사용하여 이 파일을 Spark DataFrame으로 로드할 수 있습니다.

```scala
val peopleDF = spark.read.csv("people.txt")
```

`peopleDF` DataFrame에는 다음과 같은 스키마가 있습니다.

```
root
 |-- id: string (nullable = true)
 |-- name: string (nullable = true)
 |-- age: string (nullable = true)
```

이제 이 DataFrame을 임시 보기로 등록하여 SQL 쿼리를 실행할 수 있습니다.

```scala
peopleDF.createOrReplaceTempView("people")
```

이제 `사람` 보기에서 SQL 쿼리를 실행할 수 있습니다. 예를 들어 뷰를 쿼리하여 25세 이상인 모든 사람의 이름을 찾을 수 있습니다.

```scala
spark.sql("SELECT name FROM people WHERE age > 25").show()
```

다음을 출력해야 합니다.

```
+-----+
| name|
+-----+
| john|
| mary|
|  bob|
+-----+
```

## 스파크 스트리밍

Spark Streaming은 실시간 데이터 스트림을 처리할 수 있는 Spark 모듈입니다. Kafka, Flume 및 Twitter와 같은 소스에서 라이브 데이터 스트림을 수신할 수 있습니다.

이 섹션에서는 Spark Streaming을 사용하여 Twitter에서 라이브 데이터 스트림을 처리하는 방법에 대해 설명합니다.

먼저 Twitter API 애플리케이션을 만들어야 합니다. [Twitter 개발자 설명서](https://developer.twitter.com/en/docs/basics/apps/overview)의 지침에 따라 이를 수행할 수 있습니다.

Twitter API 응용 프로그램을 만든 후에는 Twitter API 자격 증명으로 `twitter.txt`라는 파일을 만들어야 합니다. 파일은 다음 형식이어야 합니다.

```
consumerKey = <your consumer key>
consumerSecret = <your consumer secret>
accessToken = <your access token>
accessTokenSecret = <your access token secret>
```

이제 다음 명령을 실행하여 Spark Streaming 셸을 시작할 수 있습니다.

```
spark-shell --packages org.apache.spark:spark-streaming-twitter_2.11:2.4.5
```

그러면 `spark-streaming-twitter_2.11` 패키지로 Spark 셸이 시작됩니다.

이제 Spark Streaming 컨텍스트를 만들고 체크포인트 디렉터리를 설정할 수 있습니다.

```scala
import org.apache.spark._
import org.apache.spark.streaming._

val ssc = new StreamingContext(sc, Seconds(10))
ssc.checkpoint("checkpoint")
```

이제 이전에 만든 `twitter.txt` 파일을 사용하여 Twitter 스트림을 만들 수 있습니다.

```scala
import org.apache.spark.streaming.twitter._

val twitterStream = TwitterUtils.createStream(ssc, None, Seq(args(0)))
```

`twitterStream`은 라이브 Twitter 스트림을 포함하는 `DStream[Status]`입니다. 이제 이 스트림에서 변환, 필터링 및 집계와 같은 다양한 작업을 수행할 수 있습니다.

예를 들어 `map()` 메서드를 사용하여 스트림을 변환할 수 있습니다.

```scala
val textStream = twitterStream.map(status => status.getText())
```

이제 `foreachRDD()` 메서드를 사용하여 스트림을 처리할 수 있습니다.

```scala
textStream.foreachRDD { (rdd, time) =>
  val count = rdd.count()
  println(s"Received ${count} tweets at time ${time}")
}
```

마지막으로 스트리밍 프로세스를 시작할 수 있습니다.

```scala
ssc.start()
```

## 스파크를 사용한 기계 학습

Spark MLlib는 다양한 기계 학습 알고리즘을 제공하는 Spark의 모듈입니다. 이 섹션에서는 Spark MLlib를 사용하여 기계 학습 모델을 교육하는 방법에 대해 설명합니다.

먼저 다음 내용으로 `training.txt`라는 텍스트 파일을 만듭니다.

```
id,features,label
1,[1.0,0.0,0.0],0.0
2,[0.0,1.0,0.0],1.0
3,[0.0,0.0,1.0],2.0
```

이제 `spark.read.csv()` 메서드를 사용하여 이 파일을 Spark DataFrame으로 로드할 수 있습니다.

```scala
val trainingDF = spark.read.csv("training.txt")
```

`trainingDF` DataFrame에는 다음과 같은 스키마가 있습니다.

```
root
 |-- id: string (nullable = true)
 |-- features: vector (nullable = true)
 |-- label: double (nullable = true)
```

이제 `LogisticRegression` 객체를 생성하고 매개변수를 설정할 수 있습니다.

```scala
import org.apache.spark.ml.classification.LogisticRegression

val lr = new LogisticRegression()
  .setMaxIter(10)
  .setRegParam(0.01)
```

이제 `fit()` 메서드를 사용하여 모델을 훈련할 수 있습니다.

```scala
val model = lr.fit(trainingDF)
```

이제 훈련된 모델을 파일에 저장할 수 있습니다.

```scala
model.write.overwrite().save("model")
```

## Spark로 그래프 처리

Spark GraphX는 다양한 그래프 처리 알고리즘을 제공하는 Spark의 모듈입니다. 이 섹션에서는 Spark GraphX를 사용하여 그래프를 처리하는 방법에 대해 설명합니다.

먼저 다음 내용으로 `edges.txt`라는 텍스트 파일을 만듭니다.

```
src,dst,weight
1,2,1.0
2,3,2.0
3,4,3.0
4,1,4.0
```

이제 `spark.read.csv()` 메서드를 사용하여 이 파일을 Spark DataFrame으로 로드할 수 있습니다.

```scala
val edgesDF = spark.read.csv("edges.txt")
```

`edgesDF` DataFrame에는 다음과 같은 스키마가 있습니다.

```
root
 |-- src: string (nullable = true)
 |-- dst: string (nullable = true)
 |-- weight: double (nullable = true)
```

이제 `edgesDF` DataFrame에서 `Graph` 개체를 만들 수 있습니다.

```scala
import org.apache.spark.graphx._

val graph = Graph.fromEdges(edgesDF, "weight")
```

`graph`는 `edgesDF` DataFrame의 가장자리를 포함하는 `Graph[Double, Double]`입니다. 이제 이 그래프에서 변환, 필터링 및 집계와 같은 다양한 작업을 수행할 수 있습니다.

예를 들어 `mapEdges()` 메서드를 사용하여 가장자리를 변환할 수 있습니다.

```scala
val transformedGraph = graph.mapEdges(e => e.attr * 2)
```

정점을 변환하기 위해 `mapVertices()` 메서드를 사용할 수도 있습니다.

```scala
val transformedGraph = graph.mapVertices { (id, attr) =>
  attr * 2
}
```

마지막으로 `aggregateMessages()` 메서드를 사용하여 에지를 집계할 수 있습니다.

```scala
val aggregatedGraph = graph.aggregateMessages[Double](
  ctx => ctx.sendToDst(ctx.srcAttr),
  (a, b) => a + b
)
```

## 결론

이 기사에서는 Apache Spark를 사용하여 빅 데이터 분석을 수행하는 방법에 대해 설명했습니다. 우리는 다음 주제를 다루었습니다.

- Spark 개발 환경 설정
- Spark에서 데이터 로드 및 처리
- 스파크 SQL
- 스파크 스트리밍
- Spark를 사용한 기계 학습
- Spark로 그래프 처리

## 참조

- [Spark 문서](https://spark.apache.org/docs/latest/)
- [Spark SQL 문서](https://spark.apache.org/docs/latest/sql-programming-guide.html)
- [Spark 스트리밍 문서](https://spark.apache.org/docs/latest/streaming-programming-guide.html)
- [Spark MLlib 문서](https://spark.apache.org/docs/latest/ml-guide.html)
- [Spark GraphX 문서](https://spark.apache.org/docs/latest/graphx-programming-guide.html)