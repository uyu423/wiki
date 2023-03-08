---
title: 094：将 Spring Boot 与 Apache Storm 集成以进行实时处理
description: 
published: true
date: 2023-02-05T23:33:00.044Z
tags: 
editor: markdown
dateCreated: 2023-02-05T23:32:54.576Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [094: Integrating Spring Boot with Apache Storm for Real-Time Processing***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/094-integrating-spring-boot-with-apache-storm-for-real-time-processing)
{.links-list}


# 094：将 Spring Boot 与 Apache Storm 集成以进行实时处理

在本文中，我们将展示如何将 Spring Boot 与 Apache Storm 集成以进行实时处理。

Storm 是一种分布式流处理框架，可以轻松可靠地处理流数据。它是处理实时数据（例如社交媒体提要、财务数据和传感器数据）的热门选择。

Spring Boot 是一种流行的 Java 框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序。

将 Storm 与 Spring Boot 集成可以让您利用这两个框架的优势。 Storm 提供实时数据处理所需的处理能力和可靠性，而 Spring Boot 使创建和部署应用程序变得容易。

## 先决条件

在我们开始之前，您需要做一些事情：

- Java开发环境
- 阿帕奇行家
- 阿帕奇风暴

## 设置你的项目

让我们从创建一个新的 Maven 项目开始。我们将我们的项目命名为“storm-spring-boot-example”。

在项目的 pom.xml 文件中，我们需要添加以下依赖项：

```xml
<dependencies>
	<dependency>
		<groupId>org.apache.storm</groupId>
		<artifactId>storm-core</artifactId>
		<version>1.1.1</version>
		<scope>provided</scope>
	</dependency>
	<dependency>
		<groupId>org.apache.storm</groupId>
		<artifactId>storm-kafka</artifactId>
		<version>1.1.1</version>
	</dependency>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-web</artifactId>
	</dependency>
</dependencies>
```

storm-core 和 storm-kafka 依赖项由 Apache Storm 提供。 spring-boot-starter-web 依赖项由 Spring Boot 提供。

## 配置风暴

现在我们已经设置了项目，让我们配置 Storm。

我们首先在项目的 src/main/resources 目录中创建一个名为“storm.yaml”的新文件。在这个文件中，我们将添加以下配置：

```yaml
storm.zookeeper.servers:
    - "localhost"
nimbus.seeds: ["localhost"]
storm.local.dir: "target/storm-data"
ui.port: 8080
logging.level: "INFO"
```

此配置告诉 Storm 使用本地 ZooKeeper 服务器并将数据存储在 target/storm-data 目录中。它还将 UI 端口设置为 8080。

## 创建拓扑

现在我们已经配置了 Storm，让我们创建一个拓扑。拓扑是接收数据、处理数据并发出新数据的流处理组件的图形。

我们将首先在项目的 src/main/java/com/example 目录中创建一个名为“Topology.java”的新文件。在这个文件中，我们将添加以下代码：

```java
public class Topology {
	public static void main(String[] args) throws Exception {
		// Create a topology builder
		TopologyBuilder builder = new TopologyBuilder();
		
		// Set the spout
		builder.setSpout("kafka-spout", new KafkaSpout<>(getKafkaSpoutConfig()));
		
		// Set the bolts
		builder.setBolt("bolt1", new Bolt1()).shuffleGrouping("kafka-spout");
		builder.setBolt("bolt2", new Bolt2()).shuffleGrouping("bolt1");
		
		// Submit the topology
		Config config = new Config();
		config.setDebug(true);
		
		StormTopology topology = builder.createTopology();
		
		if (args.length == 0) {
			LocalCluster cluster = new LocalCluster();
			cluster.submitTopology("storm-spring-boot-example", config, topology);
		}
		else {
			StormSubmitter.submitTopology(args[0], config, topology);
		}
	}
	
	private static KafkaSpoutConfig<String, String> getKafkaSpoutConfig() {
		// Configure Kafka
		Map<String, Object> kafkaParams = new HashMap<>();
		kafkaParams.put("bootstrap.servers", "localhost:9092");
		kafkaParams.put("key.deserializer", StringDeserializer.class);
		kafkaParams.put("value.deserializer", StringDeserializer.class);
		kafkaParams.put("group.id", "storm-spring-boot-example");
		kafkaParams.put("auto.offset.reset", "latest");
		kafkaParams.put("enable.auto.commit", false);
		
		// Configure the Kafka spout
		KafkaSpoutConfig<String, String> kafkaSpoutConfig = KafkaSpoutConfig.builder(kafkaParams, getTopicMap())
			.setOffsetCommitPeriodMs(10_000)
			.setFirstPollOffsetStrategy(FirstPollOffsetStrategy.EARLIEST)
			.build();
		
		return kafkaSpoutConfig;
	}
	
	private static Map<String, List<String>> getTopicMap() {
		Map<String, List<String>> topicMap = new HashMap<>();
		topicMap.put("storm-topic", Collections.singletonList("storm-partition"));
		
		return topicMap;
	}
}
```

在此代码中，我们首先创建一个 TopologyBuilder。该构建器将用于构建我们的拓扑。

接下来，我们设置喷嘴。 spout 是一个从外部源读取数据的组件。在本例中，我们使用 KafkaSpout 从 Kafka 读取数据。稍后我们将配置 Kafka spout。

在喷嘴之后，我们设置螺栓。 Bolts是处理数据的组件。在这个拓扑中，我们有两个螺栓。第一个螺栓只是将数据传递给第二个螺栓。第二个螺栓将数据打印到控制台。

最后，我们提交拓扑。如果我们在本地模式下运行，我们将使用 LocalCluster。如果我们在集群模式下运行，我们将使用 StormSubmitter。

## 创建 Kafka spout

现在让我们看一下 Kafka spout 配置。我们首先创建一个 Kafka 参数映射。这些参数将用于配置 Kafka spout。

接下来，我们创建一个 KafkaSpoutConfig。这个配置告诉 Kafka spout 如何连接到 Kafka 以及从哪个主题读取。

## 创建螺栓

现在让我们来看看螺栓。我们首先创建一个 Bolt1 类。这个螺栓只是将数据传递给拓扑中的下一个螺栓。

```java
public class Bolt1 extends BaseRichBolt {
	private OutputCollector collector;
	
	@Override
	public void prepare(Map<String, Object> config, TopologyContext context, OutputCollector collector) {
		this.collector = collector;
	}
	
	@Override
	public void execute(Tuple tuple) {
		collector.emit(tuple, new Values(tuple.getValue()));
		collector.ack(tuple);
	}
	
	@Override
	public void declareOutputFields(OutputFieldsDeclarer declarer) {
		declarer.declare(new Fields("value"));
	}
}
```

接下来，我们创建一个 Bolt2 类。这个螺栓只是将数据打印到控制台。

```java
public class Bolt2 extends BaseRichBolt {
	private OutputCollector collector;
	
	@Override
	public void prepare(Map<String, Object> config, TopologyContext context, OutputCollector collector) {
		this.collector = collector;
	}
	
	@Override
	public void execute(Tuple tuple) {
		System.out.println(tuple.getValue());
		collector.ack(tuple);
	}
	
	@Override
	public void declareOutputFields(OutputFieldsDeclarer declarer) {
		// This bolt does not emit any data
	}
}
```

## 运行拓扑

现在我们已经创建了拓扑，让我们运行它。

如果我们在本地模式下运行，我们可以简单地从我们的 IDE 运行拓扑。 Storm 将启动本地集群并提交拓扑。

如果我们在集群模式下运行，我们需要将我们的拓扑打包成一个 jar 文件并将其提交到集群。我们可以使用以下命令执行此操作：

```
mvn package
storm jar storm-spring-boot-example-0.0.1-SNAPSHOT.jar com.example.Topology storm-topology
```

## 结论

在本文中，我们展示了如何将 Spring Boot 与 Apache Storm 集成以进行实时处理。我们创建了一个从 Kafka 读取数据、处理数据并将其打印到控制台的拓扑。

将 Storm 与 Spring Boot 集成是利用这两个框架优势的好方法。 Storm 提供实时数据处理所需的处理能力和可靠性，而 Spring Boot 使创建和部署应用程序变得容易。